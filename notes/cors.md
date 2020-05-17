# Cross-Origin Resource Sharing

In this article we're going to talk about Cross-Origin Resource Sharing, a.k.a CORS. What is it? How does it work? Why do we need CORS? We'll answer all of those questions and more. Before we can do that though, we need to cover some basics.

## What happens when you navigate to a web page?

There are a lot of different ways to answer this question. What we need is as simple an answer as is possible, while still providing us enough information to understand CORS. Here goes.

When you navigate to a web page, your browser sends a message to a server.  The server receives the message and sends a message back. Often, the message from the server contains an HTML document. After receiving the HTML document, your browser then sends several other messages, asking for things like CSS files, images, etc. and in the process builds and displays the new page.

MIGHT NEED MORE ABOUT PROXY SERVERS AND MODERN WEB ARCHITECTURE: CDN'S ETC.

Simplified indeed, but good enough for our purposes. Now let's talk about those messages in more detail. 

On the modern web, some of the resources requested by your browser will be served by servers that are between you and the original server. 

## What's an HTTP Request?

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

I know that that looks like a lot, but don't worry. You won't often have to deal directly with headers like these. That's a relief, because, even though only the stating line and host header are required, messages often include a great many headers. (Here's a breakdown of all those headers.)

## What's an HTTP Response?

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

Again, there's a lot there, but you won't often have to deal with those headers directly. (Here's a breakdown of all those headers.)

DO WE NEED TO TALK MORE ABOUT HOW RESOURCES ARE SENT TO THE CLIENT? SESSIONS? COOKIES? AUTHENTICATION? WE'VE COVERED THE BARE ESSENTIALS. THE CLIENT REQUESTS A RESOURCE FROM A SERVER. THE SERVER SENDS IT. WHAT ABOUT THAT REQUIRES SOP AND CORS? IS THERE ANYTHING MORE THE READER NEEDS TO UNDERSTAND.

## Who are the bad guys?

Now we know a bit more about how clients and servers exchange messages and what those message look like. But what does any of that have to do with CORS?

The first tool in the bad guy's tool belt is Cross-Site Scripting, a.k.a. XSS. 

### What is XSS?

Imagine the following scenario. You have three tabs open in your browser. In one tab, you've opened your mail account. In another, you've logged into a social media account. In a third tab, your reading a post on a friend's blog. Your friend's blog site depends on a variety of resources, including CSS files, images, multimedia, and scripts from various places around the web. Furthermore, when your friend built their blog, they used dozens of third-party modules. Each of those resources and modules represents an attack vector. It only takes one polluted resource or module to endanger your data. 

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
