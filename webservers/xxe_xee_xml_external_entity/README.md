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