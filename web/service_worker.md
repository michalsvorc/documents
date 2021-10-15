# Service Worker API

Overview:

* [Service Worker API](https://developer.mozilla.org/en-US/docs/Web/API/Service_Worker_API)
* [Using Service Workers](https://developer.mozilla.org/en-US/docs/Web/API/Service_Worker_API/Using_Service_Workers)

Tools:

* [Workbox](https://developers.google.com/web/tools/workbox/)
* [Tools for PWA Developers](https://developers.google.com/web/ilt/pwa/tools-for-pwa-developers)
* [Lighthouse](https://developers.google.com/web/tools/lighthouse)

Examples:

* [Service Worker Cookbook](https://serviceworke.rs/)

Service workers essentially act as proxy servers that sit between web applications, the browser, and the network (when
available). They are intended, among other things, to enable the creation of effective offline experiences, intercept
network requests and take appropriate action based on whether the network is available, and update assets residing on
the server. They will also allow access to push notifications and background sync APIs.

A service worker is an event-driven worker registered against an origin and a path.

A service worker is run in a worker context: it therefore has no DOM access, and runs on a different thread to the main
JavaScript that powers your app, so it is non-blocking. It is designed to be fully async; as a consequence, APIs such as
synchronous XHR and Web Storage can't be used inside a service worker.

## Use cases

Service workers are also intended to be used for such things as:

* Background data synchronization.
* Responding to resource requests from other origins.
* Receiving centralized updates to expensive-to-calculate data such as geolocation or gyroscope, so multiple pages can make use of one set of data.
* Client-side compiling and dependency management of CoffeeScript, less, CJS/AMD modules, etc. for development purposes.
* Hooks for background services.
* Custom templating based on certain URL patterns.
* Performance enhancements, for example pre-fetching resources that the user is likely to need in the near future, such as the next few pictures in a photo album.

## HTTPS

Service workers only run over HTTPS, for security reasons.

Note: On Firefox, for testing you can run service workers over HTTP (insecurely); simply check the "Enable Service
Workers over HTTP (when toolbox is open)" option in the Firefox Devtools options.

## IndexedDB

The service worker becomes idle when not in use and restarts when it's next needed. You cannot rely on a global state
persisting between events. If there is information that you need to persist and reuse across restarts, you can use
*IndexedDB*.

## Cache

Saving to web storage won't work, because web storage is synchronous. With Service Workers, we use the Cache API instead.

## Lifecycle

* [Google developers](https://developers.google.com/web/ilt/pwa/introduction-to-service-worker#service_worker_lifecycle) 

If the service worker API is supported in the browser, it is registered against the site using the
`ServiceWorkerContainer.register()` method. When registration is complete, the Service worker JavaScript file is
automatically downloaded, then installed, and finally activated.

### Registration

* [ServiceWorkerContainer.register()](https://developer.mozilla.org/en-US/docs/Web/API/ServiceWorkerContainer/register)

A service worker is first registered using the `ServiceWorkerContainer.register()` method. 

If successful, your service worker will be downloaded to the client and attempt installation/activation (see below) for
URLs accessed by the user inside the whole origin, or inside a subset specified by you.

If successful, a service worker registration ties the provided script URL to a scope, which is subsequently used for
navigation matching. Since a service worker can't have a scope broader than its own location, only use the scope option
when you need a scope that is narrower than the default.

### Download, install and activate

* [MDN](https://developer.mozilla.org/en-US/docs/Web/API/Service_Worker_API#download_install_and_activate)
* [ExtendableEvent.waitUntil()](https://developer.mozilla.org/en-US/docs/Web/API/ExtendableEvent/waitUntil)

At this point, your service worker will observe the following lifecycle:

1. Download
2. Install
3. Activate

The service worker is immediately downloaded when a user first accesses a service worker–controlled site/page.

Because install/activate events could take a while to complete, the service worker spec provides a `waitUntil()` method.
Once it is called on install or activate events with a promise, functional events such as fetch and push will wait until
the promise is successfully resolved.

### Updating

If there is an existing service worker available, the new version is installed in the background, but not yet activated
— at this point it is called the worker in waiting. It is only activated when there are no longer any pages loaded that
are still using the old service worker. As soon as there are no more pages to be loaded, the new service worker
activates (becoming the active worker).

## self

Self refers to a global object. In service worker script, self refers to that SW, otherwise it refers to the Window
object.

## Events

### Install event

* [MDN](https://developer.mozilla.org/en-US/docs/Web/API/ServiceWorkerGlobalScope/install_event)

A standard action is to prepare your service worker for usage when this fires, for example by creating a cache using the
built in storage API, and placing assets inside it that you'll want for running your app offline.

### Activate event

* [MDN](https://developer.mozilla.org/en-US/docs/Web/API/ServiceWorkerGlobalScope/activate_event)

The point where this event fires is generally a good time to clean up old caches and other things associated with the
previous version of your service worker.

### Fetch event

* [MDN](https://developer.mozilla.org/en-US/docs/Web/API/FetchEvent)
* [FetchEvent.respondWith()](https://developer.mozilla.org/en-US/docs/Web/API/FetchEvent/respondWith)

You can modify the response to these requests in any way you want, using the `FetchEvent.respondWith()` method.

## Responding to fetches

We also have a `fetch` event at our disposal, which fires every time an HTTP request is fired off from our app. It
allows us to intercept requests and respond to them with custom responses.

