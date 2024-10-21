#cs161 

Cookies encode state data that are stored within your browser and persist across multiple requests and responses. The browser automatically attaches the relevant cookies to send to a web server upon request.

### background
HTTP is a *stateless* protocol. This means that each request-response pair is independent of all others. Some [[world wide web|web]] features require persisting states (e.g. staying logged into a website across multiple visits, preference settings, etc.), and these require browsers and servers to store **HTTP cookies**. 

### structure
The base of a cookie is its name-value pair, which stores what the cookie is actually used for (e.g. `name: theme`, `value: dark`). Additionally, the cookie stores additional attributes which dictate its policies:
- **Domain & path**: define which requests the browser should attach the cookie for
- **Secure**: if `Secure == True`, then the cookie may only be attached to requests using the HTTPS secure protocol
- **HTTPOnly**: if this attribute is set to `True`, then JavaScript in the browser may not access the cookie
- **Expires**: dictates when the cookie will no longer be valid and deleted by the browser

---
## session authentication

One common usage of cookies is for **session authentication**, which is used to associate requests with authenticated users. By storing this information, it saves the end user from having to authenticate themselves before every request.

#### session tokens
The idea behind cookies as session tokens is as follows:
- The user authenticates themselves (for example, by logging in with correct username and password)
- The server generates a *session token* value securely and randomly
- The server sends back the session token, which it will now associate with the user
- When the user makes future requests, the browser attaches the session token cookie with the request
- When the user logs out or the session expires, the token is deleted.

#### cross-site request forgery
CSRF is an attack that exploits cookie-based authentication to perform an action as the victim. These attacks work by tricking an authenticated user into making a malicious request. This can happen in a few ways:
- **Trick the victim into clicking a malicious link**. The link would be to the domain that the user has access to, but that the attacker cannot because they are not authenticated.



