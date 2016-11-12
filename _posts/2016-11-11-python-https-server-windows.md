---
layout: post
title:  "HTTPS server for Python application, on Windows"
categories: Python
---

I found myself needing to serve some files over HTTPS while tinkering with some stuff.
The simplest way to do so in a pure-Python way is described in [this post from 2011](https://www.piware.de/2011/01/creating-an-https-server-in-python/).
However, I'm on Windows and Python 3.5, and those instructions were written with Python 2 and Linux in mind.
Naturally, things didn't quite work out, and I ended up using IIS with a reverse proxy config.

For reference, here's the Python 3 snippet for SimpleHTTPServer over HTTPS:

```python
from http.server import SimpleHTTPRequestHandler, HTTPServer
import ssl

httpd = HTTPServer(('', 4443), Service)
httpd.socket = ssl.wrap_socket(httpd.socket, certfile='server.pem', server_side=True)
httpd.serve_forever()
```

This works for the most part, but for some reason it takes a few seconds to respond,
and will very quickly stop responding at all, causing all requests to time out.

Rather than going down the rabbit hole of issues involving SSL sockets,
I decided to have Python serve over HTTP, and set up an HTTPS reverse proxy to it using IIS.
It's fairly straightforward, and all GUI-based:

1. Install IIS via Add/Remove Windows Features.
2. Get the Web Platform Installer, and use it to install the URL Rewrite and
   Application Request Routing modules.
3. Open IIS Manager. In Server Certificates, run 'Create Self-Signed Certificate...'.
4. In Default Web Site, edit the Site Bindings and add HTTPS ones for the hostnames you need.
   Make sure the hostname(s) will be the ones used to make the request.
   Pick the SSL certificate generated in the previous step.
5. In URL Rewrite, add a Reverse Proxy rule, and point it to `localhost:4443`.
