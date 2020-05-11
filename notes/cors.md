# Cross-Origin Resource Sharing

In this article we're going to talk about Cross-Origin Resource Sharing, a.k.a CORS. What is it? How does it work? Why do we need CORS? We'll answer all of those questions and more. Before we can do that though, we need to cover some basics.

## What happens when you navigate to a web page?

There are a lot of different ways to answer this question. What we need is an answer that will help us understand CORS. Here's a quick and dirty explanation that will help us later.

When you navigate to a web page, your browser sends a message to a server.  The server receives the message and sends a message back. Often, the message from the server contains an HTML document. After receiving the HTML document, your browser then sends several other messages, asking for things like CSS files, images, etc. and in the process builds and displays the new page.

Quick and dirty indeed, but good enough for our purposes. 

Let's talk about those messages. The message that your browser sends is called an HTTP GET request. Let's break that down.

HTTP is a protocol that specifies how a client and a server can go about exchanging certain kinds of information. The HTTP protocol deals with HTML documents, images, and a few other things. Other protocols deal with still more types of information. For example, mailto and FTP deal with email and files, respectively. 

Let's skip to the "request" part of "HTTP GET request" for a minute. There are two types of HTTP messages: requests and responses. Both message types include three parts - a starting line, some headers, and an optional body.  In a request, the starting line tells the server what the client would like to do. Maybe the client wants an HTML document. Maybe it wants to send the server information from a form you filled out. The request headers contain more detailed information about exactly what the client wants. Maybe the client wants an image that's only available from a second server located somewhere else. Maybe it wants a document that is available only to a client with proper credentials. The request headers are where the client supplies that sort of information. The request body is often empty, but in the case where your client is sending a server information from a form, the message body is where the server will find that information.

Now let's return to the "GET" portion of "HTTP GET request." HTTP specifies a set of operations that clients can perform. GET and POST are two of the most common. When you navigate to a web page, your browser sends a GET request to a server. When you submit a form, your browser sends a POST request to a server.

Here's an example of a GET request to "example.com" using Google Chrome on Windows:

```HTTP
GET / HTTP/1.1 
Host: example.com 
Connection: keep-alive 
Pragma: no-cache 
Cache-Control: no-cache 
DNT: 1 
Upgrade-Insecure-Requests: 1 
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/81.0.4044.138 Safari/537.36 
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.9 
Accept-Encoding: gzip, deflate 
Accept-Language: en-US,en;q=0.9
```

How does a server respond to your browser's request?

## What is the same-origin policy?
Short version: The same-origin-policy prevents bad guys from hacking your browser and doing all sorts of horrible things like stealing your credit card information. 

ensures that only resources from the "origin"  serving the document you are currently looking at are allowed to run in your browser. It prevents resources from other servers

## Why do we need it?
Because, without the same-origin policy, the page you are currently looking at in your browser could be used to run malicious code, and that code could, for example, access and interact with other open tabs in your browser, including your email services, banking services, etc.


## What is the same-origin policy?
Short version: The same-origin-policy prevents bad guys from hacking your browser and doing all sorts of horrible things like stealing your credit card information. 

ensures that only resources from the "origin"  serving the document you are currently looking at are allowed to run in your browser. It prevents resources from other servers

## Why do we need it?
Because, without the same-origin policy, the page you are currently looking at in your browser could be used to run malicious code, and that code could, for example, access and interact with other open tabs in your browser, including your email services, banking services, etc.
