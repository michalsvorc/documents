# TinyURL (URL shortener)

- [educative.io](https://www.educative.io/blog/system-design-tinyurl-instagram)
- [(Video) How to implement TinyURL - youtu.be](https://youtu.be/eCLqmPBIEYs)

## Functional requirements

- Our service will generate a shorter alias of the original URL that can easily be copied and pasted.
- The short link should redirect users to the original link.
- Users should have the option to pick a custom short link for their URL.
- Short links will expire after a default timespan, which users can specify.

## Non-functional requirements

- The system must be highly available.
- URL redirection should happen in real-time with minimal latency.
- Shortened links should not be predictable.

## Capacity estimation

Our system will be read-heavy. There will be a large number of redirection requests compared to new URL shortenings.

## Short url generation

We can compute unique hash from long url via SHA256.

Base64url (URL- and filename-safe standard) with `-` and `_` characters can be used to encode the hash.

As we're picking starting N characters from encoded hash, we can have duplicates. This can be solved with using a
sequence number or user_id number.
