# Security

- [OWASP Top 10](https://owasp.org/Top10/)
- [MDN - Types of attacks](https://developer.mozilla.org/en-US/docs/Web/Security/Types_of_attacks)

## Same-origin policy

- [MDN](https://developer.mozilla.org/en-US/docs/Web/Security/Same-origin_policy)
- [Wikipedia](https://en.wikipedia.org/wiki/Same-origin_policy)

Under the policy, a web browser permits scripts contained in a first web page to access data in a second web page, but
only if both web pages have the same origin.

An origin is defined as a combination of URI scheme, host name, and port number.

This policy prevents a malicious script on one page from obtaining access to sensitive data on another web page through
that page's Document Object Model.

## Cross-Origin Resource Sharing (CORS)

- [MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS)
- [(Video) Animated Explained](https://youtu.be/Qf2V6v1pdRY)

For security reasons, browsers restrict cross-origin HTTP requests initiated from scripts.

The CORS mechanism supports secure cross-origin requests and data transfers between browsers and servers.

The CORS standard works by adding new HTTP headers that let servers describe which origins are permitted to read that
information from a web browser.

CORS also relies on a mechanism by which browsers make a "preflight" request to the server hosting the cross-origin
resource. The browser first sends an HTTP request using the `OPTIONS` method to the resource on the other origin, in
order to determine if the actual request is safe to send.

The request header of note is `Origin`, which shows that the invocation is coming from https://foo.example.

`Origin: https://foo.example`

If the resource owners at https://bar.other wished to restrict access to the resource to requests only from
https://foo.example, they would send response header:

`Access-Control-Allow-Origin: https://foo.example`

## Cross-site scripting (XSS)

- [MDN](https://developer.mozilla.org/en-US/docs/Web/Security/Types_of_attacks#cross-site_scripting_xss)
- [Wikipedia](https://en.wikipedia.org/wiki/Cross-site_scripting)

Cross-site scripting (XSS) is a security exploit which allows an attacker to inject into a website malicious client-side
code.

A cross-site scripting vulnerability may be used by attackers to bypass access controls such as the same-origin policy.

## Cross-site request forgery (CSRF / XSRF)

- [MDN](https://developer.mozilla.org/en-US/docs/Web/Security/Types_of_attacks#cross-site_request_forgery_csrf)
- [Wikipedia](https://en.wikipedia.org/wiki/Cross-site_request_forgery)
- [(Video) Cross-Site Request Forgery (CSRF) Explained](https://youtu.be/eWEgUcHPle0)

The attacker causes the user's browser to perform a request to the website's backend without the user's consent or
knowledge. An attacker can use an XSS payload to launch a CSRF attack.

Specially-crafted image tags, hidden forms, and JavaScript XMLHttpRequests, for example, can all work without the
user's interaction or even knowledge.

Unlike cross-site scripting (XSS), which exploits the trust a user has for a particular site, CSRF exploits the trust
that a site has in a user's browser.

## Content-Security-Policy (CSP)

- [MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Security-Policy)
- [Wikipedia](https://en.wikipedia.org/wiki/Content_Security_Policy)
