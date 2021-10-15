# Web APIs

* [Specifications - MDN](https://developer.mozilla.org/en-US/docs/Web/API#specifications)

## Cache API

* [API](https://developer.mozilla.org/en-US/docs/Web/API/Cache)
* [Cache Storage](https://developer.mozilla.org/en-US/docs/Web/API/CacheStorage)

The Cache interface provides a persistent storage mechanism for Request / Response object pairs that are cached in long
lived memory. The Cache interface is exposed to windowed scopes as well as workers.

An origin can have multiple, named Cache objects. Items in a Cache do not get updated unless explicitly requested; they
don’t expire unless deleted.

You can access CacheStorage through the global `caches` property.

## Fetch API

* [API](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API)
* [Using Fetch](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API/Using_Fetch)

The Fetch API provides a JavaScript interface for accessing and manipulating parts of the HTTP pipeline, such as
requests and responses. It also provides a global `fetch()` method that provides an easy, logical way to fetch resources
asynchronously across the network.

Fetch provides a generic definition of `Request` and `Response` objects (and other things involved with network
requests). This will allow them to be used wherever they are needed in the future, whether it’s for service workers,
Cache API, and other similar things that handle or modify requests and responses

The `body` read-only property of the `Response` interface is a `ReadableStream` of the body contents.

## IndexedDB API

* [API](https://developer.mozilla.org/en-US/docs/Web/API/IndexedDB_API)
* [Using IndexedDB](https://developer.mozilla.org/en-US/docs/Web/API/IndexedDB_API/Using_IndexedDB)

Libraries:

* [jakearchibald/idb: IndexedDB, but with promises](https://github.com/jakearchibald/idb)

IndexedDB is a low-level API for client-side storage of significant amounts of structured data, including files/blobs.
This API uses indexes to enable high-performance searches of this data.

IndexedDB is a transactional database system, like an SQL-based RDBMS. However, unlike SQL-based RDBMSes, which use
fixed-column tables, IndexedDB is a JavaScript-based object-oriented database. IndexedDB lets you store and retrieve
objects that are indexed with a key.

You need to specify the database schema, open a connection to your database, and then retrieve and update data within a
series of transactions.

Operations performed using IndexedDB are done asynchronously.

## Intersection Observer API

* [API](https://developer.mozilla.org/en-US/docs/Web/API/Intersection_Observer_API)
* [Viewport](https://developer.mozilla.org/en-US/docs/Glossary/Viewport)

The Intersection Observer API provides a way to asynchronously observe changes in the intersection of a target element
with an ancestor element or with a top-level document's `viewport`.

Intersection information is needed for many reasons, such as:

* Lazy-loading of images or other content as a page is scrolled.
* Implementing "infinite scrolling" web sites, where more and more content is loaded and rendered as you scroll, so that
  the user doesn't have to flip through pages.
* Reporting of visibility of advertisements in order to calculate ad revenues.
* Deciding whether or not to perform tasks or animation processes based on whether or not the user will see the result.

## Push API

* [API](https://developer.mozilla.org/en-US/docs/Web/API/Push_API)
* [Service Worker Recipes](https://serviceworke.rs/web-push.html)
* [Data Encryption Test Page](https://jrconlin.github.io/WebPushDataTestPage/)
* [Sending VAPID identified WebPush Notifications](https://blog.mozilla.org/services/2016/08/23/sending-vapid-identified-webpush-notifications-via-mozillas-push-service/)

The Push API gives web applications the ability to receive messages pushed to them from a server, whether or not the web
app is in the foreground, or even currently loaded, on a user agent. This lets developers deliver asynchronous
notifications and updates to users that opt in, resulting in better engagement with timely new content.

## Streams API

* [API](https://developer.mozilla.org/en-US/docs/Web/API/Streams_API)
* [Concepts](https://developer.mozilla.org/en-US/docs/Web/API/Streams_API/Concepts)
* [Using readable streams](https://developer.mozilla.org/en-US/docs/Web/API/Streams_API/Using_readable_streams)
* [Using writable streams](https://developer.mozilla.org/en-US/docs/Web/API/Streams_API/Using_writable_streams)

The Streams API allows JavaScript to programmatically access streams of data received over the network and process them
as desired by the developer. This feature is available in Web Workers.

You can detect when streams start or end, chain streams together, handle errors and cancel streams as required, and
react to the speed the stream is being read at.

There are two types of underlying source:

* Push sources constantly push data at you when you’ve accessed them, and it is up to you to start, pause, or cancel
  access to the stream. Examples include video streams and TCP/Web sockets.
* Pull sources require you to explicitly request data from them once connected to. Examples include a file access
  operation via a Fetch or XHR call.

## Web Workers API

* [API](https://developer.mozilla.org/en-US/docs/Web/API/Web_Workers_API)

Web Workers makes it possible to run a script operation in a background thread separate from the main execution thread
of a web application. The advantage of this is that laborious processing can be performed in a separate thread, allowing
the main (usually the UI) thread to run without being blocked/slowed down.

