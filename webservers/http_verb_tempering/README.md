# HTTP Verb Tempering

## Overview

HTTP Verb Tampering is a web application attack where an attacker manipulates the HTTP method (verb) (like GET, POST, PUT, DELETE, etc.) to bypass security controls or access unintended functionality.

If the server does not properly enforce method handling, an attacker might:

- Change a GET request to a DELETE request.
- Use HEAD, OPTIONS, or uncommon verbs to interact with endpoints in unexpected ways.
- Bypass protections by sending a POST request to an endpoint that was only meant to allow GET

For instance if we try a GET in a page, but we don't have permissions to request it (403), we can try a HEAD verb to see if we can bypass the permission check.

The other and more common type of HTTP Verb Tampering vulnerability is caused by Insecure Coding errors made during the development of the web application, which lead to web application not covering all HTTP methods in certain functionalities. This is commonly found in security filters that detect malicious requests. For example, if a security filter was being used to detect injection vulnerabilities and only checked for injections in POST parameters (e.g. $_POST['parameter']), it may be possible to bypass it by simply changing the request method to GET.

## Identification

```shell
curl -i -X OPTIONS http://SERVER_IP:PORT/
```
```
HTTP/1.1 200 OK
Date: 
Server: Apache/2.4.41 (Ubuntu)
Allow: POST,OPTIONS,HEAD,GET
Content-Length: 0
Content-Type: httpd/unix-directory
```