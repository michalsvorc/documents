# Progressive web app (PWA)

Overview:

* [MDN](https://developer.mozilla.org/en-US/docs/Web/Progressive_web_apps)
* [Google](https://developers.google.com/web/ilt/pwa)
* [web.dev](https://web.dev/progressive-web-apps/)

Tools:

* [Lighthouse](https://developers.google.com/web/tools/lighthouse)
* [Tools for PWA Developers](https://developers.google.com/web/ilt/pwa/tools-for-pwa-developers)
* [Workbox](https://developers.google.com/web/tools/workbox)

Guides:

* [Re-engageable Notifications Push](https://developer.mozilla.org/en-US/docs/Web/Progressive_web_apps/Re-engageable_Notifications_Push)
* [How to make PWAs installable](https://developer.mozilla.org/en-US/docs/Web/Progressive_web_apps/Installable_PWAs)
* [Add to Home screen](https://developer.mozilla.org/en-US/docs/Web/Progressive_web_apps/Add_to_home_screen)

Caching:

* [Offline Service workers - MDN](https://developer.mozilla.org/en-US/docs/Web/Progressive_web_apps/Offline_Service_workers)
* [Caching Files with Service Worker - Google developers](https://developers.google.com/web/ilt/pwa/caching-files-with-service-worker)

There are some key principles a web app should try to observe to be identified as a PWA. It should be:

* **Discoverable**, so the contents can be found through search engines.
* **Installable**, so it can be available on the device's home screen or app launcher.
* **Linkable**, so you can share it by sending a URL.
* **Network independent**, so it works offline or with a poor network connection.
* **Progressively enhanced**, so it's still usable on a basic level on older browsers, but fully-functional on the
  latest ones.
* **Re-engageable**, so it's able to send notifications whenever there's new content available.
* **Responsively designed**, so it's usable on any device with a screen and a browser—mobile phones, tablets, laptops,
  TVs, refrigerators, etc.
* **Secure**, so the connections between the user, the app, and your server are secured against any third parties trying
  to get access to sensitive data.

The key ingredient required for PWAs is service worker support. Thankfully service workers are now supported on all
major browsers on desktop and mobile.

## Progressive enhancement

By using progressive enhancement, PWAs are cross-browser. This means developers should take into account the
differences in implementation of some PWA features and technologies between different browser implementations.

Start with the "good, old basic website” and progressively add new features while remembering to detect if they are
available in the browser and gracefully handle any errors that crop up if support is not available.

For example, an offline mode with the help of service workers is just an extra trait that makes the website experience
better, but it's still perfectly usable without it.

## Discoverability

* [Web app manifests](https://developer.mozilla.org/en-US/docs/Web/Manifest)

Some of the capabilities have already been enabled on certain web-based platforms by proprietary technologies like Open
Graph.

The relevant web standard here is the **Web app** manifest, which defines features of an app such as name, icon, splash
screen, and theme colors in a JSON-formatted manifest file.

## Network independence

* [Service Worker API](https://developer.mozilla.org/en-US/docs/Web/API/Service_Worker_API)
* [Cache](https://developer.mozilla.org/en-US/docs/Web/API/Cache)
* [Web Storage API](https://developer.mozilla.org/en-US/docs/Web/API/Web_Storage_API)
* [IndexedDB API](https://developer.mozilla.org/en-US/docs/Web/API/IndexedDB_API)

* Revisit a site and get its contents even if no network is available.
* Browse any kind of content the user has previously visited at least once, even under situations of poor connectivity.
* Control what is shown to the user in situations where there is no connectivity.

This is achieved using a combination of technologies:

* **Service Workers** to control page requests (for example storing them offline).
* The **Cache API** for storing responses to network requests offline (very useful for storing site assets).
* Client-side data storage technologies such as **Web Storage** and **IndexedDB** to store application data offline.

## Re-engageability

* [Push API](https://developer.mozilla.org/en-US/docs/Web/API/Push_API)
* [Notifications API](https://developer.mozilla.org/en-US/docs/Web/API/Notifications_API)

One major advantage of native platforms is the ease with which users can be re-engaged by updates and new content, even
when they aren't looking at the app or using their devices.

The **Push API** and **Notifications API** are two separate APIs, but they work well together when you want to provide
engaging functionality in your app. Push is used to deliver new content from the server to the app without any
client-side intervention, and its operation is handled by the app's service worker. Notifications can be used by the
service worker to show new information to the user, or at least alert them when something has been updated.

## Responsiveness

* [Media queries](https://developer.mozilla.org/en-US/docs/Web/CSS/Media_Queries)
* [Viewport](https://developer.mozilla.org/en-US/docs/Glossary/Viewport)

Responsive web apps use technologies like **media queries** and **viewport** to make sure that their UIs will fit any
form factor: desktop, mobile, tablet, or whatever comes next.

## Installable

* [Web app manifests](https://developer.mozilla.org/en-US/docs/Web/Manifest)

Add to home screen is a feature implemented by mobile browsers that takes the information found in
an app's web manifest and uses them to represent the app on the device's home screen with an icon and name.

To make the web site installable, it needs the following things in place:

* A web manifest, with the correct fields filled in.
* The web site to be served from a secure (HTTPS) domain.
* An icon to represent the app on the device.
* A service worker registered, to allow the app to work offline (this is required only by Chrome for Android in **2021**).

## Progressive loading

* [Progressive loading](https://developer.mozilla.org/en-US/docs/Web/Progressive_web_apps/Loading)

### Javascript

```html
<script src="app.js" defer></script>
```

When the `defer` attribute is present, then the script is executed when the page has finished parsing (DOMContentLoaded
event), so it won't block rendering the HTML structure.

### CSS

We can split css files and add `media` types to them:

```html
<link rel="stylesheet" href="print.css" media="print">
```

This will tell the browser to load them only when the condition is met.

See [media queries](https://developer.mozilla.org/en-US/docs/Web/CSS/Media_Queries/Using_media_queries).

### Images

* [Loading via JavaScript](https://developer.mozilla.org/en-US/docs/Web/Progressive_web_apps/Loading#loading_via_javascript)
* [Loading on demand](https://developer.mozilla.org/en-US/docs/Web/Progressive_web_apps/Loading#loading_on_demand)
* [Intersection Observer API](https://developer.mozilla.org/en-US/docs/Web/API/Intersection_Observer_API)
```html
<img src='data/img/placeholder.png' data-src='data/img/SLUG.jpg' alt='NAME'>
```

The app uses a placeholder image instead, which is small and lightweight, while the final paths to target images are
stored in `data-src` attributes. Those images will be loaded via JavaScript after the site finishes building the HTML
structure. The problem is that it still loads all the images at once.

We can ensure that images will be loaded only when they appear in the viewport with Intersection Observer API.
Intersection Observer will load target images only when the user scrolls down, causing them to display in the viewport.

You could try to make your apps more bulletproof by making them work without JavaScript - either using `<noscript>` to
show the image with final src already assigned, or by wrapping `<img>` tags with `<a>` elements pointing at the target
images, so the user can click and access them when desired.

## Web app manifest

* [MDN](https://developer.mozilla.org/en-US/docs/Web/Manifest)
* [W3C manifest specification](https://w3c.github.io/manifest/)
* [Canise](https://caniuse.com/#feat=web-app-manifest)

The web app manifest provides information about a web application in a JSON text file, necessary for the web app to be
downloaded and be presented to the user similarly to a native app.

Web app manifests are deployed in your HTML pages using a `<link>` element in the `<head>` of a document:

```html
<link rel="manifest" href="<name>.webmanifest">
```

### File extension

A few common kinds of manifest file have been used in the past: `manifest.webapp` was popular in Firefox OS app manifests,
and many use `manifest.json` for web manifests as the contents are organized in a JSON structure. However, the
`.webmanifest` file format is explicitly mentioned in the W3C manifest specification.

The `.webmanifest` extension is specified in the Media type registration section of the specification, but generally
browsers will support manifests with other appropriate extensions, e.g. `.json`.

### Members

* [MDN](https://developer.mozilla.org/en-US/docs/Web/Manifest#members)

A minimal web manifest must have at least a `name` and an `icons` field with at least one icon defined; that icon must
have at least the `src`, `sizes`, and `type` sub-fields as well.

Beyond that, everything is optional, though the `description`, `short_name`, and `start_url` fields are recommended.

## Other APIs used in PWAs

* [Fetch API](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API)

Intercept network requests and then modify the response with content other than the requested resource

* [Push API](https://developer.mozilla.org/en-US/docs/Web/API/Push_API)

An API that enables your app to subscribe to a push service and receive push messages. Push messages are delivered to a
service worker, which can use the information in the message to update the local state or display a notification to the
user. Because service workers run independently of the main app, they can receive and display notifications even when
the browser is not running.

* [Background Sync API](https://developer.mozilla.org/en-US/docs/Web/API/Web_Periodic_Background_Synchronization_API)

Lets you defer actions until the user has stable connectivity. This is useful to ensure that whatever the user wants to
send is actually sent. This API also allows servers to push periodic updates to the app so the app can update when it's
next online

* [Channel Messaging API](https://developer.mozilla.org/en-US/docs/Web/API/Channel_Messaging_API)

Lets web workers and service workers communicate with each other and with the host application. Examples of this API
include new content notification and updates that require user interaction.
