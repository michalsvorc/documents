
# Documentation



* [Angular Docs](https://angular.io/docs)
* [API List](https://angular.io/api)

# Read



* [Angular Concepts](https://angular.io/guide/architecture#introduction-to-angular-concepts)
* [Glossary](https://angular.io/guide/glossary)
* [Binding syntax](https://angular.io/guide/binding-syntax#binding-syntax-an-overview)
* [Attribute, class, and style bindings](https://angular.io/guide/attribute-binding)
* [Lifecycle event sequence](https://angular.io/guide/lifecycle-hooks#lifecycle-event-sequence)

# [Components](https://angular.io/guide/architecture-components): @<code>[Component](https://angular.io/api/core/Component)()</code>

Components define views, which are sets of screen elements that Angular can choose among and modify according to your program logic and data. Components use services, which provide specific functionality not directly related to views. 

```js


```
@Component({ selector, template, providers, ... })
export class HeroListComponent implements OnInit {}
```


```

# Template [data binding](https://angular.io/guide/architecture-components#data-binding)

{{value}}			[Interpolation and template expressions](https://angular.io/guide/interpolation)	Component -> DOM

[property]=”value”		[Property binding](https://angular.io/guide/property-binding)				Component -> DOM \
(event)=”handler()”		[Event binding (event)](https://angular.io/guide/event-binding)				Component &lt;- DOM \
[(ng-model)]=”property”	[Two-way binding [(...)]](https://angular.io/guide/two-way-binding)				Component &lt;-> DOM

# [Directives](https://angular.io/guide/architecture-components#directives): @[Directive](https://angular.io/api/core/Directive)()

A component is technically a directive. In addition to components, there are two other kinds of directives: structural and attribute. You can build your own directives with @Directive decorator.

[Built-in directives](https://angular.io/guide/built-in-directives)

## [Structural directives](https://angular.io/guide/structural-directives)

Structural directives are responsible for HTML layout. They shape or reshape the DOM's structure, typically by adding, removing, or manipulating elements.

```js


```
<li *ngFor="let hero of heroes"></li>
<app-hero-detail *ngIf="selectedHero"></app-hero-detail>
<div [ngSwitch]="hero?.emotion"> /* *ngSwitchCase */ </div>
```
```


## [Attribute directives](https://angular.io/guide/attribute-directives)

An Attribute directive changes the appearance or behavior of a DOM element, component, or another directive.

```js


```
<div [ngClass]="isSpecial ? 'special' : ''">This div is special</div>
<div [ngStyle]="currentStyles">This div is styled</div>
```
```


# Pipes: @[Pipe](https://angular.io/api/core/Pipe), [[API list](https://angular.io/api?type=pipe)]

Angular pipes let you declare display-value transformations in your template HTML. A class with the @[Pipe](https://angular.io/api/core/Pipe) decorator defines a function that transforms input values to output values for display in a view. To specify a value transformation in an HTML template, use the [pipe operator (|)](https://angular.io/guide/template-expression-operators#pipe).

```js


```
{{interpolated_value | pipe_name}}
```


```

## Unwrapping data from an observable

[AsyncPipe](https://angular.io/api/common/AsyncPipe) is an impure pipe that saves boilerplate code in your component to maintain the subscription and keep delivering values from that observable as they arrive.

# [Services](https://angular.io/guide/architecture-services)

A service is typically a class with a narrow, well-defined purpose. Services are available to components through [dependency injection](https://angular.io/guide/architecture-services#dependency-injection-di).

## [Dependency injection](https://angular.io/guide/architecture-services#dependency-injection-di)

DI is a coding pattern in which a class receives its dependencies from external sources rather than creating them itself.

@[Injectable](https://angular.io/api/core/Injectable)()



* The **injector** is the main mechanism. Angular creates an application-wide injector for you during the bootstrap process, and additional injectors as needed. You don't have to create injectors.
* An injector creates dependencies, and maintains a **container** of dependency instances that it reuses if possible.
* A **provider** is an object that tells an injector how to obtain or create a dependency.

[Providing dependencies in modules](https://angular.io/guide/providers)

## [Providers](https://angular.io/guide/architecture-services#providing-services)

You must register at least one provider of any service you are going to use. You can configure injectors with providers at different levels of your app, by setting a metadata value in one of three places:



* In the @[Injectable](https://angular.io/api/core/Injectable)({providedIn: ‘root’}) decorator for the service itself.
* In the @[NgModule](https://angular.io/api/core/NgModule)({`providers: []}`) decorator for an NgModule.
* In the @[Component](https://angular.io/api/core/Component)(`providers: []}`) decorator for a component.

When you provide the service at the root level, Angular creates a single, shared instance of HeroService and injects it into any class that asks for it.

## [Singleton services](https://angular.io/guide/singleton-services#singleton-services)

A singleton service is a service for which only one instance exists in an app. There are two ways to make a service a singleton in Angular:



* Set the providedIn property of the @[Injectable](https://angular.io/api/core/Injectable)() to "root".
* Include the service in the AppModule or in a module that is only imported by the AppModule

# [Modules](https://angular.io/guide/architecture-modules) @[NgModule](https://angular.io/api/core/NgModule)()

NgModules are containers for a cohesive block of code dedicated to an application domain, a workflow, or a closely related set of capabilities. They can import functionality that is exported from other NgModules, and export selected functionality for use by other NgModules. NgModules provide a compilation context for their components.

Metadata:



* declarations[]: The [components](https://angular.io/guide/architecture-components), directives, and pipes that belong to this NgModule.
* exports[]: The subset of declarations that should be visible and usable in the component templates of other NgModules.
* imports[]: Other modules whose exported classes are needed by component templates declared in this NgModule.
* providers[]: Creators of [services](https://angular.io/guide/architecture-services) that this NgModule contributes to the global collection of services; they become accessible in all parts of the app. (You can also specify providers at the component level.)

[Frequently-used modules](https://angular.io/guide/frequent-ngmodules) \
[Feature modules](https://angular.io/guide/feature-modules) \
[NgModule FAQ](https://angular.io/guide/ngmodule-faq) \
 \
# [Template reference variables (#var)](https://angular.io/guide/template-reference-variables) \
 \
Template variables help you use data from one part of a template in another part of the template. Instead of passing $event target value, you can use template reference: \
 \
```js


```
<!-- The following template variable, #phone, declares a phone variable on an input element. -->
<input #phone placeholder="phone number" />

<!-- phone now refers to the input element; pass its `value` to an event handler -->
<button (click)="callPhone(phone.value)">Call</button>
```


```

# [Communicating with backend services using HTTP](https://angular.io/guide/http)

Angular’s [HttpClient](https://angular.io/api/common/http/HttpClient) returns observables from HTTP method calls. For instance, http.get(‘/api’) returns an observable.

# [Async pipe](https://angular.io/guide/observables-in-angular#async-pipe)

The [AsyncPipe](https://angular.io/api/common/AsyncPipe) subscribes to an observable or promise and returns the latest value it has emitted. When a new value is emitted, the pipe marks the component to be checked for changes.

