# Nest remeber

For quickly creating a CRUD controller with the validation built-in, you may use the CLI's CRUD generator:
`nest g resource [name]`. 

Prefer applying filters by using classes instead of instances when possible. It reduces memory usage since Nest can
easily reuse instances of the same class across your entire module. 

In the case of hybrid apps the `useGlobalPipes()` method doesn't set up pipes for gateways and micro services. For
"standard" (non-hybrid) microservice apps, `useGlobalPipes()` does mount pipes globally.

Pipes, guards, interceptors and exception filters can be controller-scoped, method-scoped, or global-scoped.

To access the route's custom metadata set with the `@SetMetadata()` decorator, we'll use the `Reflector#get` method.
It's not good practice to use `@SetMetadata()` directly in your routes. Instead, create your own decorators.

## Webpack

Hot reload with [webpack](https://docs.nestjs.com/recipes/hot-reload)

Bundling external dependencies in production build is [not recommended](https://github.com/ZenSoftware/bundled-nest).

## HTTP libraries

- [Fastify vs. Express](https://docs.nestjs.com/controllers#library-specific-approach)
- Since Fastify lacks support for nested routers, when using sub-domain routing, the (default) Express adapter should be
  used instead.
- The Fastify package uses the latest version of the path-to-regexp package, which no longer supports wildcard asterisks
  `*`. Instead, you must use parameters (e.g., `(.*)`, `:splat*`). 
- Multer middleware package for file uploading is not compatible with Fastify.

