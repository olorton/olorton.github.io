---
layout: post
published: true
title: Adding http basic auth to Django using a view decorator
date: '2020-02-02 07:25:00 +0000'
---

When configuring nginx or apache based servers it is very easy to add http basic auth on to a single view or sub-directory by modifying the config files. These days I'm mostly developing for Heroku which does not allow me to do this, so if I need to add basic auth to a view then I need to add it to the Django app directly.

In this post I'll show you how to add http basic auth to a single Django view using a decorator. Most of the other examples I have seen implement basic auth by returning a user object to the app, in my case I do not want that, but to use a single user name and password that I can set with environment vars and share with the rest of the development team or client. I do not consider these credentials to be super secure because they can be shared widely within a team.

I plan to follow this post with a [middleware example to enable http basic auth on a whole site](/post/2020-02-07-adding-basic-auth-to-django-part-2.html) rather than a single route.

## Step 1

Add some credentials to `settings.py`:

```python
import os

...

HTTP_BASIC_AUTH_USER = os.environ.get("HTTP_BASIC_AUTH_USER", None)
HTTP_BASIC_AUTH_PASS = os.environ.get("HTTP_BASIC_AUTH_PASS", None)
```

## Step 2

Create a `decorators.py` file in your app directory. Here you can add the logic to check that the user is logged in using the basic auth credentials. If they are not it will prompt them to authenticate, if they are, the line `return func(request, *args, **kwargs)` will return the result of the view method.

```python
import base64
from functools import wraps

from django.core.exceptions import PermissionDenied
from django.http import HttpResponse

from config import settings


def http_basic_auth():
    def decorator(func):
        @wraps(func)
        def inner(request, *args, **kwargs):
            if (
                settings.HTTP_BASIC_AUTH_USER is None
                or settings.HTTP_BASIC_AUTH_PASS is None
            ):
                raise PermissionDenied()
            if "HTTP_AUTHORIZATION" in request.META:
                auth = request.META["HTTP_AUTHORIZATION"].split()
                if len(auth) == 2:
                    if auth[0].lower() == "basic":
                        username, password = (
                            base64.b64decode(auth[1]).decode().split(":")
                        )
                        if (
                            username == settings.HTTP_BASIC_AUTH_USER
                            and password == settings.HTTP_BASIC_AUTH_PASS
                        ):
                            return func(request, *args, **kwargs)
            realm = ""
            response = HttpResponse()
            response.status_code = 401
            response["WWW-Authenticate"] = 'Basic realm="%s"' % realm
            return response
        return inner
    return decorator
```

## Step 3

You can finally add your new decorator to your view:

```python
@http_basic_auth
def new_feature(request):
    ...
```
