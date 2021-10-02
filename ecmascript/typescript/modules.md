# Modules

* [Documentation](https://www.typescriptlang.org/docs/handbook/2/modules.html)
* [Reference](https://www.typescriptlang.org/docs/handbook/modules.html)

Depending on the module target specified during compilation, the compiler will generate appropriate code for:

* [CommonJS](http://wiki.commonjs.org/wiki/CommonJS)
* [AMD](https://github.com/amdjs/amdjs-api/wiki/AMD)
* [UMD](https://github.com/umdjs/umd)
* [SystemJS](https://github.com/systemjs/systemjs)
* [ECMAScript 2015 native modules](http://www.ecma-international.org/ecma-262/6.0/#sec-modules)

In TypeScript, just as in ECMAScript 2015, any file containing a top-level import or export is considered a module.

Conversely, a file without any top-level import or export declarations is treated as a script whose contents are
available in the global scope (and therefore to modules as well).

## Declaration files

* [Documentation](https://www.typescriptlang.org/docs/handbook/declaration-files/introduction.html)
* [TypeScript Deep Dive](https://basarat.gitbook.io/typescript/type-system/intro/d.ts)
* [Modules .d.ts](https://www.typescriptlang.org/docs/handbook/declaration-files/templates/module-d-ts.html)

The `d.ts` file is used to provide typescript type information about an API that's written in pure JavaScript. The idea
is that you're using something like `jQuery` or underscore, an existing JavaScript library. You want to consume those
from your TypeScript code.

Rather than rewriting JavaScript library in typescript, you can instead write the `d.ts` file, which contains only the
type annotations. Then from your typescript code you get the TypeScript benefits of static type checking while still
using a pure JS library.

### Triple-Slash Directives

* [Documentation](https://www.typescriptlang.org/docs/handbook/triple-slash-directives.html)

The `/// <reference path="..." />` directive serves as a declaration of dependency between files.

Triple-slash references instruct the compiler to include additional files in the compilation process. If the compiler
flag `--noResolve` is specified, triple-slash references are ignored.

Add path for TypeScript `.d.ts` file to regular `.ts` file:

```typescript
///<reference path="path/to/file.d.ts" />
```

## Ambient declarations

Ambient declarations are promises that you are making with the compiler. If these do not exist at runtime and you try to
use them, things will break without warning.

Ambient declarations are like docs. If the source changes the docs need to be kept updated. So you might have new
behaviours that work at runtime but no one's updated the ambient declaration and hence you get compiler errors.

### Ambient modules

* [Documentation](https://www.typescriptlang.org/docs/handbook/modules.html#working-with-other-javascript-libraries)

To describe the shape of libraries not written in TypeScript, we need to `declare` the API that the library exposes.

We could define each module in its own `.d.ts` file with top-level export declarations, but it’s more convenient to
write them as one larger `.d.ts` file.

We use a construct similar to ambient namespaces, but we use the `module` keyword and the quoted name of the module
which will be available to a later import.

Example `node.d.ts` file:

```typescript
declare module "path" {
 export function normalize(p: string): string;
 export function join(...paths: any[]): string;
 export var sep: string;
}
```

Regular `.ts` file:

```typescript
/// <reference path="node.d.ts"/>
import * as Path from "path";
```

If you don’t want to take the time to write out declarations before using a new module, you can use a shorthand
declaration to get started quickly.

`declarations.d.ts`:

```typescript
`declare module "hot-new-module";`
```

All imports from a shorthand module will have the `any` type.

See [DefinitelyTyped](https://definitelytyped.org/) repository for TypeScript type definitions.

### Ambient variables

* [TypeScript Deep Dive](https://basarat.gitbook.io/typescript/type-system/intro/variables)

`declare var process: any;`

Or use an interface:

```typescript
interface Process {
  exit(code?: number): void;
}

declare var process: Process;
```

This allows you to use the process variable without TypeScript complaining.

## Module resolution

* [Documentation](https://www.typescriptlang.org/docs/handbook/module-resolution.html)

1. First, the compiler will try to locate a file that represents the imported module. To do so the compiler follows one
   of two different strategies. These strategies tell the compiler where to look for *moduleA*:
   * [Classic](https://www.typescriptlang.org/docs/handbook/module-resolution.html#classic)
   * [Node](https://www.typescriptlang.org/docs/handbook/module-resolution.html#node). 
2. If that didn’t work and if the module name is non-relative (and in the case of *moduleA*, it is), then the compiler
will attempt to locate an ambient module declaration.
3. Finally, if the compiler could not resolve the module, it will log an error.

## Module Output Options

* [Documentation](https://www.typescriptlang.org/docs/handbook/2/modules.html#typescripts-module-output-options)

There are two options which affect the emitted JavaScript output:

* `target` which determines which JS features are downleveled and which are left intact. Which `target` you use is
  determined by the features available in the JavaScript runtime you expect to run the TypeScript code in.
* `module` which determines what code is used for modules to interact with each other.

## Import an export Types

* [TypeScript 3.8](https://devblogs.microsoft.com/typescript/announcing-typescript-3-8-beta/#type-only-imports-exports)

Explicitly import type:

```typescript
import type { APIResponseType } from "./api";
```

Import type is always guaranteed to be removed from your JavaScript, and tools like Babel can make better assumptions
about your code via the `isolatedModules` compiler flag.

### Import a module for side-effects only

Though not recommended practice, some modules set up some global state that can be used by other modules. These modules
may not have any exports, or the consumer is not interested in any of their exports. To import these modules, use:

`import "./my-module.js";`

## Namespaces

* [Namespaces](https://www.typescriptlang.org/docs/handbook/namespaces.html)
* [Namespaces and Modules](https://www.typescriptlang.org/docs/handbook/namespaces-and-modules.html)

TypeScript has its own module format called namespaces which pre-dates the ES Modules standard.

This syntax has a lot of useful features for creating complex definition files, and still sees active use in
[DefinitelyTyped](https://www.typescriptlang.org/dt).

It is also worth noting that, for Node.js applications, modules are the default and we *recommended modules over
namespaces* in modern code.

Starting with ECMAScript 2015, modules are native part of the language, and should be supported by all compliant engine
implementations.

Thus, for new projects modules would be the recommended code organization mechanism.

## Wildcard module declarations

Some module loaders such as *SystemJS* and *AMD* allow non-JavaScript content to be imported. These typically use a
prefix or suffix to indicate the special loading semantics.

Wildcard module declarations can be used to cover these cases.

```typescript
declare module "*!text"
declare module "json!*"
```

## Non-modules

If you have a file that doesn’t currently have any imports or exports, but you want to be treated as a module, add the
line:

```typescript
export {};
```

which will change the file to be a module exporting nothing. This syntax works regardless of your module target.
