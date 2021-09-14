# Next.js

* [Docs | Next.js](https://nextjs.org/docs/)

Libraries:

* [Basic Features: ESLint](https://nextjs.org/docs/basic-features/eslint)

## Pages

* [nextjs.org Basic Features: Pages](https://nextjs.org/docs/basic-features/pages)

`/pages/*.{js, .jsx, .ts, .tsx}`

Each page is associated with a route based on its file name. By default, Next.js pre-renders every page. 

Each generated HTML is associated with minimal JavaScript code necessary for that page. When a page is loaded by the
browser, its JavaScript code runs and makes the page fully interactive. (This process is called *hydration*.)

## Static Generation

* [getStaticProps](https://nextjs.org/docs/basic-features/data-fetching#getstaticprops-static-generation): Fetch data at build time.
* [getStaticPaths](https://nextjs.org/docs/basic-features/data-fetching#getstaticpaths-static-generation): Specify dynamic routes to pre-render pages based on data.

The HTML is generated at build time and will be reused on each request. To make a page use Static Generation, either
export the page component, or export getStaticProps (and getStaticPaths if necessary). It's great for pages that can be
pre-rendered ahead of a user's request. You can also use it with Client-side Rendering to bring in additional data.

For more info, see data fetching documentation.

## Server-side Rendering (getServerSideProps)

* [getServerSideProps](https://nextjs.org/docs/basic-features/data-fetching#getserversideprops-server-side-rendering): Fetch data on each request.

The HTML is generated on *each request*. To make a page use Server-side Rendering, export `getServerSideProps`. Because
Server-side Rendering results in slower performance than Static Generation, use this only if absolutely necessary.

## Static File Serving

* [Basic Features: Static File Serving](https://nextjs.org/docs/basic-features/static-file-serving)

Next.js can serve static files, like images, under a folder called `public` in the root directory. Files inside public
can then be referenced by your code starting from the base URL (/). Only assets that are in the public directory at
build time will be served by Next.js. Files added at runtime won't be available. 

## Environment Variables

* [Basic Features: Environment Variables](https://nextjs.org/docs/basic-features/environment-variables)

Next.js has built-in support for loading environment variables from `.env.local` into process.env.

By default all environment variables loaded through .env.local are only available in the Node.js environment, meaning
they won't be exposed to the browser.

In order to expose a variable to the browser you have to prefix the variable with NEXT_PUBLIC_.

Environment variables must be referenced as e.g. process.env.NEXT_PUBLIC_PUBLISHABLE_KEY, not with object destructuring.

## Image Optimization

* [Basic Features: Image Optimization](https://nextjs.org/docs/basic-features/image-optimization)

Since version *10.0.0*, Next.js has a built-in Image Component and Automatic Image Optimization. The Next.js Image
Component,[ next/image](https://nextjs.org/docs/api-reference/next/image), is an extension of the HTML &lt;img> element,
evolved for the modern web.

## Font Optimization

* [Basic Features: Font Optimization](https://nextjs.org/docs/basic-features/font-optimization)

Since version *10.2*, Next.js has built-in web font optimization. To add a web font to your Next.js application,
override next/head.

## Script Component

* [Basic Features: Script Optimization](https://nextjs.org/docs/basic-features/script)

The Next.js Script component enables developers to set the loading priority of third-party scripts to save developer
time and improve loading performance.

## [Routing](https://nextjs.org/docs/routing/introduction)

* [next/link](https://nextjs.org/docs/api-reference/next/link): Handle client-side navigations.
* [next/router](https://nextjs.org/docs/api-reference/next/router): Leverage the router API in your pages.

[next/link](https://nextjs.org/docs/api-reference/next/link) should be able to cover most of your routing needs, but you
can also do client-side navigations without it, take a look at the [documentation for
next/router](https://nextjs.org/docs/api-reference/next/router).

### [Routing: Shallow Routing](https://nextjs.org/docs/routing/shallow-routing)

Shallow routing allows you to change the URL without running data fetching methods again, that includes
[getServerSideProps](https://nextjs.org/docs/basic-features/data-fetching#getserversideprops-server-side-rendering),
[getStaticProps](https://nextjs.org/docs/basic-features/data-fetching#getstaticprops-static-generation), and
[getInitialProps](https://nextjs.org/docs/api-reference/data-fetching/getInitialProps). Shallow routing only works for
same page URL changes.

## Data fetching

* [Basic Features: Data Fetching](https://nextjs.org/docs/basic-features/data-fetching)

Look at Incremental Static Regeneration instead of pure SSR. (?)

## [Pre-rendering](https://nextjs.org/docs/basic-features/pages#pre-rendering)

By default, Next.js pre-renders every page.

* [Static Generation](https://nextjs.org/docs/basic-features/pages#static-generation-recommended): The HTML is generated at build time and will be reused on each request.
* [Server-side Rendering](https://nextjs.org/docs/basic-features/pages#server-side-rendering): The HTML is generated on each request.

Or you can skip pre-rendering and use client-side JavaScript to populate data.

In development mode, every page is pre-rendered on each request - **even for pages that use Static Generation**.

## [getStaticProps (Static Generation)](https://nextjs.org/docs/basic-features/data-fetching#getstaticprops-static-generation)

```jsx
export async function getStaticProps(context) {
  return {
    props: {}, // will be passed to the page component as props
    // optional:
    revalidate, 
    notFound,
    redirect,
  }
}
```

Technical details:

* [Only runs at build time](https://nextjs.org/docs/basic-features/data-fetching#only-runs-at-build-time): it does not receive data that’s only available during request time.
* [Write server-side code directly](https://nextjs.org/docs/basic-features/data-fetching#write-server-side-code-directly): getStaticProps runs only on the server-side. It won’t even be included in the JS bundle for the browser.
* [Statically Generates both HTML and JSON](https://nextjs.org/docs/basic-features/data-fetching#statically-generates-both-html-and-json): Next.js generates a JSON file holding the result of running getStaticProps.
* [Only allowed in a page](https://nextjs.org/docs/basic-features/data-fetching#only-allowed-in-a-page)
* [Runs on every request in development](https://nextjs.org/docs/basic-features/data-fetching#runs-on-every-request-in-development)
* [Preview Mode](https://nextjs.org/docs/basic-features/data-fetching#preview-mode)

Note: notFound is not needed for[ fallback: false](https://nextjs.org/docs/basic-features/data-fetching#fallback-false)
mode as only paths returned from getStaticPaths will be pre-rendered.

When you use getStaticProps on a page with dynamic route parameters, you must use getStaticPaths.

### Reading files

* [Basic Features: Data Fetching](https://nextjs.org/docs/basic-features/data-fetching#reading-files-use-processcwd)

Files can be read directly from the filesystem in getStaticProps.

## [getStaticPaths (Static Generation)](https://nextjs.org/docs/basic-features/data-fetching#getstaticpaths-static-generation)

If you export an async function called `getStaticPaths` from a page that uses dynamic routes, Next.js will statically
pre-render all the paths specified by getStaticPaths.

```jsx
export async function getStaticPaths() {
  return {
    paths: [
      { params: { ... } }
    ],
    fallback: true | false // required
  };
}
```

### The fallback key (required)

* [Basic Features: Data Fetching](https://nextjs.org/docs/basic-features/data-fetching#the-fallback-key-required)

If fallback is *false*, then any paths not returned by getStaticPaths will result in a 404 page error.

If fallback is *true*, Next.js will serve a *fallback version of the page* on the first request to such a path.
See [ Fallback pages](https://nextjs.org/docs/basic-features/data-fetching#fallback-pages) for details.

If fallback is *blocking*, new paths not returned by getStaticPaths will wait for the HTML to be generated, identical to
SSR (hence why blocking), and then be cached for future requests so it only happens once per path.

## [getServerSideProps (Server-side Rendering)](https://nextjs.org/docs/basic-features/data-fetching#getserversideprops-server-side-rendering)

If you export an async function called getServerSideProps from a page, Next.js will pre-render this page on each request
using the data returned by getServerSideProps.

```jsx
export async function getServerSideProps(context) {
const data = ...
 if (!data) {
    return {
      notFound | redirect,
    }
  }
  return {
    props: {},
  }
}
```

Note: You can import modules in top-level scope for use in getServerSideProps. Imports used in getServerSideProps will
not be bundled for the client-side.

This means you can write server-side code directly in getServerSideProps. This includes reading from the filesystem or a
database.

Technical details:

* [Only runs on server-side](https://nextjs.org/docs/basic-features/data-fetching#only-runs-on-server-side)
* [Only allowed in a page](https://nextjs.org/docs/basic-features/data-fetching#only-allowed-in-a-page-2)

## [Fetching data on the client side (SWR, Client-side data fetching)](https://nextjs.org/docs/basic-features/data-fetching#fetching-data-on-the-client-side)

The team behind Next.js has created a React hook for data fetching called [SWR](https://swr.now.sh/). 

1. First, immediately show the page without data. Parts of the page can be pre-rendered using Static Generation. You can
   show loading states for missing data.
2. Then, fetch the data on the client side and display it when ready.

## Incremental Static Regeneration (ISR)

* [Basic Features: Data Fetching](https://nextjs.org/docs/basic-features/data-fetching#incremental-static-regeneration)
* [Incremental Static Regeneration - Vercel Documentation](https://vercel.com/docs/next.js/incremental-static-regeneration)

Next.js allows you to create or update static pages *after* you’ve built your site. Incremental Static Regeneration
(ISR) enables you to use static-generation on a per-page basis, *without needing to rebuild the entire site*. 

Example: `revalidate: 10`

When a request is made to a page that was pre-rendered at build time, it will initially show the cached page.

* Any requests to the page after the initial request and before 10 seconds are also cached and instantaneous.
* After the 10-second window, the next request will still show the cached (stale) page
* Next.js triggers a regeneration of the page in the background.
* Once the page has been successfully generated, Next.js will invalidate the cache and show the updated product page. If
  the background regeneration fails, the old page will stay unaltered.
