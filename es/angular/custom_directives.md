
# Documentation

[Attribute directives](https://angular.io/guide/attribute-directives)

## Overview

An attribute directive minimally requires building a controller class annotated with @[Directive](https://angular.io/api/core/Directive), which specifies the selector that identifies the attribute. The controller class implements the desired directive behavior. Directives must be declared in [Angular Modules](https://angular.io/guide/ngmodules) in the same manner as components. Prefix selector names to ensure they don't conflict with standard HTML attributes.

## Access DOM element: [ElementRef](https://angular.io/api/core/ElementRef)

[ElementRef](https://angular.io/api/core/ElementRef) grants direct access to the host DOM element through its nativeElement property.

## Respond to user-initiated events: @[HostListener](https://angular.io/api/core/HostListener)

The @[HostListener](https://angular.io/api/core/HostListener) decorator lets you subscribe to events of the DOM element that hosts an attribute directive

## Binding to an @[Input](https://angular.io/api/core/Input) property

It adds metadata to the class that makes the directive's highlightColor property available for binding. It's called an input property because data flows from the binding expression into the directive.

