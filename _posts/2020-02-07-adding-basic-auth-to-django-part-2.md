---
layout: post
published: true
title: Adding site-wide http basic auth to Django using middleware
date: '2020-02-07 13:25:00 +0000'
---

In this post I'll show you how to add site wide basic auth to a Django web app without utilising or interfering with any existing Django authentication systems that you might already have set up.

If you just want to restrict access to a single route, and again you do not want to involve the Django user system, then you might want to look at my last post where I describe [how to use decorators to apply http basic auth](/post/2020-02-02-adding-basic-auth-to-django-part-1.html).

## Step 1

Add some credentials to `settings.py`:

```python
import os

...

HTTP_BASIC_AUTH_USER = os.environ.get("HTTP_BASIC_AUTH_USER", None)
HTTP_BASIC_AUTH_PASS = os.environ.get("HTTP_BASIC_AUTH_PASS", None)
SITE_WIDE_HTTP_BASIC_AUTH = (
    os.environ.get("SITE_WIDE_HTTP_BASIC_AUTH", "false") == "True"
)
```

## Step 2

Create a `middleware.py` file in your app directory. Here you can add the logic to check that the user is logged in using the basic auth credentials. If they are not it will prompt them to authenticate, if they are, the line `return self.get_response(request)` will return the result of the view method.

```python
import base64

from django.http import HttpResponse

from config import settings


class SiteWideHttpBasicAuth:
    def __init__(self, get_response):
        self.get_response = get_response
        # One-time configuration and initialization.

    def __call__(self, request):
        if not settings.SITE_WIDE_HTTP_BASIC_AUTH:
            return self.get_response(request)
        if (
            settings.HTTP_BASIC_AUTH_USER is None
            or settings.HTTP_BASIC_AUTH_PASS is None
        ):
            raise PermissionDenied()
        if "HTTP_AUTHORIZATION" in request.META:
            auth = request.META["HTTP_AUTHORIZATION"].split()
            if len(auth) == 2:
                if auth[0].lower() == "basic":
                    username, password = base64.b64decode(auth[1]).decode().split(":")
                    if (
                        username == settings.HTTP_BASIC_AUTH_USER
                        and password == settings.HTTP_BASIC_AUTH_PASS
                    ):
                        return self.get_response(request)
        realm = ""
        response = HttpResponse()
        response.status_code = 401
        response["WWW-Authenticate"] = 'Basic realm="%s"' % realm
        return response
```
