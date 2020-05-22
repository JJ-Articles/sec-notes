# Cross-Origin Resource Sharing

In this article we're going to talk about Cross-Origin Resource Sharing, a.k.a. CORS. What is it? How does it work? Why do we need CORS? We'll answer all of those questions and more. Before we can do that though, we need to review some basics.

## What happens when you navigate to a web page?

There are a lot of different ways to answer this question. What we need is as simple an answer as is possible, while still providing us enough information to understand CORS. Here goes.

When you navigate to a web page, your browser sends a message to a server.  The server receives the message and sends a message back. Often, the message from the server contains a resource, like an HTML document. Several further exchanges ensue and in the process your browser builds and displays the new page.

Let's talk about those messages in more detail. 

MIGHT NEED MORE ABOUT PROXY SERVERS AND MODERN WEB ARCHITECTURE: CDN'S ETC.
On the modern web, some of the resources requested by your browser will be served by servers that are between you and the original server. 

## What is an HTTP Request?

The message that your browser sends is called an HTTP GET request. Let's talk about each of those terms in turn.

HTTP: HyperText Transfer Protocol (HTTP) provides a set of rules that clients like your browser use to request resources from servers, and that servers use to respond to those requests. The resources in question are things like text files (that includes HTML, CSS, and JavaScript), images, fonts, audio, and video. Other protocols deal with other types of information. 

Request: Let's jump ahead to the request part of HTTP GET request. As we just alluded to, there are two types of HTTP messages: requests and responses. Both message types include three parts - a starting line, followed by one or more headers, followed by an optional body.  In a request, the starting line briefly tells the server what the client wants to do.  The request headers contain more detailed information about the request. Each header is a key-value pair. For example, `Host: example.com`. A typical request might contain a dozen or more headers, providing information about the client, what sorts of data the client will accept, whether the client can accept compressed data, etc. The request body is often empty, but in the case where your client sends a server information from a form, the message body is where the server will find that information.

Get: When a server receives a GET request, it knows that the client is asking it to retrieve and respond with a specific resource from a specific location. The location is indicated by the path parameter that follows GET, in combination with the Host header that appears in the request's headers section. HTTP provides several request methods that a client can use when sending a request to a server. GET and POST are two of the most common. When you navigate to a web page, your browser sends a GET request to a server. When you submit a form, your browser sends a POST request to a server. The other two types of request that you're likely to run into are PUT and DELETE. Together these four request methods allow a client to request that a server retrieve, create, update, or delete a resource. There are other request methods, but we don't need to worry about them now.

Here are the first couple of lines of a GET request to "example.com":

```HTTP
GET / HTTP/1.1 
Host: example.com 
```

If you're curious about the complete request and what each of the headers in it means, here's a breakdown.

## What is an HTTP Response?

As we noted above, the HTTP response message also has a starting line, headers, and body. In a response, we call the starting line the status line. It tells the client whether the request was successful. The headers provide information about the server and the resource sent to the client. The body contains the resource.

Here are the first couple of lines of the response to my request to "example.com":

```HTTP
HTTP/1.1 200 OK
Accept-Ranges: bytes
```

Just like a request, an actual response can contain a dozen headers or more. If you're curious about the complete response and what each of the headers in it mean, here's a breakdown.

## What is the Same Origin Policy?

Now we know a bit more about how clients and servers exchange messages and what those message look like. But what does any of that have to do with CORS? We're getting there. We just need to talk about one more thing- the Same-Origin Policy.

The Same-Origin Policy (SOP) is a browser security feature that attempts to prevent malicious code from interacting with your browser and doing things like stealing sensitive information or tricking you into wiring all of your money to an account in the Cayman Islands. More specifically, the SOP prevents scripts running on one origin from reading data from resources served from a different origin (a.k.a. cross-origin resources). That a complex idea. Let's break it down a bit. 

Reading data from a resource refers to using a scripting language to manipulate the resource. Examples include things like (1) using JavaScript to insert an image from a different origin into a canvas element, (2) using JavaScript to read the contents of an iFrame containing a document from a different origin, and (3) using JavaScript TWO MORE EXAMPLES. 

Just to be clear, the SOP does not prevent a page running on one origin from using ordinary HTML tags like link, script, img, and iframe to embed resources from a different origin. As far as the SOP is concerned, a page served from one origin is free to use CSS files, scripts, and other resources from other origins, as long as those resources are embedded in the page with the proper tags. What the SOP prevents is a script running on the first origin from reading data from those potentially corrupted cross-origin resources. 

The word "origin" appeared ten times in the previous two paragraphs. You might be wondering what it means. An origin is essentially a computer somewhere out there on the internet. More specifically, it's the combination of a scheme, host, and optional port number used to reach resources on that computer. Let's think about http://example.com/example/example-page.html. In this example, the scheme is "http," the host is "example.com," and the port is left undefined. The path "example/example-page.html" is ignored.

Thus, the SOP allows scripts running on http://example.com/exampple/example-page.html to read data from resources served from places like http://example.com/images/ (same scheme, host, and port), but prevents those scripts from interacting with resources from places like https://example.com/ (the scheme has changed from "http" to "https"), http://www.example.com (the subdomain "www" has been added to the domain, thus changing the host), and http://corrupted-site.com (the domain has changed). 


HOW DOES YOUR BROWSER KNOW WHERE A RESOURCE IS FROM THE SAME ORIGIN?

HOW WOULD BAD CODE STEAL YOUR MONEY?

## CORS, finally!

### What is XSS?

Imagine the following scenario. You have three tabs open in your browser. In one tab, you're logged in to your email account. In another, you're logged into a social media account. In a third tab, you're reading a post on a friend's blog. Now imagine that unbeknownst to your friend, their blog contains malicious code. What's to stop that malicious code from stealing the login credentials you used to log in to your mail and social media accounts? In a modern browser, several  

Lot's of things. SOP, CORS, encryption, JWT, OAuth

Your friend's blog site depends on a variety of resources, including CSS files, images, multimedia, and scripts from various places around the web. Furthermore, when your friend built their blog, they used dozens of third-party modules. Each of those resources and modules represents an attack vector. It only takes one polluted resource or module to endanger your data. 
