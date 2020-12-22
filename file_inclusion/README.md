# File Inclusion

## Overview

	File Inclusion is a common web application vulnerability, which can be easily overlooked as part of the application functionality. Server-side languages such as PHP or JSP can dynamically include external scripts, reducing the script's overall size and simplifying the code. If this inclusion logic isn't implemented properly, attackers can include both local and remote files, potentially leading to source code disclosure, sensitive data exposure, and code execution under certain conditions. There are two types of file inclusion, namely Local File Inclusion (LFI) and Remote File Inclusion (RFI).

## LFI vs RFI

	Almost any Remote File Inclusion (RFI) can also be a Local File Inclusion (LFI); however, any LFI may not be an RFI. This is primarily because of two reasons:

	You may only control a portion of the filename and not the entire protocol wrapper (ex: http://, ftp://, https://)

	The configuration may prevent RFI all together. For example, in PHP, by setting allow_url_include to 0, it will not be possible to use remote sources within the include() statement.
