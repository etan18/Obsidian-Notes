---

---
#cs161
## urls
URL stands for **uniform resource locator**, and it is essentially the address that identifies the location of everything on the internet. That is, all webpages, PDFs, and even images on the internet have a corresponding URL.

There are three mandatory parts to a URL:
```
http://www.berkeleyproject.org/index.html
```
1. ***Protocol***: the protocol tells the browser *how* to retreive the resource in question. Most commonly, we see HTTP and HTTPS.
>[!tip] Hypertext Transfer Protocol (HTTP)
>HTTP is the protocol that powers the World Wide Web. It follows a request-response model, where clients (i.e. browsers) send a request that the server can respond to. HTTPS is a secure version of HTTP.

1. ***Location***: the location contains the name of the web server to retreive the resource from, usually a web domain. In this example, that is  `www.berkeleyproject.org` .
2. ***Path***: the path tells the browser *which* resource located on the web server to request. In this example, that is the specific `index.html` webpage.

Optionally, there are a few additional features we see in URLs:
- *Usernames* and *ports* can be specified as part of the location.
- *Arguments* are added after the path and denoted by a `?`. Each of the specified parameters is separated by an `&` and provides information for the web server to use when fetching.
- *Anchors* are denoted using `#` and is used by the webpage after its already been fecthed and run by the browser. Anchors are often used to scroll to a particular section of the webpage.
 
---
## webpages
Modern webpages are primarily designed in three main languages: HTML, CSS, and Javascript. Generally,
- **Hypertext Markup Language (HTML)** generates the foundation of a webpage with basic, structured documents
- **Cascading Style Sheets (CSS)** allows us to alter the appearance of HTML components
- **JavaScript** is the programming language that runs in the browser. It allows for dynamic features and interactive components within a webpage.
When a browser receives an HTML document, it first converts the HTML into an internal form called the DOM (Document Object Model). The JavaScript is then applied on the DOM to modify how the page is displayed to the user. The browser then renders the DOM to display the result to the user.

The origin of a webpage is defined by its protocol, domain name, and port. Two webpages have the same origin if all three of those values match.

>[!warning] Same-Origin Policy
>Modern web browsers isolate each open webpage, meaning they cannot communicate with or access any information within each other. The only exception is if multiple webpages share the same origin. This is to prevent security risks from visiting malicious websites.

### cookies
HTTP is a *stateless* protocol. This means that each request-response pair is independent of all others. Some web features require persisting states (e.g. staying logged into a website across multiple visits, preference settings, etc.), and these require browsers and servers to store **HTTP cookies**. 

Cookies encode state data that are stored within your browser and persist across multiple requests and responses. The browser automatically attaches the relevant cookies to send to a web server upon request.