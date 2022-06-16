# Module decorators

## @Module()

- [Documentation](https://github.com/nestjs/nest/blob/master/packages/common/decorators/modules/module.decorator.ts)

Decorator that marks a class as a [module](https://docs.nestjs.com/modules).

Modules are used by Nest to organize the application structure into scopes. Controllers and Providers are scoped by the
module they are declared in. Modules and their classes (Controllers and Providers) form a graph that determines how
Nest performs [Dependency Injection (DI)](https://docs.nestjs.com/providers#dependency-injection).

@param metadata module configuration metadata

@see [Modules](https://docs.nestjs.com/modules)

```typescript
export function Module(metadata: ModuleMetadata): ClassDecorator;
```

## @Global

- [Documentation](https://github.com/nestjs/nest/blob/master/packages/common/decorators/modules/global.decorator.ts)

Decorator that makes a module global-scoped.

Once imported into any module, a global-scoped module will be visible in all modules. Thereafter, modules that wish to
inject a service exported from a global module do not need to import the provider module.

@see [Global modules](https://docs.nestjs.com/modules#global-modules)

```typescript
export function Global(): ClassDecorator;
```
