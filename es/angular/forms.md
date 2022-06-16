# Forms

- [Documentation](https://angular.io/guide/forms-overview)
- [NgModel](https://angular.io/api/forms/NgModel)
- [FormControl](https://angular.io/api/forms/FormControl)

Angular provides two different approaches to handling user input through forms:

- reactive: through the `[formControl]` directive on the form input element
- template-driven: the [(NgModel)] directive creates and manages a FormControl instance for a given form element

Both reactive and template-driven forms are built on the following base classes.

- [FormControl](https://angular.io/api/forms/FormControl) tracks the value and validation status of an individual form control.
- [FormGroup](https://angular.io/api/forms/FormGroup) tracks the same values and status for a collection of form controls.
- [FormArray](https://angular.io/api/forms/FormArray) tracks the same values and status for an array of form controls.
- [ControlValueAccessor](https://angular.io/api/forms/ControlValueAccessor) creates a bridge between Angular FormControl instances and native DOM elements.

## Reactive forms

- [Documentation](https://angular.io/guide/reactive-forms)
- [API summary](https://angular.io/guide/reactive-forms#reactive-forms-api-summary)

Remember to `import {FormsModule, ReactiveFormsModule} from @angular/forms` to module imports: [] metadata

## FormBuilder

- [Documentation](https://angular.io/api/forms/FormBuilder)

The FormBuilder provides syntactic sugar that shortens creating instances of a FormControl, FormGroup, or FormArray. It reduces the amount of boilerplate needed to build complex forms.

## Examples

- [Angular Example - Angular Reactive Forms](https://angular.io/generated/live-examples/reactive-forms/stackblitz.html)
