# Remember

## Polyfills

- [Supported Browsers and Features](https://nextjs.org/docs/basic-features/supported-browsers-features#polyfills)

We transparently inject polyfills required for IE11 compatibility. If any of your dependencies includes these polyfills,
they’ll be eliminated automatically from the production build to avoid duplication.

### Server-Side Polyfills

In addition to `fetch()` on the client-side, Next.js polyfills `fetch()` in the Node.js environment. You can use
`fetch()` in your server code (such as getStaticProps/getServerSideProps) without using polyfills such as
isomorphic-unfetch or node-fetch.

## SWC

Next.js now uses Rust-based compiler SWC to compile JavaScript/TypeScript.

When an application has a custom Babel configuration, Next.js will automatically opt-out of using SWC for compiling
JavaScript/Typescript and will fall back to using Babel in the same way that it was used in Next.js 11.
