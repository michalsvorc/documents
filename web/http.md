# HTTP

* [MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP)

Topics:

* [HTTP Messages - MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/Messages)
* [Common MIME types - MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/Basics_of_HTTP/MIME_types/Common_types)
* [Persistent connections - MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/Connection_management_in_HTTP_1.x#persistent_connections)

HTTP is:

* An application layer protocol that is sent over TCP, or over a TLS-encrypted TCP connection.
* A client-server protocol: requests are sent by one entity, the user-agent (or a proxy on behalf of it). 
* Stateless: there is no link between two requests being successively carried out on the same connection. But
while the core of HTTP itself is stateless, HTTP cookies allow the use of stateful sessions.

Here is a list of common features controllable with HTTP:

* Caching
* Relaxing the origin constraint
* Authentication
* Proxy and tunneling
* Sessions

## HTTP/2

* [MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/Basics_of_HTTP/Evolution_of_HTTP#http2_%E2%80%93_a_protocol_for_greater_performance)

HTTP/2 introduces an extra step: it divides HTTP/1.x messages into frames which are embedded in a stream. Data and
header frames are separated, this allows header compression. 

HTTP/2 is multiplexing messages over a single connection, helping keep the connection warm and more efficient.

The HTTP/2 protocol has several prime differences from the HTTP/1.1 version:

* It is a binary protocol rather than text. It can no longer be read and created manually. Despite this hurdle, improved
  optimization techniques can now be implemented.
* It is a multiplexed protocol. Parallel requests can be handled over the same connection, removing the order and
  blocking constraints of the HTTP/1.x protocol.
* It compresses headers. As these are often similar among a set of requests, this removes duplication and overhead of
  data transmitted.
* It allows a server to populate data in a client cache, in advance of it being required, through a mechanism called the
  server push.

## Proxies

Proxies may perform numerous functions:

* caching (the cache can be public or private, like the browser cache)
* filtering (like an antivirus scan or parental controls)
* load balancing (to allow multiple servers to serve the different requests)
* authentication
* logging

## Sessions

In client-server protocols, like HTTP, sessions consist of three phases:

1. The client establishes a TCP connection (or the appropriate connection if the transport layer is not TCP).
2. The client sends its request, and waits for the answer.
3. The server processes the request, sending back its answer, providing a status code and appropriate data.

As of HTTP/1.1, the connection is no longer closed after completing the third phase, and the client is now granted a
further request: this means the second and third phases can now be performed any number of times.

## Security

* [Mozilla web security guidelines - MDN](https://infosec.mozilla.org/guidelines/web_security)
* [XSS - MDN](https://developer.mozilla.org/en-US/docs/Glossary/Cross-site_scripting)

### Content Security Policy (CSP)

* [MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/CSP)
* [Content-Security-Policy HTTP header - MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Security-Policy)

Content Security Policy (CSP) is an added layer of security that helps to detect and mitigate certain types of attacks,
including Cross-Site Scripting (XSS) and data injection attacks. CSP makes it possible for server administrators to
reduce or eliminate the vectors by which XSS can occur by specifying the domains that the browser should consider to be
valid sources of executable scripts.

`Content-Security-Policy: default-src 'self'`

### Strict-Transport-Security (HSTS)

* [MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Strict-Transport-Security)

If a website accepts a connection through HTTP and redirects to HTTPS, visitors may initially communicate with the
non-encrypted version of the site before being redirected. This creates an opportunity for a man-in-the-middle attack.
The redirect could be exploited to direct visitors to a malicious site instead of the secure version of the original
site.

The HTTP Strict Transport Security header informs the browser that it should never load a site using HTTP and should
automatically convert all attempts to access the site using HTTP to HTTPS requests instead.

Note: The Strict-Transport-Security header is ignored by the browser when your site is accessed using HTTP; this is
because an attacker may intercept HTTP connections and inject the header or remove it. When your site is accessed over
HTTPS with no certificate errors, the browser knows your site is HTTPS capable and will honor the
Strict-Transport-Security header.

Example: As long as you've accessed your bank's web site once using HTTPS, and the bank's web site uses Strict Transport
Security, your browser will know to automatically use only HTTPS.

`Strict-Transport-Security: max-age=<expire-time>`

The time, in seconds, that the browser should remember that a site is only to be accessed using HTTPS.

### X-Content-Type-Options

* [MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/X-Content-Type-Options)

The X-Content-Type-Options response HTTP header is a marker used by the server to indicate that the MIME types
advertised in the Content-Type headers should not be changed and be followed. This is a way to opt out of MIME type
sniffing, or, in other words, to say that the MIME types are deliberately configured. 

`X-Content-Type-Options: nosniff`

### X-Frame-Options

* [MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/X-Frame-Options)

The X-Frame-Options HTTP response header can be used to indicate whether or not a browser should be allowed to render a
page in a `<frame>`, `<iframe>`, `<embed>` or `<object>`. Sites can use this to avoid click-jacking attacks, by ensuring that
their content is not embedded into other sites.

### X-XSS-Protection

* [MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/X-XSS-Protection)

The HTTP X-XSS-Protection response header is a feature of Internet Explorer, Chrome and Safari that stops pages from
loading when they detect reflected cross-site scripting (XSS) attacks.

Although these protections are largely unnecessary in modern browsers when sites implement a strong
Content-Security-Policy that disables the use of inline JavaScript ('unsafe-inline'), they can still provide protections
for users of older web browsers that don't yet support CSP.

### Secure cookies

* [MDN](https://infosec.mozilla.org/guidelines/web_security#cookies)

All cookies should be created such that their access is as limited as possible. This can help minimize damage from
cross-site scripting (XSS) vulnerabilities, as these cookies often contain session identifiers or other sensitive
information.

All cookies must be set with the Secure flag, and set as restrictively as possible.

## Cross-Origin Resource Sharing (CORS)

* [MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS)

Cross-Origin Resource Sharing (CORS) is an HTTP-header based mechanism that allows a server to indicate any origins
(domain, scheme, or port) other than its own from which a browser should permit loading of resources. 

In that preflight, the browser sends headers that indicate the HTTP method and headers that will be used in the actual
request.

For security reasons, browsers restrict cross-origin HTTP requests initiated from scripts. For example, XMLHttpRequest
and the Fetch API follow the same-origin policy.

This means that a web application using those APIs can only request resources from the same origin the application was
loaded from unless the response from other origins includes the right CORS headers.

The only headers which are allowed to be manually set are those which the Fetch spec defines as a CORS-safelisted request-header, which are:

* Accept
* Accept-Language
* Content-Language
* Content-Type (but note the additional requirements below)
  - application/x-www-form-urlencoded
  - multipart/form-data
  - text/plain

`Access-Control-Allow-Origin: <origin> | *`

Access-Control-Allow-Origin specifies either a single origin, which tells browsers to allow that origin to access the
resource; or else — for requests without credentials — the `*` wildcard, to tell browsers to allow any origin to access
the resource.

```
Access-Control-Allow-Origin: https://mozilla.org
Vary: Origin
```

If the server specifies a single origin (that may dynamically change based on the requesting origin as part of a
allowlist), then the server should also include `Origin` in the `Vary` response header - to indicate to clients that
server responses will differ based on the value of the `Origin` request header.

### Requests with credentials

* [MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS#requests_with_credentials)

For a CORS request with credentials, in order for browsers to expose the response to frontend JavaScript code, both the
server (using the `Access-Control-Allow-Credentials` header) and the client (by setting the *credentials mode* for the
XHR, Fetch, or Ajax request) must indicate that they’re opting in to including credentials. 

## Cookies

* [MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/Cookies)
* [Wikipedia](https://en.wikipedia.org/wiki/HTTP_cookie)
* [Cookie header - MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Cookie)

An HTTP cookie (web cookie, browser cookie) is a small piece of data that a server sends to the user's web browser. 

It remembers stateful information for the stateless HTTP protocol. 

Cookies are mainly used for three purposes:

* Session management: Logins, shopping carts, game scores, or anything else the server should remember.
* Personalization: User preferences, themes, and other settings.
* Tracking: Recording and analyzing user behavior.

Cookies are sent with every request, so they can worsen performance (especially for mobile data connections). An
expiration date or duration can be specified, after which the cookie is no longer sent.

Server response:
`Set-Cookie: yummy_cookie=choco`

Each subsequent client request:
`Cookie: yummy_cookie=choco`

### Lifetime

*Session cookies* are deleted when the current session ends. The browser defines when the "current session" ends, and
some browsers use session restoring when restarting, which can cause session cookies to last indefinitely long.

*Permanent cookies* are deleted at a date specified by the Expires attribute, or after a period of time specified by the
Max-Age attribute. When an Expires date and time are set, they are relative to the client the cookie is being set on,
not the server.

### Restricted access

* [MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/Cookies#restrict_access_to_cookies)

Restricted access attributes:

* A cookie with the `Secure` attribute is sent to the server only with an encrypted request over the
  HTTPS protocol, never with unsecured HTTP (except on localhost), and therefore can't easily be accessed by a
  man-in-the-middle attacker. 
* A cookie with the `HttpOnly` attribute is inaccessible to the JavaScript Document.cookie API; it is
  sent only to the server. For example, cookies that persist server-side sessions don't need to be available to
  JavaScript, and should have the HttpOnly attribute. This precaution helps mitigate cross-site scripting (XSS) attacks.

### Scope

The `Domain` and `Path` attributes define the scope of the cookie: what URLs the cookies should be sent to.

The `SameSite` attribute lets servers specify whether/when cookies are sent with cross-site requests (where Site is
defined by the registrable domain), which provides some protection against cross-site request forgery attacks (CSRF).
It takes three possible values: `Strict`, `Lax`, and `None`.

### Security

* [Security](https://developer.mozilla.org/en-US/docs/Web/HTTP/Cookies#security)
* [Cookie prefixes - MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/Cookies#restrict_access_to_cookies#cookie_prefixes)

Cookies available to JavaScript can be stolen through XSS.  Information should be stored in cookies with the
understanding that all cookie values are visible to, and can be changed by, the end-user.

### Third-party cookies

* [MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/Cookies#third-party_cookies)

A cookie is associated with a domain. If this domain is the same as the domain of the page you are on, the cookie is
called a *first-party cookie*.

If the domain is different, it is a third-party cookie. While the server hosting a web page sets first-party cookies,
the page may contain images or other components stored on servers in other domains (for example, ad banners), which may
set third-party cookies.

These are mainly used for advertising and tracking across the web.

