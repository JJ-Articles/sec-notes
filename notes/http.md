# Cross-Origin Resource Sharing

In this article we're going to talk about Cross-Origin Resource Sharing, a.k.a CORS. What is it? How does it work? Why do we need CORS? We'll answer all of those questions and more. Before we can do that though, we need to cover some basics.

## What happens when you navigate to a web page?

There are a lot of different ways to answer this question. What we need is an answer that will help us understand CORS. Here's a simplified explanation that will help us later.

When you navigate to a web page, your browser sends a message to a server.  The server receives the message and sends a message back. Often, the message from the server contains an HTML document. After receiving the HTML document, your browser then sends several other messages, asking for things like CSS files, images, etc. and in the process builds and displays the new page.

Simplified indeed, but good enough for our purposes. Now let's talk about those messages in more detail. 

## HTTP Requests

The message that your browser sends is called an **HTTP GET request**. Let's break that down.

**HTTP** is a protocol that specifies how a client and a server can go about exchanging certain kinds of information. The HTTP protocol deals with HTML documents, images, and a few other things. Other protocols deal with other types of information. For example, mailto and FTP deal with email and files, respectively. 

Let's skip to the **request** part of "HTTP GET request" for a minute. There are two types of HTTP messages: requests and responses. Both message types include three parts - a starting line, some headers, and an optional body.  In a request, the **starting line** very briefly tells the server what the client would like to do.  The request **headers** contain more detailed information about exactly what the client wants. For example, the client might want a document that's available only if the client has proper credentials. The request headers are where the client supplies that sort of information. The request **body** is often empty, but in the case where your client sends a server information from a form, the message body is where the server will find that information.

Now let's return to the **GET** portion of "HTTP GET request." HTTP defines several request methods. GET and POST are two of the most common. When you navigate to a web page, your browser sends a GET request to a server. When you submit a form, your browser sends a POST request to a server. The other two types of request that you're likely to run into are UPDATE and DELETE. Together these four request methods allow a client to create, read, update, and delete resources, as long as the server accepts those requests.

Here's what the GET request to "example.com" looks like when I type the URL into my address bar in Google Chrome on Windows:

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

I know that that looks like a lot, but don't worry. You won't often have to deal directly with headers like these. That's a relief, because, even though only the stating line and host header are required, messages often include a great many headers. 

### What do all those headers mean?
 
- "Host: example.com" provides the domain name of the sought after page. 
- "Connection: keep-alive" asks the server not to immediately terminate the connection it has with the client after responding to the request. 
- "Pragma: no-cache" and "Cache-Control: no-cache" both ask the server to specify in its response that the response should not be used by the client to fulfill subsequent requests without first checking in with the server. 
- "DNT: 1" asks the server not to track the client's user information.
- "Upgrade-Insecure-Requests: 1" asks the server to respond over a secure https connection, if one is available.
- User-Agent tells the server a bit more about the client making the request.
- Accept tells the server what sort of data the client will accept.
- "Accept-Encoding: gzip, deflate" tells the server that it can feel free to compress its response.
- Accept-Language: en-US,en;q=0.9 tells the server the client's preferred languages.

## HTTP Responses

So, we've covered how a client sends a request message to a server, but we haven't talked about how the server responds. As we noted above, the HTTP response message also has a starting line, headers, and body. In a response, we call the starting line the status line. It tells the browser whether the request was successful. The headers provide information about the server and the resource sent to the client. The body contains the resource.

Here's what the status line and headers in the response to my request to "example.com" look like:

```HTTP
HTTP/1.1 200 OK
Accept-Ranges: bytes
Age: 461924
Cache-Control: max-age=604800
Content-Type: text/html; charset=UTF-8
Date: Wed, 13 May 2020 16:50:48 GMT
Etag: "3147526947"
Expires: Wed, 20 May 2020 16:50:48 GMT
Last-Modified: Thu, 17 Oct 2019 07:18:26 GMT
Server: ECS (bsa/EB24)
Vary: Accept-Encoding
X-Cache: HIT
Content-Length: 1256
```

### What do all those headers mean?
 
- "Accept-Ranges: bytes" tells the client that the server allows things like pausing and resuming a large download.
- "Age: 461924" tells the client that the resource has been a proxy server's cache for around 12 hours.
- The Cache-Control header with a max-age directive and the Expires header tell the client when the resource is considered stale. The Cache-Control header actually makes the Expires header irrelevant.
- "Content-Type: text/html; charset=UTF-8" tells the client that the resource is an HTML document.
- The Date header tells the client when the response was sent.
- The Etag is a unique identifier for this version of the resource.
- Last-Modified tells the client when the resource was last modified.
- "Server: ECS (bsa/EB24)" tells the client that the resource is hosted on Amazon's ECS.
- "Vary: Accept-Encoding" is a message for proxy servers that may be storing a cached version of certain resources. This header tells the proxy to store both compressed and uncompressed versions of the resource in cache.
- "X-Cache: HIT" is a message from a proxy server that tells your client that the resource was served from the proxy server and not from the destination server.
- "Content-Length: 1256" tells the client the size of the resource in the response message body.

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
