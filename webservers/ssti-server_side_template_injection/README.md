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
