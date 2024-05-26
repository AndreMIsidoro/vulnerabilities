# DEP - Data Execution Prevention

## Overview

Data Execution Prevention (DEP) is a technology built into Windows that helps protect you from executable code launching from places it's not supposed to. DEP does that by marking some areas of your PC's memory as being for data only, no executable code or apps will be allowed to run from those areas of memory.

This is designed to make it harder for attacks that try to use buffer overflows, or other techniques, to run their malware from those parts of memory that normally only contain data.



## ASLR

## Overview

Address space layout randomization (ASLR) is a computer security technique involved in preventing exploitation of memory corruption vulnerabilities. In order to prevent an attacker from reliably redirecting code execution to, for example, a particular exploited function in memory, ASLR randomly arranges the address space positions of key data areas of a process, including the base of the executable and the positions of the stack, heap and libraries.