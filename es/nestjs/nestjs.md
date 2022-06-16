# NestJS

Overview:

- [Documentation](https://docs.nestjs.com/first-steps)
- [Examples](https://github.com/nestjs/nest/tree/master/sample/)
- [CLI](https://docs.nestjs.com/cli/usages)
- [Built-in HTTP exceptions](https://docs.nestjs.com/exception-filters#built-in-http-exceptions)
- [Built-in pipes](https://docs.nestjs.com/pipes#built-in-pipes)

Topics:

- [Standalone applications](https://docs.nestjs.com/standalone-applications)
- [Middleware](https://docs.nestjs.com/middleware)
- [Class validator](https://docs.nestjs.com/pipes#class-validator)
- [Decorator composition](https://docs.nestjs.com/custom-decorators#decorator-composition)
- [Lifecycle events](https://docs.nestjs.com/fundamentals/lifecycle-events)
- [Request lifecycle](https://docs.nestjs.com/faq/request-lifecycle)
- [Lazy loading modules](https://docs.nestjs.com/fundamentals/lazy-loading-modules)
- [Testing](https://docs.nestjs.com/fundamentals/testing)
- [Validation mapped types](https://docs.nestjs.com/techniques/validation#mapped-types)
- [Workspaces](https://docs.nestjs.com/cli/monorepo)

Resources:

- [Awesome Nest](https://github.com/juliandavidmr/awesome-nestjs)

## Design

- Singleton instances means returning the existing instance if it has already been requested elsewhere.
- lmost everything is shared across incoming requests.
- Application graph is the internal data structure Nest uses to resolve module and provider relationships and
  dependencies.
- Nest has a built-in inversion of control ("IoC") container that resolves relationships between providers. 

## Controllers

- [Overview](https://docs.nestjs.com/controllers)
- [Full resource sample](https://docs.nestjs.com/controllers#full-resource-sample)

A controller's purpose is to receive specific requests for the application. The
[routing](https://docs.nestjs.com/controllers#routing) mechanism controls which controller receives which requests.
Controllers should handle HTTP requests and delegate more complex tasks to providers.

Controllers always belong to a module:

```typescript
@Module({
  controllers: [CatsController],
})
```

### Routing

- [Overview](https://docs.nestjs.com/controllers#routing)

Nest employs two different options for manipulating responses:

- Standard (recommended): The response's status code is always 200 by default, except for POST requests which use *201*. 
- Library-specific: We can use the library-specific (e.g., Express) response object, which can be injected using the
  `@Res()` decorator.

Topics:

- [Request object](https://docs.nestjs.com/controllers#request-object)
- [Status code](https://docs.nestjs.com/controllers#status-code)
- [Headers](https://docs.nestjs.com/controllers#headers)
- [Redirection](https://docs.nestjs.com/controllers#redirection): The default value of statusCode is *302*.
- [Route parameters](https://docs.nestjs.com/controllers#route-parameters)
- [Custom route decorators](https://docs.nestjs.com/custom-decorators)

### Asynchronicity

- [Controllers guide](https://docs.nestjs.com/controllers#asynchronicity)

Nest route handlers are able to return RxJS observable streams. Nest will automatically subscribe to the source
underneath and take the last emitted value (once the stream is completed).

```typescript
// Promise based example
@Get()
async findAll(): Promise<any[]> {
  return [];
}

// Observable based example
@Get()
findAll(): Observable<any[]> {
  return of([]);
}
```

### DTO

- [Request payloads](https://docs.nestjs.com/controllers#request-payloads)

We could determine the DTO schema by using TypeScript interfaces, or by simple classes. We recommend using classes here,
as they are preserved as real entities in the compiled JavaScript.

### Controller scope

- [Fundamentals](https://docs.nestjs.com/fundamentals/injection-scopes#controller-scope)

For a request-scoped controller, a new instance is created for each inbound request, and garbage-collected when the
request has completed processing.)

## Providers

- [Overview](https://docs.nestjs.com/providers)
- [Custom providers](https://docs.nestjs.com/fundamentals/custom-providers#custom-providers-1)
- [Asynchronous providers](https://docs.nestjs.com/fundamentals/async-providers)

Providers are plain JavaScript classes that are declared as `providers` in a module.

The main idea of a provider is that it can be injected as *dependency*. Many of the basic Nest classes may be treated as
a provider – services, repositories, factories, helpers, and so on. 

In Nest, thanks to TypeScript capabilities, it's extremely easy to manage dependencies because they are resolved just by
type. Nest will resolve the provider by creating and returning an instance of that provider (or, in the normal case of a
singleton, returning the existing instance if it has already been requested elsewhere). This dependency is resolved and
passed to the constructor.

The `@Injectable()` decorator attaches metadata, which declares that a class can be managed by the Nest IoC container.

To indicate a provider is optional, use the `@Optional()` decorator in the constructor's signature.

### Property-based injection

- [Overview](https://docs.nestjs.com/providers#property-based-injection)
- [Fundamentals](https://docs.nestjs.com/fundamentals/custom-providers#non-class-based-provider-tokens)

If your top-level class depends on either one or multiple providers, passing them all the way up by calling `super()` in
sub-classes from the constructor can be very tedious. In order to avoid this, you can use the `@Inject()` decorator at the
property level.

If your class doesn't extend another provider, you should always prefer using constructor-based injection.

```tyepscript
constructor(@Inject('CONNECTION') connection: Connection) {}
```

In this example, we are associating a string-valued token 'CONNECTION' with a pre-existing connection object we've
imported from an external file.

### Scopes

- [Fundamentals](https://docs.nestjs.com/fundamentals/injection-scopes)

A provider can have any of the following scopes:

- DEFAULT: A single instance of the provider is shared across the entire application. The instance lifetime is tied
  directly to the application lifecycle. Once the application has bootstrapped, all singleton providers have been
  instantiated. Singleton scope is used by default.
- REQUEST: A new instance of the provider is created exclusively for each incoming request. The instance is
  garbage-collected after the request has completed processing.
- TRANSIENT: Transient providers are not shared across consumers. Each consumer that injects a transient provider will
  receive a new, dedicated instance.

### Custom Providers

- [Fundamentals](https://docs.nestjs.com/fundamentals/custom-providers)

Use cases:

- You want to create a custom instance instead of having Nest instantiate (or return a cached instance of) a class.
- You want to re-use an existing class in a second dependency.
- You want to override a class with a mock version for testing.

Nest provides several ways to define custom providers:

- Value providers: `useValue`
- Non-class-based provider tokens: strings or symbols as the DI token with the `@Inject()` decorator
- Class providers: `useClass`
- Factory providers: `useFactory`, allows for creating providers dynamically
- Alias providers: `useExisting`

While providers often supply services, they are not limited to that usage. A provider can supply *any value*. For example,
a provider may supply an array of configuration objects based on the current environment.

### Asynchronous providers

- [Fundamentals](https://docs.nestjs.com/fundamentals/async-providers)

At times, the application start should be delayed until one or more asynchronous tasks are completed. For example, you
may not want to start accepting requests until the connection with the database has been established.

## Modules

- [Overview](https://docs.nestjs.com/modules)
- [Introduction](https://docs.nestjs.com/fundamentals/dynamic-modules#introduction)

A module is a class annotated with a @Module() decorator.

Modules define groups of components like providers and controllers that fit together as a modular part of an overall
application. They provide an execution context, or scope, for these components.

In Nest, modules are singletons by default, and thus you can share the same instance of any provider between multiple
modules effortlessly.

The @Module() decorator takes a single object whose properties describe the module:

- *providers*: The providers that will be instantiated by the Nest injector and that may be shared at least across this
  module.
- *controllers*: The set of controllers defined in this module which have to be instantiated.
- *imports*: The list of imported modules that export the providers which are required in this module.
- *exports*: The subset of providers that are provided by this module and should be available in other modules which
  import this module.

Providers defined in a module are visible to other members of the module without the need to export them. When a
provider needs to be visible outside of a module, it is first exported from its host module, and then imported into its
consuming module.

The module encapsulates providers by default. This means that it's impossible to inject providers that are neither
directly part of the current module nor exported from the imported modules. Thus, you may consider the exported
providers from a module as the module's public interface, or API.

### Shared modules

- [Overview](https://docs.nestjs.com/modules#shared-modules)

Every module is automatically a shared module. Once created it can be reused by any module. 

Let's imagine that we want to share an instance of the CatsService between several other modules. In order to do that,
we first need to *export* the CatsService provider:

```typescript
@Module({
  controllers: [CatsController],
  providers: [CatsService],
  exports: [CatsService]
})
```

Now any module that imports this module has access to the CatsService and will share the same *instance* with all other
modules that import it as well.

In addition, modules can [re-export modules](https://docs.nestjs.com/modules#module-re-exporting) that they import.

### Global modules

- [Overview](https://docs.nestjs.com/modules#global-modules)

Nest encapsulates providers inside the module scope. You aren't able to use a module's providers elsewhere without first
importing the encapsulating module.

The `@Global()` decorator makes the module global-scoped. Global modules should be registered only once, generally by
the root or core module.

Making everything global is not a good design decision. Global modules are available to reduce the amount of necessary
boilerplate. The imports array is generally the preferred way to make the module's API available to consumers.

### Dynamic modules

- [Overview](https://docs.nestjs.com/modules#dynamic-modules) 
- [Fundamentals](https://docs.nestjs.com/fundamentals/dynamic-modules)
- [Example](https://github.com/nestjs/nest/tree/master/sample/25-dynamic-modules)

This feature enables you to easily create customizable modules that can register and configure providers dynamically.

In other words, dynamic modules provide an API for importing one module into another, and customizing the properties and
behavior of that module when it is imported, as opposed to using the static bindings.

Dynamic modules must return an object with the exact same interface, plus one additional property called `module`. The
`module` property serves as the name of the module, and should be the same as the class name of the module.

### Module reference

- [Fundamentals](https://docs.nestjs.com/fundamentals/module-ref)

Nest provides the ModuleRef class to navigate the internal list of providers and obtain a reference to any provider using its injection token as a lookup key. 

The ModuleRef class also provides a way to dynamically instantiate both static and scoped providers.

## Pipes

- [Overview](https://docs.nestjs.com/pipes)
- [Providing defaults](https://docs.nestjs.com/pipes#providing-defaults)

- A pipe is a class annotated with the `@Injectable()` decorator.
- Pipes should implement the `PipeTransform` interface.

Pipes have two typical use cases:

- transformation: transform input data to the desired form (e.g., from string to integer)
- validation: evaluate input data and if valid, simply pass it through unchanged; otherwise, throw an exception when the
  data is incorrect

Nest supports both synchronous and asynchronous pipes.

### Exceptions in pipes

Pipes run inside the exceptions zone. This means that when a Pipe throws an exception it is handled by the exceptions
layer (global exceptions filter and any exceptions filters that are applied to the current context). Given the above, it
should be clear that when an exception is thrown in a Pipe, no controller method is subsequently executed. This gives
you a best-practice technique for validating data coming into the application from external sources at the system
boundary. 

## Exception filters

- [Overview](https://docs.nestjs.com/exception-filters)

### Standard exceptions

Nest comes with a built-in exceptions layer which is responsible for processing all unhandled exceptions across an
application.

The global exception filter partially supports the `http-errors` library. Basically, any thrown exception containing the
statusCode and message property will be properly populated and send back as a response (instead of the default
InternalServerErrorException for unrecognized exceptions).

### Custom exceptions

- [Overview](https://docs.nestjs.com/exception-filters#custom-exceptions)

For full full control over the exceptions layer, use custom exception filters. Exception filters let you control the
exact flow of control and the content of the response sent back to the client.

### Catch all

In order to catch every unhandled exception (regardless of the exception type), leave the @Catch() decorator's parameter
list empty

## Guards

- [Overview](https://docs.nestjs.com/guards)

- A guard is a class annotated with the `@Injectable()` decorator.
- Guards should implement the `CanActivate` interface.

Guards determine whether a given request will be handled by the route handler or not, depending on certain conditions
(like permissions, roles, ACLs, etc.) present at run-time.

Guards are executed after each middleware, but before any interceptor or pipe.

### Comparison to authentication middleware

Middleware, by its nature, is dumb. It doesn't know which handler will be executed after calling the next() function. On
the other hand, Guards have access to the ExecutionContext instance, and thus know exactly what's going to be executed
next.

They're designed, much like exception filters, pipes, and interceptors, to let you interpose processing logic at exactly
the right point in the request/response cycle, and to do so declaratively. 

## Interceptors

- [Overview](https://docs.nestjs.com/interceptors)
- [Response mapping](https://docs.nestjs.com/interceptors#response-mapping)
- [Exception mapping](https://docs.nestjs.com/interceptors#exception-mapping)
- [Stream overriding, e.g. caching](https://docs.nestjs.com/interceptors#stream-overriding)

- An interceptor is a class annotated with the `@Injectable()` decorator.
- Interceptors should implement the `NestInterceptor` interface.

Usage:

- bind extra logic before / after method execution
- transform the result returned from a function
- transform the exception thrown from a function
- extend the basic function behavior
- completely override a function depending on specific conditions (e.g., for caching purposes)

### Call handler

- [Overview](https://docs.nestjs.com/interceptors#call-handler)

The `intercept()` method effectively wraps the request/response stream. As a result, you may implement custom logic both
*before* and *after* the execution of the final route handler.

## Dependency injection

- [Fundamentals](https://docs.nestjs.com/fundamentals/custom-providers#di-fundamentals)
- [Circular dependency](https://docs.nestjs.com/fundamentals/circular-dependency)

Dependency injection is an inversion of control (IoC) technique wherein you delegate instantiation of dependencies to
the IoC container (in our case, the NestJS runtime system), instead of doing it in your own code imperatively. 

Constructor based dependency injection is used to inject instances (often service providers) into classes. 

Passing a token (instead of an instance) into a constructor means leaving responsibility for instantiation to the
framework and enabling dependency injection.

### Instance levels

- The construction above attaches the interceptor to every handler declared by this controller.
- If we want to restrict the interceptor's scope to a single method, we simply apply the decorator at the method level.
- In order to set up a global interceptor, we use the `useGlobalInterceptors()` method of the Nest application instance.

### Constructor injection

CatsController declares a dependency on the CatsService token with constructor injection:
```typescript
constructor(private catsService: CatsService)
```

When the Nest IoC container instantiates a CatsController, it first looks for any dependencies. When it finds the
CatsService dependency, it performs a lookup on the CatsService token, which returns the CatsService class, per the
registration step.

Assuming SINGLETON scope (the default behavior), Nest will then either create an instance of CatsService, cache it, and
return it, or if one is already cached, return the existing instance.

### Constructor injection with new instance

We can also pass a new instance and define custom instance only for this constructor:

```typescript
constructor(private catsService: new CatsService(customOptions))
```

## Injection tokens

Examples:

- [Dynamic module configuration](https://docs.nestjs.com/fundamentals/dynamic-modules#module-configuration)
- [Non-class-based provider tokens](https://docs.nestjs.com/fundamentals/custom-providers#non-class-based-provider-tokens)

In addition to using strings as token values, you can also use JavaScript `symbols` or TypeScript `enums`.

## Execution context

- [Fundamentals](https://docs.nestjs.com/fundamentals/execution-context)

Nest provides several utility classes that help make it easy to write applications that function across multiple
application contexts (e.g., Nest HTTP server-based, microservices and WebSockets application contexts).

### ArgumentsHost class

- [Overview](https://docs.nestjs.com/exception-filters#arguments-host)
- [Fundamentals](https://docs.nestjs.com/fundamentals/execution-context#argumentshost-class)

The `ArgumentsHost` class provides methods for retrieving the arguments being passed to a handler. 

The framework provides an instance of `ArgumentsHost`, typically referenced as a `host` parameter, in places where you
may want to access it.

`ArgumentsHost` simply acts as an abstraction over a handler's arguments.

### ExecutionContext class

- [Fundamentals](https://docs.nestjs.com/fundamentals/execution-context#executioncontext-class)

`ExecutionContext` extends `ArgumentsHost`, providing additional details about the current execution process.

Like `ArgumentsHost`, Nest provides an instance of `ExecutionContext` in places you may need it, such as in the
`canActivate()` method of a guard and the `intercept()` method of an interceptor.

- The `getHandler()` method returns a reference to the handler about to be invoked.
- The `getClass()` method returns the type of the Controller class which this particular handler belongs to.

The ability to access references to both the current class and handler method provides great flexibility. Most
importantly, it gives us the opportunity to access the metadata set through the `@SetMetadata()` decorator from within
guards or interceptors.

### Reflection and metadata

- [Fundamentals](https://docs.nestjs.com/fundamentals/execution-context#reflection-and-metadata)

Nest provides the ability to attach *custom metadata* to route handlers through the `@SetMetadata()` decorator.

To access the route's custom metadata set with the `@SetMetadata()` decorator, we'll use the `Reflector#get` method.

It's not good practice to use `@SetMetadata()` directly in your routes. Instead, create your own decorators.

## Serialization

- [Fundamentals](https://docs.nestjs.com/techniques/serialization)
- [Example](https://github.com/nestjs/nest/tree/master/sample/21-serializer)

Serialization is a process that happens before objects are returned in a network response. 

The built-in `ClassSerializerInterceptor` interceptor uses the powerful class-transformer package to provide a declarative
and extensible way of transforming objects. It can apply rules expressed by class-transformer decorators.

## HTTP module

- [Fundamentals](https://docs.nestjs.com/techniques/http-module)

The HttpModule exports the HttpService class, which exposes [Axios](https://github.com/axios/axios)-based methods to
perform HTTP requests. The library also transforms the resulting HTTP responses into Observables.

