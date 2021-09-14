# Nest decorators

## Core

### [@Controller()](https://github.com/nestjs/nest/blob/master/packages/common/decorators/core/controller.decorator.ts)

Decorator that marks a class as a Nest controller that can receive inbound
requests and produce responses.

`@param prefixOrOptions` a `route path prefix` or a `ControllerOptions` object.
A `route path prefix` is pre-pended to the path specified in any request decorator in the class. `ControllerOptions` is
an options configuration object specifying:
- `scope` - symbol that determines the lifetime of a Controller instance.
[See Scope](https://docs.nestjs.com/fundamentals/injection-scopes#usage) for more details.
- `prefix` - string that defines a `route path prefix`.  The prefix is pre-pended to the path specified in any request
  decorator in the class.
- `version` - string, array of strings, or Symbol that defines the version of all routes in the class. [See
  Versioning](https://docs.nestjs.com/techniques/versioning) for more details.

```typescript
export function Controller(
  prefixOrOptions?: string | string[] | ControllerOptions,
): ClassDecorator
```

See:

- [Routing](https://docs.nestjs.com/controllers#routing)
- [Controllers](https://docs.nestjs.com/controllers)
- [Microservices](https://docs.nestjs.com/microservices/basics#request-response)
- [Scope](https://docs.nestjs.com/fundamentals/injection-scopes#usage)
- [Versioning](https://docs.nestjs.com/techniques/versioning)

### [@Injectable()](https://github.com/nestjs/nest/blob/master/packages/common/decorators/core/injectable.decorator.ts)

Decorator that marks a class as a [provider](https://docs.nestjs.com/providers).  Providers can be injected into other
classes via constructor parameter injection using Nest's built-in [Dependency Injection
(DI)](https://docs.nestjs.com/providers#dependency-injection) system.

`@param options` options specifying scope of injectable

```typescript
export function Injectable(options?: InjectableOptions): ClassDecorator
```

See:

- [Providers](https://docs.nestjs.com/providers)
- [Custom Providers](https://docs.nestjs.com/fundamentals/custom-providers)
- [Injection Scopes](https://docs.nestjs.com/fundamentals/injection-scopes)

### [@Inject()](https://github.com/nestjs/nest/blob/master/packages/common/decorators/core/inject.decorator.ts)

Decorator that marks a constructor parameter as a target for
[Dependency Injection (DI)](https://docs.nestjs.com/providers#dependency-injection).

Injection tokens:

Can be *types* (class names), *strings* or *symbols*. This depends on how the provider with which it is associated was
defined. Providers defined with the `@Injectable()` decorator use the class name. Custom Providers may use strings or
symbols as the injection token.

`@param token` lookup key for the provider to be injected (assigned to the constructor parameter).

```typescript
export function Inject<T = any>(token?: T)
```

See:

- [Providers](https://docs.nestjs.com/providers)
- [Custom Providers](https://docs.nestjs.com/fundamentals/custom-providers)
- [Injection Scopes](https://docs.nestjs.com/fundamentals/injection-scopes)

### [@Optional()](https://github.com/nestjs/nest/blob/master/packages/common/decorators/core/optional.decorator.ts)

Parameter decorator for an injected dependency marking the dependency as optional.

For example:
```typescript
constructor(@Optional() @Inject('HTTP_OPTIONS')private readonly httpClient: T) {}
```

```typescript
export function Optional()
```

See [Optional providers](https://docs.nestjs.com/providers#optional-providers)

## Modules

### [@Module()](https://github.com/nestjs/nest/blob/master/packages/common/decorators/modules/module.decorator.ts)

Decorator that marks a class as a [module](https://docs.nestjs.com/modules).

`@param metadata` module configuration metadata

```typescript
export function Module(metadata: ModuleMetadata): ClassDecorator
```

See [Modules](https://docs.nestjs.com/modules)

### [@Global](https://github.com/nestjs/nest/blob/master/packages/common/decorators/modules/global.decorator.ts)

Decorator that makes a module global-scoped.

Once imported into any module, a global-scoped module will be visible in all modules. Thereafter, modules that wish to
inject a service exported from a global module do not need to import the provider module.

```typescript
export function Global(): ClassDecorator
```

See [Global modules](https://docs.nestjs.com/modules#global-modules)

## HTTP

### [@Header()](https://github.com/nestjs/nest/blob/master/packages/common/decorators/http/header.decorator.ts)

Request method Decorator. Sets a response header.

For example:
`@Header('Cache-Control', 'none')`

`@param name` string to be used for header name
`@param value` string to be used for header value

```typescript
export function Header(name: string, value: string): MethodDecorator
```

See [Headers](https://docs.nestjs.com/controllers#headers)

@HttpCode()
@Redirect()
@Catch()

### [HTTP methods](https://github.com/nestjs/nest/blob/master/packages/common/decorators/http/request-mapping.decorator.ts)

- @Get()
- @Post()
- @Put()
- @Delete()
- @Patch()
- @Options()
- @Head()
- @All()

### HTTP library

@Request(), @Req(): req
@Response(), @Res(): res
@Next(): next
@Session(): req.session
@Param(key?: string): req.params / req.params[key]
@Body(key?: string): req.body / req.body[key]
@Query(key?: string): req.query / req.query[key]
@Headers(name?: string): req.headers / req.headers[name]
@Ip(): req.ip
@HostParam(): req.hosts

## Common

@UsePipes()
@UseInterceptors()
@SetMetadata()
