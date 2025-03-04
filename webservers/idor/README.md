# IDOR - Insecure Direct Object References

## Overview

The very first step of exploiting IDOR vulnerabilities is identifying Direct Object References. Whenever we receive a specific file or resource, we should study the HTTP requests to look for URL parameters or APIs with an object reference (e.g. ?uid=1 or ?filename=file_1.pdf). These are mostly found in URL parameters or APIs but may also be found in other HTTP headers, like cookies.

### Encoding

Suppose the reference was encoded with a common encoder (e.g. base64). In that case, we could decode it and view the plaintext of the object reference, change its value, and then encode it again to access other data. For example, if we see a reference like (?filename=ZmlsZV8xMjMucGRm), we can immediately guess that the file name is base64 encoded (from its character set), which we can decode to get the original object reference of (file_123.pdf). Then, we can try encoding a different object reference (e.g. file_124.pdf) and try accessing it with the encoded object reference (?filename=ZmlsZV8xMjQucGRm), which may reveal an IDOR vulnerability if we were able to retrieve any data.