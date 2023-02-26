# File Inclusion

## Overview

File Inclusion is a common web application vulnerability, which can be easily overlooked as part of the application functionality. Server-side languages such as PHP or JSP can dynamically include external scripts, reducing the script's overall size and simplifying the code. 
If this inclusion logic isn't implemented properly, attackers can include both local and remote files, potentially leading to source code disclosure, sensitive data exposure, and code execution under certain conditions. 
There are two types of file inclusion, namely Local File Inclusion (LFI) and Remote File Inclusion (RFI).

LFI or Local File Inclusion occurs when an attacker is able to get a website to include a file that was not
intended to be an option for this application. A common example is when an application uses the path to a
file as input. If the application treats this input as trusted, and the required sanitary checks are not
performed on this input, then the attacker can exploit it by using the ../ string in the inputted file name
and eventually view sensitive files in the local file system. In some limited cases, an LFI can lead to code
execution as well.

RFI or Remote File Inclusion is similar to LFI but in this case it is possible for an attacker to load a remote
file on the host using protocols like HTTP, FTP etc.

## LFI vs RFI

Almost any Remote File Inclusion (RFI) can also be a Local File Inclusion (LFI); however, any LFI may not be an RFI. This is primarily because of two reasons:

You may only control a portion of the filename and not the entire protocol wrapper (ex: http://, ftp://, https://)

The configuration may prevent RFI all together. For example, in PHP, by setting allow_url_include to 0, it will not be possible to use remote sources within the include() statement.

## Examples of where this vulnerability can happen

The most common place you will find LFI Vulnerabilities is within templating engines. This is because websites want to keep a large majority of the website the same when navigating between pages, such as the header, navigation bar, and footer. Without dynamic page generation, every page on the server would need to be modified when changes are made to any of those sections. This is why you will often see a parameter like /index.php?page=about. Under the hood, index.php will probably pull header.php, about.php, and footer.php. Since you control the about portion of the request, it may be possible to have the webserver grab other files! Another common place is within languages. If you see ?lang=en; then the website will grab files from the /en/ directory.

## Local File Inclusion into Remote Code Execution

LFI can lead to Remote Code Execution (RCE) under some conditions, resulting in a complete server compromise. One common way is to poison log files, which are modified based on requests to the webserver.

## After finding a PHP LFI vulnerability

After finding a LFI, we can try to exploit it by getting the NETNTLMv2 hash by using the tool Responder to load aan SMB URL and then brute force it with john.

We can do this because even if allow_url_include and allow_url_fopen are set to "Off", PHP will not prevent the loading of SMB URLs.

## See Also

	https://book.hacktricks.xyz/pentesting-web/file-inclusion
