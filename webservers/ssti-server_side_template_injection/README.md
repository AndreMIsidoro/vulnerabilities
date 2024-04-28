# SSTI - Server Side Template Injection

## Overview

Server-side template injection is a vulnerability where the attacker injects malicious input into a template in order
to execute commands on the server.

To put it plainly an SSTI is an exploitation technique where the attacker injects native (to the Template
Engine) code into a web page. The code is then run via the Template Engine and the attacker gains code
execution on the affected server.

This attack is very common on Node.js websites and there is a good possibility that a Template Engine is
being used to reflect the email that the user inputs in the contact field.


## Relevant Information

https://book.hacktricks.xyz/pentesting-web/ssti-server-side-template-injection


## Tips

Remember to check the programming language that the server or its framework is running

Encode the input and the payload in url

If there is input validation, try sending some filler but valid input, followed by a special character like ; or \n and then the payload.
