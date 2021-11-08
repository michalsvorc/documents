# Service Worker API

* [Service Worker API](https://developer.mozilla.org/en-US/docs/Web/API/Service_Worker_API)
* [Using Service Workers](https://developer.mozilla.org/en-US/docs/Web/API/Service_Worker_API/Using_Service_Workers)
* [Cheatsheet](https://developer.mozilla.org/en-US/docs/Web/API/Service_Worker_API/Using_Service_Workers/sw101.png)

Tools:

* [Workbox](https://developers.google.com/web/tools/workbox/)
* [Tools for PWA Developers](https://developers.google.com/web/ilt/pwa/tools-for-pwa-developers)
* [Lighthouse](https://developers.google.com/web/tools/lighthouse)

APIs:

* [ServiceWorkerGlobalScope](https://developer.mozilla.org/en-US/docs/Web/API/ServiceWorkerGlobalScope)
* [ExtendableEvent.waitUntil()](https://developer.mozilla.org/en-US/docs/Web/API/ExtendableEvent/waitUntil)
* [ServiceWorkerGlobalScope.skipWaiting()](https://developer.mozilla.org/en-US/docs/Web/API/ServiceWorkerGlobalScope/skipWaiting)
* [Clients.claim()](https://developer.mozilla.org/en-US/docs/Web/API/Clients/claim)

Examples:

* [Service Worker Cookbook](https://serviceworke.rs/)

## Overview

Service workers essentially act as proxy servers that sit between web applications, the browser, and the network (when
available). 

A service worker is an event-driven worker registered against an origin and a path.

A service worker is run in a worker context: it therefore has no DOM access, and runs on a different thread to the main
JavaScript that powers your app, so it is non-blocking.


Service workers only run over HTTPS, for security reasons.

The service worker becomes idle when not in use and restarts when it's next needed. You cannot rely on a global state
persisting between events. If there is information that you need to persist and reuse across restarts, you can use
*IndexedDB*.

It is designed to be fully async; as a consequence, APIs such as synchronous XHR and Web Storage can't be used inside a
service worker. With Service Workers, we use the Cache API instead.

A single service worker can control many pages. Each time a page within your scope is loaded, the service worker is
installed against that page and operates on it.

The service worker will only catch requests from clients under the service worker's scope. The max scope for a service
worker is the location of the worker.

## Use cases

Service workers are also intended to be used for such things as:

* Background data synchronization.
* Responding to resource requests from other origins.
* Receiving centralized updates to expensive-to-calculate data such as geolocation or gyroscope, so multiple pages can
  make use of one set of data.
* Client-side compiling and dependency management of CoffeeScript, less, CJS/AMD modules, etc. for development purposes.
* Hooks for background services.
* Custom templating based on certain URL patterns.
* Performance enhancements, for example pre-fetching resources that the user is likely to need in the near future, such
  as the next few pictures in a photo album.

## Objects

* [ServiceWorkerContainer](https://developer.mozilla.org/en-US/docs/Web/API/ServiceWorkerContainer)

Provides an object representing the service worker as an overall unit in the network ecosystem, including facilities to
register, unregister and update service workers, and access the state of service workers and their registrations.

* [self](https://developer.mozilla.org/en-US/docs/Web/API/Window/self)

Self refers to a global object. In service worker script, self refers to that SW, otherwise it refers to the Window
object. See also
[globalThis](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/globalThis).

## Lifecycle

* [Basic architecture - MDN](https://developer.mozilla.org/en-US/docs/Web/API/Service_Worker_API/Using_Service_Workers#basic_architecture)
* [Download, install and activate - MDN](https://developer.mozilla.org/en-US/docs/Web/API/Service_Worker_API#download_install_and_activate)
* [Google developers](https://developers.google.com/web/ilt/pwa/introduction-to-service-worker#service_worker_lifecycle) 

### Events

* [Install event](https://developer.mozilla.org/en-US/docs/Web/API/ServiceWorkerGlobalScope/install_event)

An Install event is always the first one sent to a service worker (this can be used to start the process of populating
an IndexedDB, and caching site assets). 


The install events in service workers use `waitUntil()` to hold the service worker in the installing phase until tasks
complete. If the promise passed to `waitUntil()` rejects, the install is considered a failure, and the installing
service worker is discarded. 

* [Activate event](https://developer.mozilla.org/en-US/docs/Web/API/ServiceWorkerGlobalScope/activate_event)

When the service worker is installed, it then receives an activate event.

The point where this event fires is generally a good time to clean up old caches and other things associated with the
previous version of your service worker.

If there is an existing service worker available, the new version is installed in the background, but not yet activated:
at this point it is called the worker in waiting.

It is only activated when there are no longer any pages loaded that are still using the old service worker. As soon as
there are no more pages to be loaded, the new service worker activates (becoming the active worker). Activation can
happen sooner using `ServiceWorkerGlobalScope.skipWaiting()` and existing pages can be claimed by the active worker using
`Clients.claim()`.

The activate events in service workers use `waitUntil()` to buffer functional events such as fetch and push until the
promise passed to `waitUntil()` settles. This gives the service worker time to update database schemas and delete
outdated caches, so other events can rely on a completely upgraded state.

## Fetching

* [FetchEvent](https://developer.mozilla.org/en-US/docs/Web/API/FetchEvent)
* [Fetch API](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API)
* [Request](https://developer.mozilla.org/en-US/docs/Web/API/Request)
* [Response](https://developer.mozilla.org/en-US/docs/Web/API/Response)

A fetch event fires every time any resource controlled by a service worker is fetched, which includes the documents
inside the specified scope, and any resources referenced in those documents.

You can modify the response to these requests in any way you want, using the `FetchEvent.respondWith()` method.

## Precaching

One feature of service workers is the ability to save a set of files to the cache when the service worker is installing.
This is often referred to as "precaching", since you are caching content ahead of the service worker being used.

The main reason for doing this is that it gives developers control over the cache, meaning they can determine when and
how long a file is cached as well as serve it to the browser without going to the network, meaning it can be used to
create web apps that work offline.

There are a number of items that are great candidates for precaching: your web app's start URL, your offline fallback
page, and key JavaScript and CSS files. By precaching files, you’ll guarantee that they’re available in the cache when
the service worker takes control of the page.

## Local development

* [http-server](https://github.com/http-party/http-server#tlsssl)

## Workbox

* [Guides](https://developers.google.com/web/tools/workbox/guides/get-started)
* [Documentation](https://developers.google.com/web/tools/workbox/reference-docs/latest)

* [Offline fallback](https://developers.google.com/web/tools/workbox/guides/get-started#offline_fallback)

This service worker precaches an offline page and, if a user is offline, returns the contents of the precached offline
page instead of producing a browser error.

### Caching strategies

* Stale While Revalidate

This strategy will use a cached response for a request if it is available and update the cache in the background
with a response from the network. (If it’s not cached it will wait for the network response and use that.) This
is a fairly safe strategy as it means users are regularly updating their cache. The downside of this strategy is
that it’s always requesting an asset from the network, using up the user’s bandwidth.

* Network First

This will try to get a response from the network first. If it receives a response, it’ll pass that to the
browser and also save it to a cache. If the network request fails, the last cached response will be used.

* Cache First

This strategy will check the cache for a response first and use that if one is available. If the request isn’t in the
cache, the network will be used and any valid response will be added to the cache before being passed to the browser.

* Network Only

Force the response to come from the network.

* Cache Only

Force the response to come from the cache.

