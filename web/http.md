# HTTP

- [MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP)

Overview:

- [Methods - MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods)
- [Status codes - MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status)
- [Headers - MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers)
- [Messages - MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/Messages)
- [Common MIME types - MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/Basics_of_HTTP/MIME_types/Common_types)

Topics:

- [Persistent connections - MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/Connection_management_in_HTTP_1.x#persistent_connections)

HTTP is:

- An application layer protocol that is sent over TCP, or over a TLS-encrypted TCP connection.
- A client-server protocol: requests are sent by one entity, the user-agent (or a proxy on behalf of it).
- Stateless: there is no link between two requests being successively carried out on the same connection. But
  while the core of HTTP itself is stateless, HTTP cookies allow the use of stateful sessions.

Here is a list of common features controllable with HTTP:

- Caching
- Relaxing the origin constraint
- Authentication
- Proxy and tunneling
- Sessions

## HTTP/2

- [MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/Basics_of_HTTP/Evolution_of_HTTP#http2_%E2%80%93_a_protocol_for_greater_performance)

HTTP/2 introduces an extra step: it divides HTTP/1.x messages into frames which are embedded in a stream. Data and
header frames are separated, this allows header compression.

HTTP/2 is multiplexing messages over a single connection, helping keep the connection warm and more efficient.

The HTTP/2 protocol has several prime differences from the HTTP/1.1 version:

- It is a binary protocol rather than text. It can no longer be read and created manually. Despite this hurdle, improved
  optimization techniques can now be implemented.
- It is a multiplexed protocol. Parallel requests can be handled over the same connection, removing the order and
  blocking constraints of the HTTP/1.x protocol.
- It compresses headers. As these are often similar among a set of requests, this removes duplication and overhead of
  data transmitted.
- It allows a server to populate data in a client cache, in advance of it being required, through a mechanism called the
  server push.

## Proxies

Proxies may perform numerous functions:

- caching (the cache can be public or private, like the browser cache)
- filtering (like an antivirus scan or parental controls)
- load balancing (to allow multiple servers to serve the different requests)
- authentication
- logging

## Sessions

In client-server protocols, like HTTP, sessions consist of three phases:

1. The client establishes a TCP connection (or the appropriate connection if the transport layer is not TCP).
2. The client sends its request, and waits for the answer.
3. The server processes the request, sending back its answer, providing a status code and appropriate data.

As of HTTP/1.1, the connection is no longer closed after completing the third phase, and the client is now granted a
further request: this means the second and third phases can now be performed any number of times.

## Security

- [Mozilla web security guidelines - MDN](https://infosec.mozilla.org/guidelines/web_security)
- [XSS - MDN](https://developer.mozilla.org/en-US/docs/Glossary/Cross-site_scripting)

### Content Security Policy (CSP)

- [MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/CSP)
- [Content-Security-Policy HTTP header - MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Security-Policy)

Content Security Policy (CSP) is an added layer of security that helps to detect and mitigate certain types of attacks,
including Cross-Site Scripting (XSS) and data injection attacks. CSP makes it possible for server administrators to
reduce or eliminate the vectors by which XSS can occur by specifying the domains that the browser should consider to be
valid sources of executable scripts.

`Content-Security-Policy: default-src 'self'`

### Strict-Transport-Security (HSTS)

- [MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Strict-Transport-Security)

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

- [MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/X-Content-Type-Options)

The X-Content-Type-Options response HTTP header is a marker used by the server to indicate that the MIME types
advertised in the Content-Type headers should not be changed and be followed. This is a way to opt out of MIME type
sniffing, or, in other words, to say that the MIME types are deliberately configured.

`X-Content-Type-Options: nosniff`

### X-Frame-Options

- [MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/X-Frame-Options)

The X-Frame-Options HTTP response header can be used to indicate whether or not a browser should be allowed to render a
page in a `<frame>`, `<iframe>`, `<embed>` or `<object>`. Sites can use this to avoid click-jacking attacks, by ensuring
that their content is not embedded into other sites.

### X-XSS-Protection

- [MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/X-XSS-Protection)

The HTTP X-XSS-Protection response header is a feature of Internet Explorer, Chrome and Safari that stops pages from
loading when they detect reflected cross-site scripting (XSS) attacks.

Although these protections are largely unnecessary in modern browsers when sites implement a strong
Content-Security-Policy that disables the use of inline JavaScript ('unsafe-inline'), they can still provide protections
for users of older web browsers that don't yet support CSP.

### Secure cookies

- [MDN](https://infosec.mozilla.org/guidelines/web_security#cookies)

All cookies should be created such that their access is as limited as possible. This can help minimize damage from
cross-site scripting (XSS) vulnerabilities, as these cookies often contain session identifiers or other sensitive
information.

All cookies must be set with the Secure flag, and set as restrictively as possible.

## Cross-Origin Resource Sharing (CORS)

- [MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS)

Cross-Origin Resource Sharing (CORS) is an HTTP-header based mechanism that allows a server to indicate any origins
(domain, scheme, or port) other than its own from which a browser should permit loading of resources.

In that preflight, the browser sends headers that indicate the HTTP method and headers that will be used in the actual
request.

For security reasons, browsers restrict cross-origin HTTP requests initiated from scripts. For example, XMLHttpRequest
and the Fetch API follow the same-origin policy.

This means that a web application using those APIs can only request resources from the same origin the application was
loaded from unless the response from other origins includes the right CORS headers.

The only headers which are allowed to be manually set are those which the Fetch spec defines as a CORS-safelisted
request-header, which are:

- Accept
- Accept-Language
- Content-Language
- Content-Type (but note the additional requirements below)
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

- [MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS#requests_with_credentials)

For a CORS request with credentials, in order for browsers to expose the response to frontend JavaScript code, both the
server (using the `Access-Control-Allow-Credentials` header) and the client (by setting the _credentials mode_ for the
XHR, Fetch, or Ajax request) must indicate that they’re opting in to including credentials.

## Cookies

- [MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/Cookies)
- [Wikipedia](https://en.wikipedia.org/wiki/HTTP_cookie)
- [Cookie header - MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Cookie)

An HTTP cookie (web cookie, browser cookie) is a small piece of data that a server sends to the user's web browser.

It remembers stateful information for the stateless HTTP protocol.

Cookies are mainly used for three purposes:

- Session management: Logins, shopping carts, game scores, or anything else the server should remember.
- Personalization: User preferences, themes, and other settings.
- Tracking: Recording and analyzing user behavior.

Cookies are sent with every request, so they can worsen performance (especially for mobile data connections). An
expiration date or duration can be specified, after which the cookie is no longer sent.

Server response:
`Set-Cookie: yummy_cookie=choco`

Each subsequent client request:
`Cookie: yummy_cookie=choco`

### Lifetime

_Session cookies_ are deleted when the current session ends. The browser defines when the "current session" ends, and
some browsers use session restoring when restarting, which can cause session cookies to last indefinitely long.

_Permanent cookies_ are deleted at a date specified by the Expires attribute, or after a period of time specified by the
Max-Age attribute. When an Expires date and time are set, they are relative to the client the cookie is being set on,
not the server.

### Restricted access

- [MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/Cookies#restrict_access_to_cookies)

Restricted access attributes:

- A cookie with the `Secure` attribute is sent to the server only with an encrypted request over the
  HTTPS protocol, never with unsecured HTTP (except on localhost), and therefore can't easily be accessed by a
  man-in-the-middle attacker.
- A cookie with the `HttpOnly` attribute is inaccessible to the JavaScript Document.cookie API; it is
  sent only to the server. For example, cookies that persist server-side sessions don't need to be available to
  JavaScript, and should have the HttpOnly attribute. This precaution helps mitigate cross-site scripting (XSS) attacks.

### Scope

The `Domain` and `Path` attributes define the scope of the cookie: what URLs the cookies should be sent to.

The `SameSite` attribute lets servers specify whether/when cookies are sent with cross-site requests (where Site is
defined by the registrable domain), which provides some protection against cross-site request forgery attacks (CSRF).
It takes three possible values: `Strict`, `Lax`, and `None`.

### Security

- [Security](https://developer.mozilla.org/en-US/docs/Web/HTTP/Cookies#security)
- [Cookie prefixes - MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/Cookies#restrict_access_to_cookies#cookie_prefixes)

Cookies available to JavaScript can be stolen through XSS. Information should be stored in cookies with the
understanding that all cookie values are visible to, and can be changed by, the end-user.

### Third-party cookies

- [MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/Cookies#third-party_cookies)

A cookie is associated with a domain. If this domain is the same as the domain of the page you are on, the cookie is
called a _first-party cookie_.

If the domain is different, it is a third-party cookie. While the server hosting a web page sets first-party cookies,
the page may contain images or other components stored on servers in other domains (for example, ad banners), which may
set third-party cookies.

These are mainly used for advertising and tracking across the web.

## Authentication

- [MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/Authentication)
- [WWW-Authenticate header - MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/WWW-Authenticate)
- [Authorization header - MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Authorization)

Common authentication schemes include:

- Basic
- Bearer
- Digest
- HOBA
- Mutual
- AWS4-HMAC-SHA256

The "Basic" HTTP authentication scheme is defined in RFC 7617, which transmits credentials as user ID/password pairs,
encoded using base64.

### The challenge and response flow

1. The server responds to a client with a `401` (Unauthorized) response status and provides information on how to
   authorize with a `WWW-Authenticate` _response header_ containing at least one challenge.
2. A client that wants to authenticate itself with the server can then do so by including an `Authorization` _request
   header_ with the credentials.
3. Usually a client will present a password prompt to the user and will then issue the request including the correct
   `Authorization` header.

In the case of a "Basic" authentication, the exchange must happen over an HTTPS (TLS) connection to be secure.

The same challenge and response mechanism can be used for proxy authentication with `407` (Proxy Authentication
Required), the `Proxy-Authenticate` _response header_ and the `Proxy-Authorization` _request header_.

The `WWW-Authenticate` and `Proxy-Authenticate` response headers define the authentication method that should be used to
gain access to a resource. They must specify which authentication scheme is used, so that the client that wishes to
authorize knows how to provide the credentials.

The `Authorization` and `Proxy-Authorization` request headers contain the credentials to authenticate a user agent with
a (proxy) server.

## Caching

- [MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/Caching)
- [Revving - MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/Caching#revved_resources)

A _shared cache_ is a cache that stores responses for reuse by more than one user.

A _private cache_ is dedicated to a single user.

### Cache-Control header

- [MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Cache-Control)

The `Cache-Control` header field is used to specify directives for caching mechanisms in both requests and responses.

`no-cache`: A cache will send the request to the origin server for validation before releasing a cached copy. This
directive is not effective in preventing caches from storing your response. If you mean to not store the response in any
cache, use no-store instead.

`no-store`: The response may not be stored in any cache. Note that this will not prevent a valid pre-existing cached
response being returned. Clients can set `max-age=0` to also clear existing cache responses, as this forces the cache to
revalidate with the server (no other directives have an effect when used with no-store).

`max-age=<seconds>`: The maximum amount of time in which a resource will be considered fresh. This directive is relative
to the time of the request, and overrides the Expires header (if set).

`must-revalidate`: The cache must verify the status of the stale resources before using it and expired ones should not
be used.

`Pragma` header should only be used for backwards compatibility with HTTP/1.0 caches where the `Cache-Control` HTTP/1.1
header is not yet present.

### Freshness

- [Cache diagram - MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/Caching/http_staleness.png)
- [Heuristic freshness checking - MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/Caching#heuristic_freshness_checking)

Caches have finite storage so items are periodically removed from storage. This process is called _cache eviction_.

Note that a stale resource is not evicted or ignored; when the cache receives a request for a stale resource, it
forwards this request with a `If-None-Match` to check if it is in fact still fresh. If so, the server returns a `304`
(Not Modified) header without sending the body of the requested resource, saving some bandwidth.

If a `Cache-Control: max-age=N` header is specified, then the freshness lifetime is equal to N. If an origin server does
not explicitly specify freshness (e.g. using `Cache-Control` or `Expires` header) then a heuristic approach may be used.

### Validation

When a cached document's expiration time has been reached, it is either validated or fetched again. Validation can only
occur if the server provided either a strong validator or a weak validator.

Revalidation is triggered when the user presses the reload button. It is also triggered under normal browsing if the
cached response includes the "Cache-Control: must-revalidate" header.

The `ETag` response header is an opaque-to-the-useragent value that can be used as a strong validator.

The `Last-Modified` response header can be used as a weak validator.

Validators are cached with the resource (like all headers) and will be used to craft conditional requests, once the
cache becomes stale.

See conditional requests.

### Varying responses

- [MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/Caching#varying_responses)
- [Vary header - MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Vary)
- [Normalization - MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/Caching#normalization)

The Vary HTTP response header determines how to match future request headers to decide whether a cached response can be
used rather than requesting a fresh one from the origin server. It is used by the server to indicate which headers it
used when selecting a representation of a resource in a content negotiation algorithm.

The Vary header should be set on a `304 Not Modified` response exactly like it would have been set on an equivalent `200 OK` response.

The Vary header can be useful for serving different content to desktop and mobile users, or to allow search engines to
discover the mobile version of a page (and perhaps also tell them that no Cloaking is intended). This is usually
achieved with the `Vary: User-Agent` header.

To avoid unnecessary requests and duplicated cache entries, caching servers should use `normalization` to pre-process
the request and cache only files that are needed. For example, in the case of Accept-Encoding you could check for gzip
and other compression types in the header before doing further processing, and otherwise unset the header.

## Conditional requests

- [MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/Conditional_requests)

HTTP has a concept of conditional requests, where the result, and even the success of a request, can be changed by
comparing the affected resources with the value of a _validator_.

All conditional headers try to check if the resource stored on the server matches a specific version. To achieve this,
the conditional requests need to indicate the version of the resource.

Such values describing the version are called validators, and are of two kinds:

- The date of last modification of the document, the last-modified date.
- An opaque string, uniquely identifying each version, called the entity tag, or the etag.

Comparing versions of the same resource is a bit tricky: depending on the context, there are two kinds of equality
checks:

- Strong validation is used when byte to byte identity is expected, for example when resuming a download.
- Weak validation is used when the user-agent only needs to determine if the two resources have the same content. This
  is even if they are minor differences; like different ads, or a footer with a different date.

### Conditional headers

- [If-Match](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/If-Match)
- [If-None-Match](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/If-None-Match)
- [If-Modified-Since](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/If-Modified-Since)
- [If-Unmodified-Since](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/If-Unmodified-Since)
- [If-Range](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/If-Range)

### Optimistic locking

Conditional requests allow implementing the optimistic locking algorithm (used by most wikis or source control systems).
The concept is to allow all clients to get copies of the resource, then let them modify it locally, controlling
concurrency by successfully allowing the first client to submit an update. All subsequent updates, based on the now
obsolete version of the resource, are rejected

## Compression

- [MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/Compression)

All modern browsers and servers do support compression and the only thing to negotiate is the compression algorithm to
use. Nowadays, only two are relevant: `gzip`, and `br`.

- _End-to-end_ compression refers to a compression of the body of a message that is done by the server and will last
  unchanged until it reaches the client. Whatever the intermediate nodes are, they leave the body untouched.
- _Hop-by-hop_ compression doesn't happen on the resource in the server, creating a specific representation that is then
  transmitted, but on the body of the message between any two nodes on the path between the client and the server.

## Redirection

- [MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/Redirections)

In HTTP, redirection is triggered by a server sending a special redirect response to a request. Redirect responses have
status codes that start with 3, and a `Location` header holding the URL to redirect to.

Alternative way of specifying redirections:

- HTML redirections with the `<meta>` element
- JavaScript redirections via the DOM

## Partial requests

- [MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/Range_requests)
- [Range header - MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Range)

If the `Accept-Ranges` is present in HTTP responses (and its value isn't "none"), the server supports range requests.

If the server supports range requests, you can issue such a request by using the `Range` header.

The `Transfer-Encoding` header allows chunked encoding, which is useful when larger amounts of data are sent to the
client and the total size of the response is not known until the request has been fully processed. The server sends data
to the client straight away without buffering the response or determining the exact length, which leads to improved
latency. Range requests and chunking are compatible and can be used with or without each other.

## Content negotiation

- [MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/Content_negotiation)

In HTTP, content negotiation is the mechanism that is used for serving different representations of a resource at the
same URI, so that the user agent can specify which is best suited for the user (for example, which language of a
document, which image format, or which content encoding).

HTML5 provides alternatives to content negotiation via, for example, the `<source>` element.

### Server-driven negotiation

The HTTP/1.1 standard defines list of the standard headers that start server-driven negotiation (such as `Accept`,
`Accept-Encoding`, and `Accept-Language`). Server-driven negotiation suffers from a few downsides: it doesn't scale
well. There is one header per feature used in the negotiation.

### Agent-driven negotiation

When facing an ambiguous request, the server sends back a page containing links to the available alternative resources.
The user is presented the resources and choose the one to use. This method is almost always used in conjunction with
scripting, especially with JavaScript redirection: after having checked for the negotiation criteria, the script
performs the redirection.
