
# Tree-shaking and @[Injectable](https://angular.io/api/core/Injectable)()

Using the @[Injectable](https://angular.io/api/core/Injectable)() providedIn property is preferable to the @[NgModule](https://angular.io/api/core/NgModule)() providers array because with @[Injectable](https://angular.io/api/core/Injectable)() providedIn, optimization tools can perform tree-shaking, which removes services that your app isn't using and results in smaller bundle sizes.

Tree-shaking is especially useful for a library because the application which uses the library may not have a need to inject it. Read more about [tree-shakable providers](https://angular.io/guide/dependency-injection-providers#tree-shakable-providers) in [DI Providers](https://angular.io/guide/dependency-injection-providers).

# [Dynamic component loader with ViewContainerRef](https://angular.io/guide/dynamic-component-loader#dynamic-component-loader) DSMT

Can contain host views (created by instantiating a component with the createComponent() method), and embedded views (created by instantiating a [TemplateRef](https://angular.io/api/core/TemplateRef) with the createEmbeddedView() method).

# [Angular Elements](https://angular.io/guide/elements#angular-elements-overview) DSMT

Angular elements are Angular components packaged as custom elements (also called Web Components), a web standard for defining new HTML elements in a framework-agnostic way.

[Angular Elements Quick Start](https://www.youtube.com/watch?v=4u9_kdkvTsc)

# Lifecycle

[AfterContent and AfterView](https://stackoverflow.com/questions/51410660/angular-afterviewinit-vs-aftercontentinit)

