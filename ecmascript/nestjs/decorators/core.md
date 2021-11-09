# Nest.js core decorators

## [@Catch()](https://github.com/nestjs/nest/blob/master/packages/common/decorators/core/catch.decorator.ts)

Decorator that marks a class as a Nest exception filter. An exception filter handles exceptions thrown by or not handled
by your application code.

The decorated class must implement the `ExceptionFilter` interface.

@param exceptions one or more exception *types* specifying the exceptions to be caught and handled by this filter.

@see [Exception Filters](https://docs.nestjs.com/exception-filters)

```typescript
export function Catch(...exceptions: Type<any>[]): ClassDecorator
```

## [@Controller()](https://github.com/nestjs/nest/blob/master/packages/common/decorators/core/controller.decorator.ts)

Decorator that marks a class as a Nest controller that can receive inbound requests and produce responses.

An HTTP Controller responds to inbound HTTP Requests and produces HTTP Responses. It defines a class that provides the
context for one or more related route handlers that correspond to HTTP request methods and associated routes for example
`GET /api/profile`, `POST /users/resume`

A Microservice Controller responds to requests as well as events, running over a variety of transports [(read more
here)](https://docs.nestjs.com/microservices/basics). It defines a class that provides a context for one or more message
or event handlers.

@param prefixOrOptions a `route path prefix` or a `ControllerOptions` object.
A `route path prefix` is pre-pended to the path specified in any request decorator
in the class. `ControllerOptions` is an options configuration object specifying:
- `scope` - symbol that determines the lifetime of a Controller instance.
[See Scope](https://docs.nestjs.com/fundamentals/injection-scopes#usage) for
more details.
- `prefix` - string that defines a `route path prefix`.  The prefix
is pre-pended to the path specified in any request decorator in the class.
- `version` - string, array of strings, or Symbol that defines the version
of all routes in the class. [See Versioning](https://docs.nestjs.com/techniques/versioning)
for more details.

@see [Routing](https://docs.nestjs.com/controllers#routing)
@see [Controllers](https://docs.nestjs.com/controllers)
@see [Microservices](https://docs.nestjs.com/microservices/basics#request-response)
@see [Scope](https://docs.nestjs.com/fundamentals/injection-scopes#usage)
@see [Versioning](https://docs.nestjs.com/techniques/versioning)

```typescript
export function Controller(
prefixOrOptions?: string | string[] | ControllerOptions,
): ClassDecorator
```

## [@Inject()](https://github.com/nestjs/nest/blob/master/packages/common/decorators/core/inject.decorator.ts)

Decorator that marks a constructor parameter as a target for [Dependency Injection
(DI)](https://docs.nestjs.com/providers#dependency-injection).

Any injected provider must be visible within the module scope (loosely speaking, the containing module) of the class it
is being injected into. This can be done by:

- defining the provider in the same module scope
- exporting the provider from one module scope and importing that module into the
  module scope of the class being injected into
- exporting the provider from a module that is marked as global using the
  `@Global()` decorator

### Injection tokens

Can be *types* (class names), *strings* or *symbols*. This depends on how the provider with which it is associated was
defined. Providers defined with the `@Injectable()` decorator use the class name. Custom Providers may use strings or
symbols as the injection token.

@param token lookup key for the provider to be injected (assigned to the constructor
parameter).

@see [Providers](https://docs.nestjs.com/providers)
@see [Custom Providers](https://docs.nestjs.com/fundamentals/custom-providers)
@see [Injection Scopes](https://docs.nestjs.com/fundamentals/injection-scopes)

```typescript
export function Inject<T = any>(token?: T | undefined)
: (target: object, key: string | symbol, index?: number | undefined) => void
```

## [@Injectable()](https://github.com/nestjs/nest/blob/master/packages/common/decorators/core/injectable.decorator.ts)

Decorator that marks a class as a [provider](https://docs.nestjs.com/providers). Providers can be injected into other
classes via constructor parameter injection using Nest's built-in [Dependency Injection
(DI)](https://docs.nestjs.com/providers#dependency-injection) system.

When injecting a provider, it must be visible within the module scope (loosely speaking, the containing module) of the
class it is being injected into. This can be done by:

- defining the provider in the same module scope
- exporting the provider from one module scope and importing that module into the module scope of the class being
  injected into
- exporting the provider from a module that is marked as global using the `@Global()` decorator

Providers can also be defined in a more explicit and imperative form using various [custom
provider](https://docs.nestjs.com/fundamentals/custom-providers) techniques that expose more capabilities of the DI
system.

@param options options specifying scope of injectable

@see [Providers](https://docs.nestjs.com/providers)
@see [Custom Providers](https://docs.nestjs.com/fundamentals/custom-providers)
@see [Injection Scopes](https://docs.nestjs.com/fundamentals/injection-scopes)

```typescript
export function Injectable(options?: InjectableOptions): ClassDecorator
```

## [@Optional()](https://github.com/nestjs/nest/blob/master/packages/common/decorators/core/optional.decorator.ts)

Parameter decorator for an injected dependency marking the dependency as optional.

For example:
```typescript
constructor(@Optional() @Inject('HTTP_OPTIONS')private readonly httpClient: T) {}
```

@see [Optional providers](https://docs.nestjs.com/providers#optional-providers)

```typescript
function Optional(): (target: object, key: string | symbol, index?: number | undefined) => void
```

## [@SetMetadata()](https://github.com/nestjs/nest/blob/master/packages/common/decorators/core/set-metadata.decorator.ts)

Decorator that assigns metadata to the class/function using the specified `key`.

Requires two parameters:
- `key` - a value defining the key under which the metadata is stored
- `value` - metadata to be associated with `key`

This metadata can be reflected using the `Reflector` class.

Example: `@SetMetadata('roles', ['admin'])`

@see [Reflection](https://docs.nestjs.com/guards#reflection)

```typescript
const SetMetadata = <K = string, V = any>(
metadataKey: K,
metadataValue: V,
): CustomDecorator<K>
```

## [@UseFilters()](https://github.com/nestjs/nest/blob/master/packages/common/decorators/core/exception-filters.decorator.ts)

Decorator that binds exception filters to the scope of the controller or method, depending on its context.

When `@UseFilters` is used at the controller level, the filter will be applied to every handler (method) in the
controller.

When `@UseFilters` is used at the individual handler level, the filter will apply only to that specific method.

@param filters exception filter instance or class, or a list of exception filter instances or classes.

@see [Exception filters](https://docs.nestjs.com/exception-filters)

@usageNotes
Exception filters can also be set up globally for all controllers and routes using `app.useGlobalFilters()`.
[See here for details](https://docs.nestjs.com/exception-filters#binding-filters)

```typescript
export const UseFilters = (...filters: (ExceptionFilter | Function)[]) => MethodDecorator & ClassDecorator
```

## [@UseGuards()](https://github.com/nestjs/nest/blob/master/packages/common/decorators/core/use-guards.decorator.ts)

Decorator that binds guards to the scope of the controller or method, depending on its context.

When `@UseGuards` is used at the controller level, the guard will be applied to every handler (method) in the
controller.

When `@UseGuards` is used at the individual handler level, the guard will apply only to that specific method.

@param guards a single guard instance or class, or a list of guard instances or classes.

@see [Guards](https://docs.nestjs.com/guards)

```typescript
function UseGuards(
...guards: (CanActivate | Function)[]
): MethodDecorator & ClassDecorator
```

## [@UseInterceptors()](https://github.com/nestjs/nest/blob/master/packages/common/decorators/core/use-interceptors.decorator.ts)

Decorator that binds interceptors to the scope of the controller or method, depending on its context.

When `@UseInterceptors` is used at the controller level, the interceptor will be applied to every handler (method) in
the controller.

When `@UseInterceptors` is used at the individual handler level, the interceptor will apply only to that specific
method.

@param interceptors a single interceptor instance or class, or a list of interceptor instances or classes.

@see [Interceptors](https://docs.nestjs.com/interceptors)

```typescript
function UseInterceptors(
...interceptors: (NestInterceptor | Function)[]
): MethodDecorator & ClassDecorator
```

## [@UsePipes()](https://github.com/nestjs/nest/blob/master/packages/common/decorators/core/use-pipes.decorator.ts)

Decorator that binds pipes to the scope of the controller or method, depending on its context.

When `@UsePipes` is used at the controller level, the pipe will be applied to every handler (method) in the controller.

When `@UsePipes` is used at the individual handler level, the pipe will apply only to that specific method.

@param pipes a single pipe instance or class, or a list of pipe instances or classes.

@see [Pipes](https://docs.nestjs.com/pipes)

```typescript
function UsePipes(
...pipes: (PipeTransform | Function)[]
): ClassDecorator & MethodDecorator
```

## [@Version()](https://github.com/nestjs/nest/blob/master/packages/common/decorators/core/version.decorator.ts)

Sets the version of the endpoint to the passed version.

```typescript
function Version(version: VersionValue): MethodDecorator
```

