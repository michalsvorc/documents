
# [Component interaction](https://angular.io/guide/component-interaction#component-interaction)

[@Input() and @Output() properties](https://angular.io/guide/inputs-outputs)

## @[Input](https://angular.io/api/core/Input)()

Pass data from parent to child with input binding  [@Input()](https://angular.io/guide/inputs-outputs#input) decorator. Use the @[Input](https://angular.io/api/core/Input)() decorator in a child component or directive to let Angular know that a property in that component can receive its value from its parent component as

```html


```
<!-- parent template -->
<app-hero-child *ngFor="let hero of heroes"
     [hero]="hero"
 </app-hero-child>
```


```

You can Intercept input property changes with a [setter](https://angular.io/guide/component-interaction#intercept-input-property-changes-with-a-setter).

## @[Output](https://angular.io/api/core/Output)()

The child component exposes an [EventEmitter](https://angular.io/api/core/EventEmitter) property with which it emits events when something happens. The parent binds to that event property and reacts to those events. The child's [EventEmitter](https://angular.io/api/core/EventEmitter) property is an output property, typically adorned with an [@Output() decorator](https://angular.io/guide/inputs-outputs#output). Parent listens for child event via [@Output()](https://angular.io/guide/inputs-outputs#how-to-use-output) decorator and [EventEmitter](https://angular.io/api/core/EventEmitter) property

```js


```
// child component
@Output() voted = new EventEmitter<boolean>();

<!-- parent template, $event contains boolean  -->
(voted)="onVoted($event)"> 
```


```

## [@ViewChild()](https://angular.io/api/core/ViewChild)

There may be situations where you want to access a directive, child component, or a DOM element from a parent component class. The ViewChild decorator returns the first element that matches a given directive, component, or template reference selector. 

ViewChild makes it possible to access a child component and call methods or access instance variables that are available to the child.

View queries are set before the ngAfterViewInit lifecycle hook (after Angular has fully initialized a component's view) callback is called.

[How To Use ViewChild in Angular to Access a Child Component, Directive, or DOM Element](https://www.digitalocean.com/community/tutorials/angular-viewchild-access-component)

In cases where you’d want to access multiple children, you’d use ViewChildren instead.

##  Service

Parents and children can communicate via a service.

##  Local variable

Parent interacts with child via #local variable. You can place a local variable, #timer, on the tag `&lt;countdown-timer #timer>` representing the child component. That gives you a reference to the child component and the ability to access any of its *properties* or *methods* from within the parent template. But it is limited because the parent-child wiring must be done entirely within the parent **template**. The parent **component** itself has no access to the child.

