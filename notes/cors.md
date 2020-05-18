# Cross-Origin Resource Sharing

In this article we're going to talk about Cross-Origin Resource Sharing, a.k.a CORS. What is it? How does it work? Why do we need CORS? We'll answer all of those questions and more. Before we can do that though, we need to cover some basics.

## What happens when you navigate to a web page?

There are a lot of different ways to answer this question. What we need is as simple an answer as is possible, while still providing us enough information to understand CORS. Here goes.

When you navigate to a web page, your browser sends a message to a server.  The server receives the message and sends a message back. Often, the message from the server contains an HTML document. Several further exchanges ensure and in the process your browser builds and displays the new page.

Let's talk about those messages in more detail. 

MIGHT NEED MORE ABOUT PROXY SERVERS AND MODERN WEB ARCHITECTURE: CDN'S ETC.
On the modern web, some of the resources requested by your browser will be served by servers that are between you and the original server. 

## What is an HTTP Request?

The message that your browser sends is called an **HTTP GET request**. Let's break that down.

**HyperText Transfer Protocol** (HTTP) specifies how a client and server exchange information. The HTTP protocol deals with, among other things, HTML documents, CSS files, and images. Other protocols deal with other types of information. For example, mailto and FTP deal with email and files, respectively. 

Let's skip to the **request** part of "HTTP GET request" for a minute. There are two types of HTTP messages: requests and responses. Both message types include three parts - a starting line, some headers, and an optional body.  In a request, the **starting line** very briefly tells the server what the client would like to do.  The request **headers** contain more detailed information about exactly what the client wants. For example, the client might want a document that's available only if the client has proper credentials. The request headers are where the client supplies that sort of information. The request **body** is often empty, but in the case where your client sends a server information from a form, the message body is where the server will find that information.

Now let's return to the **GET** portion of "HTTP GET request." HTTP defines several request methods. GET and POST are two of the most common. When you navigate to a web page, your browser sends a GET request to a server. When you submit a form, your browser sends a POST request to a server. The other two types of request that you're likely to run into are UPDATE and DELETE. Together these four request methods allow a client to create, read, update, and delete resources.

Here are the first couple of lines of a GET request to "example.com":

```HTTP
GET / HTTP/1.1 
Host: example.com 
```

If you're curious about the complete request and what each of the header in it mean, here's a breakdown.

## What is an HTTP Response?

So, we've covered how a client sends a request message to a server, but we haven't talked about how the server responds. As we noted above, the HTTP response message also has a starting line, headers, and body. In a response, we call the starting line the status line. It tells the browser whether the request was successful. The headers provide information about the server and the resource sent to the client. The body contains the resource.

Here are the first couple of lines of the response to my request to "example.com":

```HTTP
HTTP/1.1 200 OK
Accept-Ranges: bytes
```

If you're curious about the complete request and what each of the header in it mean, here's a breakdown.

DO WE NEED TO TALK MORE ABOUT HOW RESOURCES ARE SENT TO THE CLIENT? SESSIONS? COOKIES? AUTHENTICATION? WE'VE COVERED THE BARE ESSENTIALS. THE CLIENT REQUESTS A RESOURCE FROM A SERVER. THE SERVER SENDS IT. WHAT ABOUT THAT REQUIRES SOP AND CORS? IS THERE ANYTHING MORE THE READER NEEDS TO UNDERSTAND.

## What is the Same Origin Policy?

Now we know a bit more about how clients and servers exchange messages and what those message look like. But what does any of that have to do with CORS? We're getting there! We just need to talk about a couple more things. First, we need to talk about the Same-Origin Policy.

The Same-Origin Policy (SOP) is a browser security feature that attempts to prevent malicious code from interacting with your browser and doing things like telling your bank to wire a thousand dollars to the Caymans. 

More specifically, the SOP prevents scripts running on http://example.com/example-page.html (let's call it Example Page) from reading data from resources served from a different origin. Let's break that down a bit. Reading data from a resource includes things like using JavaScript to insert an image from a different origin into a canvas element. TWO MORE EXAMPLES. Next, an origin is essentially a computer somewhere on the internet. More specifically, it's the combination of a scheme, host, and optional port number used to reach resources on that computer. Using the URL above, the scheme is "http," the host is "example.com," and the port is left off. Thus, the SOP allows scripts running on "Example Page" to read data from resources served from places like http://example.com/images/, but prevents those scripts from interacting resources from places like https://example.com/ (the scheme has changed from "http" to "https"), http://www.example.com (the subdomain "www" has been added to the domain, thus changing the host), and http://corrupted-site.com (the domain has changed). 

Just to be clear, "Example Page" can embed resources from corrupted-site.com by using HTML tags like link, script, img, and iframe. What the SOP prevents is a script running on Example Page from interacting those potentially corrupted resources. 

### What is XSS?

Imagine the following scenario. You have three tabs open in your browser. In one tab, you're logged in to your email account. In another, you're logged into a social media account. In a third tab, you're reading a post on a friend's blog. Now imagine that unbeknownst to your friend, their blog contains malicious code. What's to stop that malicious code from stealing the login credentials you used to log in to your mail and social media accounts? In a modern browser, several  

Lot's of things. SOP, CORS, encryption, JWT, OAuth

Your friend's blog site depends on a variety of resources, including CSS files, images, multimedia, and scripts from various places around the web. Furthermore, when your friend built their blog, they used dozens of third-party modules. Each of those resources and modules represents an attack vector. It only takes one polluted resource or module to endanger your data. 

## Why do we need it?
Because, without the same-origin policy, the page you are currently looking at in your browser could be used to run malicious code, and that code could, for example, access and interact with other open tabs in your browser, including your email services, banking services, etc.


## What is the same-origin policy?
Short version: The same-origin-policy prevents bad guys from hacking your browser and doing all sorts of horrible things like stealing your credit card information. 

ensures that only resources from the "origin"  serving the document you are currently looking at are allowed to run in your browser. It prevents resources from other servers

## Why do we need it?
Because, without the same-origin policy, the page you are currently looking at in your browser could be used to run malicious code, and that code could, for example, access and interact with other open tabs in your browser, including your email services, banking services, etc.
