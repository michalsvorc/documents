
# [Forms](https://angular.io/guide/forms-overview)

Angular provides two different approaches to handling user input through forms:



* reactive: through the [formControl] directive on the form input element
* template-driven: the [([NgModel](https://angular.io/api/forms/NgModel))] directive creates and manages a [FormControl](https://angular.io/api/forms/FormControl) instance for a given form element

Both reactive and template-driven forms are built on the following base classes.



* [FormControl](https://angular.io/api/forms/FormControl) tracks the value and validation status of an individual form control.
* [FormGroup](https://angular.io/api/forms/FormGroup) tracks the same values and status for a collection of form controls.
* [FormArray](https://angular.io/api/forms/FormArray) tracks the same values and status for an array of form controls.
* [ControlValueAccessor](https://angular.io/api/forms/ControlValueAccessor) creates a bridge between Angular [FormControl](https://angular.io/api/forms/FormControl) instances and native DOM elements.

# [Reactive forms](https://angular.io/guide/reactive-forms)

Remember to import import {FormsModule, ReactiveFormsModule} from '@angular/forms'; to module imports: [] metadata

[API summary](https://angular.io/guide/reactive-forms#reactive-forms-api-summary)

## [FormBuilder](https://angular.io/api/forms/FormBuilder)

The [FormBuilder](https://angular.io/api/forms/FormBuilder) provides syntactic sugar that shortens creating instances of a [FormControl](https://angular.io/api/forms/FormControl), [FormGroup](https://angular.io/api/forms/FormGroup), or [FormArray](https://angular.io/api/forms/FormArray). It reduces the amount of boilerplate needed to build complex forms.

## Examples

[Angular Example - Angular Reactive Forms (Demo runner)](https://angular.io/generated/live-examples/reactive-forms/stackblitz.html)

