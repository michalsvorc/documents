# Next.js

- [Docs | Next.js](https://nextjs.org/docs/)

Topics:

- [TypeScript support](https://nextjs.org/docs/basic-features/typescript)
- [API Routes](https://nextjs.org/docs/api-routes/introduction)
- [Production: caching, logging, error handling](https://nextjs.org/docs/going-to-production)
- [Authentication](https://nextjs.org/docs/authentication)
- [Testing](https://nextjs.org/docs/testing)
- [Upgrading, new features](https://nextjs.org/docs/upgrading)

API:

- [next.config.js](https://nextjs.org/docs/api-reference/next.config.js/introduction)

## Pages

- [nextjs.org Basic Features: Pages](https://nextjs.org/docs/basic-features/pages)

`/pages/*.{js, .jsx, .ts, .tsx}`

Each page is associated with a route based on its file name.

By default, Next.js pre-renders every page. This means that Next.js generates HTML for each page in advance, instead of
having it all done by client-side JavaScript.

Each generated HTML is associated with minimal JavaScript code necessary for that page. When a page is loaded by the
browser, its JavaScript code runs and makes the page fully interactive. (This process is called _hydration_.)

Next.js has two forms of pre-rendering:

- Static Generation
- Server-side Rendering

The difference is in _when_ it generates the HTML for a page.

## Data fetching

- [Basic Features: Data Fetching](https://nextjs.org/docs/basic-features/data-fetching)

### Static Generation

- [getStaticProps](https://nextjs.org/docs/basic-features/data-fetching#getstaticprops-static-generation): Fetch data at build time.
- [getStaticPaths](https://nextjs.org/docs/basic-features/data-fetching#getstaticpaths-static-generation): Specify dynamic routes to pre-render pages based on data.

The HTML is generated at build time and will be reused on each request. It's great for pages that can be pre-rendered
ahead of a user's request. You can also use it with Client-side Rendering to bring in additional data.

Files can be [read directly](<(https://nextjs.org/docs/basic-features/data-fetching#reading-files-use-processcwd)>) from the filesystem in `getStaticProps`.

### Server-side Rendering (getServerSideProps)

- [getServerSideProps](https://nextjs.org/docs/basic-features/data-fetching#getserversideprops-server-side-rendering): Fetch data on each request.

The HTML is generated on each request. To make a page use Server-side Rendering, export `getServerSideProps`.

### Client-side data fetching

- [Fetching data on the client side (SWR, Client-side data fetching)](https://nextjs.org/docs/basic-features/data-fetching#fetching-data-on-the-client-side)

If your page contains frequently updating data, and you don’t need to pre-render the data, you can fetch the data on the
client side. An example of this is user-specific data.

1. First, immediately show the page without data. Parts of the page can be pre-rendered using Static Generation. You can
   show loading states for missing data.
2. Then, fetch the data on the client side and display it when ready.

The team behind Next.js has created a React hook for data fetching called [SWR](https://swr.now.sh/).

### Incremental Static Regeneration (ISR)

- [ISR](https://nextjs.org/docs/basic-features/data-fetching#incremental-static-regeneration)

Next.js allows you to create or update static pages _after_ you’ve built your site. Incremental Static Regeneration
(ISR) enables you to use static-generation on a per-page basis, without needing to rebuild the entire site.

Example: `revalidate: 10`

When a request is made to a page that was pre-rendered at build time, it will initially show the cached page.

- Any requests to the page after the initial request and before 10 seconds are also cached and instantaneous.
- After the 10-second window, the next request will still show the cached (stale) page
- Next.js triggers a regeneration of the page in the background.
- Once the page has been successfully generated, Next.js will invalidate the cache and show the updated product page. If
  the background regeneration fails, the old page will stay unaltered.

## Layouts

- [Docs](https://nextjs.org/docs/basic-features/layouts)
- [With TypeScript](https://nextjs.org/docs/basic-features/layouts#with-typescript)

Inside your layout, you can fetch data on the client-side using `useEffect` or a library like `SWR`.

When navigating between pages, we want to persist page state (input values, scroll position, etc) for a Single-Page
Application (SPA) experience.

## Static File Serving

- [Basic Features: Static File Serving](https://nextjs.org/docs/basic-features/static-file-serving)

Next.js can serve static files, like images, under a folder called `public` in the root directory. Files inside public
can then be referenced by your code starting from the base URL (/). Only assets that are in the public directory at
build time will be served by Next.js. Files added at runtime won't be available.

## Environment Variables

- [Basic Features: Environment Variables](https://nextjs.org/docs/basic-features/environment-variables)

Next.js has built-in support for loading environment variables from `.env.local` into process.env.

In order to expose a variable to the browser you have to prefix the variable with `NEXT_PUBLIC_`.

!Note:

Environment variables must be directly referenced as `process.env.NEXT_PUBLIC_PUBLISHABLE_KEY`, not declared through
object destructuring.

## Optimization

- [Image Optimization](https://nextjs.org/docs/basic-features/image-optimization)
- [Font Optimization](https://nextjs.org/docs/basic-features/font-optimization)
- [Script Optimization](https://nextjs.org/docs/basic-features/script)

## Routing

- [Documentation](https://nextjs.org/docs/routing/introduction)

- [next/link](https://nextjs.org/docs/api-reference/next/link): Handle client-side navigations.

The Next.js router allows you to do client-side route transitions between pages, similar to a single-page application.
A React component called `Link` is provided to do this client-side route transition.

- [next/router](https://nextjs.org/docs/api-reference/next/router): Leverage the router API in your pages.

To access the router object in a React component you can use `useRouter` or `withRouter`.

- [Shallow Routing](https://nextjs.org/docs/routing/shallow-routing)

Shallow routing allows you to change the URL without running data fetching methods again.

You'll receive the updated pathname and the query via the router object (added by `useRouter` or `withRouter`), without
losing state.

## Middleware

- [Documentation](https://nextjs.org/docs/middleware)

You can run code before a request is completed. Based on the user's incoming request, you can modify the response by
rewriting, redirecting, adding headers, or even streaming HTML.

Middleware can be used for anything that shares logic for a set of pages, including:

- Authentication
- Bot protection
- Redirects and rewrites
- Handling unsupported browsers
- Feature flags and A/B tests
- Server-side analytics
- Advanced i18n routing requirements
- Logging
