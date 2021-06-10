---
layout: post
published: true
title: Kubernetes load balancing test
date: '2021-06-10 12:17:51 +0000'
---

In this post I will run through the steps to build a basic Kubernetes deployment that allows me to verify that the load balancer is balancing traffic between pods in an roughly even manner. Parts of this document are verbose as I am re-familiarizing myself with K8s after too many years of not using it.

### Sources

- [kubernetes.io/docs/tutorials/hello-minikube/](https://kubernetes.io/docs/tutorials/hello-minikube/)
- [someweb.github.io/devops/ingress-nodejs-app-kubernetes/](https://someweb.github.io/devops/ingress-nodejs-app-kubernetes/)

## NodeJS app

A basic NodeJS app has been created, which on startup creates a unique ID and returns that ID on every subsequent http request. This will be used later for verifying that the pods are evenly load balanced.

The code for this is here: [app/index.js](https://github.com/olorton/k8s-load-balancing-test/blob/main/app/index.js)

The container for this is on [Docker Hub](https://hub.docker.com/r/olorton/load-balancing-test-app)

## Start Minikube

    minikube start --vm=true --cpus 4 --memory 4098

Create a namespace for our project:

    kubectl create namespace lb-test

## K8s Deployment

### Pods

Config file: [deployment.yaml](https://github.com/olorton/k8s-load-balancing-test/blob/main/deployment.yaml)

To start with, a replica of two pods containing our NodeJS app have been configured. Having at least two pods is necessary to verify that the load balancer is balancing the traffic at a later step. The container port 3000 is exposed so that the app can receive connection from within the cluster.

Apply this configuration: `kubectl apply -f deployment.yaml`

Verify that these two pods have started:

    $ kubectl get pods -n lb-test
    NAME                                       READY   STATUS    RESTARTS   AGE
    load-balancing-test-app-8468bd8785-sjtn8   1/1     Running   0          19s
    load-balancing-test-app-8468bd8785-t62vh   1/1     Running   0          19s

### Service (Load balancer)

Config file: [service.yaml](https://github.com/olorton/k8s-load-balancing-test/blob/main/service.yaml)

This creates a new service, a load balancer, which balances traffic from port 80 to port 3000 of all pods labeled `load-balancing-test-app`.

Apply this configuration: `kubectl apply -f service.yaml`

Verify that this configuration has been applied:

    $ kubectl get service -n lb-test
    NAME                      TYPE           CLUSTER-IP     EXTERNAL-IP   PORT(S)        AGE
    load-balancing-test-app   LoadBalancer   10.96.65.215   <pending>     80:30793/TCP   7s

At this point the external IP is pending and not available. This is because Minikube is being used to manage the cluster and assign the external IP. To expose the external IP, run: `minikube tunnel`. Leave this process running to maintain the external IP address.

    $ kubectl get service -n lb-test
    NAME                      TYPE           CLUSTER-IP     EXTERNAL-IP    PORT(S)        AGE
    load-balancing-test-app   LoadBalancer   10.96.65.215   10.96.65.215   80:30793/TCP   88s

The external IP has now been resolved and curl can be used to connect to the application pods via the load balancer service.

    $ curl 10.96.65.215
    App id: 562704180445

### Ingress

Config file: [ingress.yaml](https://github.com/olorton/k8s-load-balancing-test/blob/main/ingress.yaml)

By creating the pods and a load balancer service, there are now enough components to complete this K8s build and verify the load balancer service works as expected. However, this can be improved by using an ingress so that the app can be accessed using a domain name rather than an IP address.

Apply this configuration: `kubectl apply -f ingress.yaml`

Enable the ingress addon for Minikube:

    $ minikube addons enable ingress
    🔎  Verifying ingress addon...
    🌟  The 'ingress' addon is enabled

Verify that this configuration has been applied:

    $ kubectl get ingress -n lb-test
    NAME             CLASS    HOSTS         ADDRESS          PORTS   AGE
    mynode-ingress   <none>   lb-test.dev   192.168.99.100   80      104m

Add the domain and IP address to the local `/etc/hosts` file:

    192.168.99.100 lb-test.dev

Verify the connection to the NodeJS app container using this new domain:

    $ curl lb-test.dev
    App id: 562704180445

## Verifying the Load Balancer works as expected

There are three different ways to verify that the load is being distributed over the different pods, as expected:

- Verifying the service is correctly configured
- Verifying the pods are returning different IDs in their responses
- Verifying the pods are logging different IDs

### Verifying the service is correctly configured

Verify that the K8s Load Balancer service is set up and configured using the `kubectl describe` command:

    $ kubectl describe service load-balancing-test-app -n lb-test
    Name:                     load-balancing-test-app
    Namespace:                lb-test
    Labels:                   <none>
    Annotations:              <none>
    Selector:                 app=load-balancing-test-app
    Type:                     LoadBalancer
    IP Families:              <none>
    IP:                       10.96.65.215
    IPs:                      10.96.65.215
    LoadBalancer Ingress:     10.96.65.215
    Port:                     <unset>  80/TCP
    TargetPort:               3000/TCP
    NodePort:                 <unset>  30793/TCP
    Endpoints:                172.17.0.3:3000,172.17.0.4:3000
    Session Affinity:         None
    External Traffic Policy:  Cluster
    Events:                   <none>

There are a few important lines in this output that demonstrate that the service is set up correctly.

    Type:                     LoadBalancer
    Port:                     <unset>  80/TCP
    TargetPort:               3000/TCP
    Endpoints:                172.17.0.3:3000,172.17.0.4:3000
    External Traffic Policy:  Cluster

These lines could be described in English as: There is a load balancer service, listening on the default http port, and evenly distributing all traffic to the two application pods on port 3000.

The line `External Traffic Policy:  Cluster` is interesting because this describes the traffic as being _evenly distributed_ between each endpoint within the cluster (default behavior).

### Verifying the pods are returning different IDs in their responses

You will remember that each application pod returns a unique ID when that page is requested over http. Curl can be run in a loop to verify that the traffic is being evenly distributed.

    $ for i in {1..20}; do echo "$(curl -s lb-test.dev)"; done
    App id: 368797613483
    App id: 767595446753
    App id: 368797613483
    App id: 767595446753
    App id: 767595446753
    App id: 767595446753
    App id: 767595446753
    App id: 368797613483
    App id: 767595446753
    App id: 368797613483
    App id: 368797613483
    App id: 368797613483
    App id: 767595446753
    App id: 368797613483
    App id: 767595446753
    App id: 767595446753
    App id: 368797613483
    App id: 767595446753
    App id: 767595446753
    App id: 368797613483

### Verifying the pods are logging different IDs

There should also be IDs logged after each http request:

    $ kubectl logs -l app=load-balancing-test-app -n lb-test

    listening on 3000, app id: 368797613483
    App id: 368797613483
    App id: 368797613483
    App id: 368797613483
    App id: 368797613483
    App id: 368797613483
    App id: 368797613483
    App id: 368797613483
    App id: 368797613483
    App id: 368797613483
    listening on 3000, app id: 767595446753
    App id: 767595446753
    App id: 767595446753
    App id: 767595446753
    App id: 767595446753
    App id: 767595446753
    App id: 767595446753
    App id: 767595446753
    App id: 767595446753
    App id: 767595446753
    App id: 767595446753
    App id: 767595446753

### Verifying these checks still apply when scaling up

Kubernetes is a valuable tool because it is often necessary to scale up/down resources to meet changing demands. By adding another pod and re-running these verifications it is possible to verify that the load balancer continues to spread the traffic over all all of it's pods. To do this, first modify `deployment.yaml` so that `spec.replicas` is changed from 2 to 3, and re-apply the config:

    $ kubectl apply -f deployment.yaml
    deployment.apps/load-balancing-test-app configured

Verify that the third pod is up and running:

    $ kubectl get pods -n lb-test
    NAME                                       READY   STATUS    RESTARTS   AGE
    load-balancing-test-app-8468bd8785-sjtn8   1/1     Running   0          32m
    load-balancing-test-app-8468bd8785-t62vh   1/1     Running   0          32m
    load-balancing-test-app-8468bd8785-vlklz   1/1     Running   0          6s

Verify that the third pod is included in the load balancer service:

    $ kubectl describe service load-balancing-test-app -n lb-test
    Name:                     load-balancing-test-app
    Namespace:                lb-test
    Labels:                   <none>
    Annotations:              <none>
    Selector:                 app=load-balancing-test-app
    Type:                     LoadBalancer
    IP Families:              <none>
    IP:                       10.96.65.215
    IPs:                      10.96.65.215
    LoadBalancer Ingress:     10.96.65.215
    Port:                     <unset>  80/TCP
    TargetPort:               3000/TCP
    NodePort:                 <unset>  30793/TCP
    Endpoints:                172.17.0.3:3000,172.17.0.4:3000,172.17.0.6:3000
    Session Affinity:         None
    External Traffic Policy:  Cluster
    Events:                   <none>

Verify that the curl loop now returns three different app ids, rather than just two:

    $ for i in {1..20}; do echo "$(curl -s lb-test.dev)"; done
    App id: 767595446753
    App id: 767595446753
    App id: 368797613483
    App id: 245752426860
    App id: 368797613483
    App id: 368797613483
    App id: 767595446753
    App id: 368797613483
    App id: 245752426860
    App id: 245752426860
    App id: 767595446753
    App id: 245752426860
    App id: 368797613483
    App id: 245752426860
    App id: 767595446753
    App id: 368797613483
    App id: 767595446753
    App id: 767595446753
    App id: 368797613483
    App id: 368797613483


And that the logs show three different IDs:

    $ kubectl logs -l app=load-balancing-test-app -n lb-test

    App id: 767595446753
    App id: 767595446753
    App id: 767595446753
    App id: 767595446753
    App id: 767595446753
    App id: 767595446753
    App id: 767595446753
    App id: 767595446753
    App id: 767595446753
    App id: 767595446753
    App id: 368797613483
    App id: 368797613483
    App id: 368797613483
    App id: 368797613483
    App id: 368797613483
    App id: 368797613483
    App id: 368797613483
    App id: 368797613483
    App id: 368797613483
    App id: 368797613483
    App id: 245752426860
    App id: 245752426860
    App id: 245752426860
    App id: 245752426860
    App id: 245752426860
    App id: 245752426860
    App id: 245752426860
    App id: 245752426860
    App id: 245752426860
    App id: 245752426860
