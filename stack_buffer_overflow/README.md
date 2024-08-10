# Stack Buffer Overflow

## Controlling the EIP

Getting control of the EIP register is a crucial step of exploit development. There are two common ways to do this:

We can find the EIP by sending a unique string of bytes, identify the 4 bytes that overwrite the EIP, and then locate those four bytes in our unique buffer.
pattern_create.rb is a ruby tool part of metasploit the allows us to do this:

	locate pattern_create

	pattern_create.rb <number_of_bytes>

After identifying which bytes overwrote the EIP register we can now use the companion to pattern_create: pattern_offset.rb. This tool will discover the offset of the specific 4 bytes that overwrote the EIP in our unique string

	pattern_offset.rb <bytes>

Where do we redirect the execution flow now that we control the EIP register? Part of our buffer can contain the code (or shellcode) we would like to have executed. Our next steps will involve examining and preparing the psace for this shellcode, and figuring out a way to redirect code execution to it.


## Checking for bad characters

Thera maybe some characters that should be used in the buffer, return address or shellcode.
To find these characters just find a script that sends all possible characters from 0x00 to 0xff as part of the buffer and see how they are dealt by the application. If any of the characters don't appear, they were truncated and should not be used.