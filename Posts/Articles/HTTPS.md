---
id: https
title: "Computer Networks: HTTPS Basics"
description: "What is HTTPS?"
tags:
  - http
  - https
  - networking
  - ssl
image: "/content/cover/https.png"
cover_image: https://raw.githubusercontent.com/oneminch/portfolio/main/public/content/cover/https.png
canonical_url: https://minch.dev/blog/https
series: Computer Networks
navOrder: 3
published_on: "2022-03-28"
---

**HTTPS** is a protocol which is an improvement over HTTP and is the short form of **HyperText Transfer Protocol Secure** (HTTP + SSL). In this article, we will look at the shortcomings of HTTP which lead to the development of HTTPS and some basic ideas behind HTTPS. It'll cover these sub topics:

- Drawbacks of HTTP
- HTTPS as the solution
- HTTPS = HTTP + SSL
- Limitations of HTTPS

As introduced in [this article about HTTP](https://dev.to/oneminch/http-basics-nji), HTTP is a protocol of the web that allows communication between devices. It is the technology behind the requests and responses made on the web. Once the client device has identified the server address, it works by opening a connection tunnel to the server, so the intended requests are made.

## Drawbacks of HTTP

HTTP requests are not considered safe since they can be easily intercepted and manipulated by anyone on the network. A very common analogy to describe plain HTTP is the use of pipes as a means of communication. Imagine a transparent glass pipe that connects two points. Everything sent between anyone from one point to the other can be seen passing through the pipe. A person standing in the middle can see the things passing through the transparent pipe. This is how plain HTTP requests work. There is no layer of security to hide the contents of requests and responses. Data can be tampered with or snooped on by any party on the network like Internet Service Providers (ISPs), malicious hackers or even employers. Therefore, sensitive data like financial information and website passwords should not be transferred over just HTTP.

Another drawback is that **someone on the network can manipulate the requests**, so they can insert ads, or inject code to serve phishing sites or just steal user information. In HTTP, if you visit a site, lets say, a shopping site, there is no way to actually verify that the site that you are visiting is the site you wanted to visit. In other words, the website you get if you wanted to go to http://dev.to, might not be the actual website. It can be a forged site injected by some entity along the network to trick users into giving away personal information. All these problems make plain HTTP a less ideal way to communicate on the web.

## The Solution: HTTPS

This is where **HTTPS** comes in. HTTPS is an extension of HTTP and it makes sure the there is a secure communication over the network. HTTPS is not actually a separate protocol from HTTP. It is the same protocol except the connection is encrypted unlike plain HTTP where the connection is unencrypted. Request and response messages include components like headers and a body. All data like request messages get encrypted before they leave the sender. Going back to our pipe analogy, HTTPS can be imagined as being an opaque metal or plastic pipe. This means that the contents of the messages transferred are hidden from visibility and manipulation.

## HTTPS = HTTP + SSL

HTTPS uses a cryptographic protocol known as TLS (Transport Layer Security) to encrypt transactions. Originally, what it used was known as SSL (Secure Sockets Layer), which later evolved to TLS. Thus, it's sometimes referred to as HTTP over SSL or HTTP over TLS. Even though SSL and TLS refer to much different versions of the same protocol, the terms are often used interchangeably. This protocol ensures data security when it is transferred over a network which means protection from issues like potential eavesdropping and man-in-the-middle attacks because of end-to-end encryption between client and server.

In addition to protecting eavesdropping, HTTPS guarantees the request/response is delivered to the right recipient. It verifies the authenticity of all the entities involved in the process. For a website to be secured with HTTPS in a user's browser, it needs to provide a form of authentication to prove that it is the actual website that belongs to the actual server. To ensure this, it requires the server to install what is known as a _certificate_ which is a unique cryptographic key and have it signed by an entity known as a _certificate authority_. The administrator of the website can ask the _certificate authority_ to issue a _certificate_. In other words, a certificate is a way of saying if a browser is opened at https://duckduckgo.com, then it is really on the official site for DuckDuckGo.

As mentioned above, SSL is the protocol used for transmitting data over the Internet securely. Before getting to the request and response transaction over SSL, a server needs to prove it is the legitimate one the client wants to communicate with. The server sends its SSL certificate to the browser which then checks if that server is who it says it is. Once the browser has verified the identity of the server, they use cryptographic keys to proceed with the data exchange.

This video explains well how SSL encryption works.

<iframe title="vimeo-player" src="https://player.vimeo.com/video/239132801?h=4bbba48a70" width="640" height="360" frameborder="0" allowfullscreen>DigiCert - # What is SSL and Why Does It Matter?</iframe>

## Limitations of HTTPS

However, HTTPS has its limitations. Domain names and IP addresses are not secure when using HTTPS. This is part of the reason why the use of VPNs is advised when using public wireless networks to mask IP addresses.

HTTPS is becoming adopted by more and more websites every day. Modern browsers like Firefox and Chrome warn users if a website has an invalid certificate or if the connection is not secure (if it uses http:// instead of https://). They use a lock icon to the left of each URL to indicate if the site is authenticated and if it uses HTTPS. Latest versions of these browsers even ask twice before navigating to insecure sites. Tools like Firefox's built-in [HTTPS-Only Mode](https://support.mozilla.org/en-US/kb/https-only-prefs) and extensions like [HTTPS Everywhere](https://www.eff.org/https-everywhere) work by rewriting insecure HTTP request to HTTPS. And with services like [Let's Encrypt](https://letsencrypt.org/), enabling HTTPS on sites is becoming more convenient.

## Further Reading

- [Computer Networks: HTTP Basics](https://minch.dev/blog/http)

---

_Originally posted on [OpenGenus IQ](https://iq.opengenus.org/idea-behind-https/)_
