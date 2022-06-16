# ng-tag

- [freecodecamp.org](https://www.freecodecamp.org/news/everything-you-need-to-know-about-ng-template-ng-content-ng-container-and-ngtemplateoutlet-4b7b51223691)

## ng-template

- [Documentation](https://angular.io/guide/structural-directives#the-ng-template)

Used as a placeholder for structural directives. If there is no structural directive and you merely wrap some elements in a `<ng-template>`, those elements disappear.

```angular
<div *ngIf="true">Truth</div>
<ng-template [ngIf]="true"> Truth </ng-template>
```

## ng-container

- [Documentation](https://angular.io/guide/structural-directives#group-sibling-elements-with-ng-container)

The Angular `<ng-container>` is a grouping element that doesn't interfere with styles or layout because Angular doesn't put it in the DOM. We should use `<ng-container>` when we just want to apply multiple structural directives (nested in each other) without introducing any extra element in our DOM.

## ng-content

- [Documentation](https://angular.io/guide/lifecycle-hooks#content-projection)

You use the `<ng-content>` tag as a placeholder (slot) for that dynamic content, then when the template is parsed Angular will replace that placeholder tag with your content.

### Microsyntax

- [Documentation](https://angular.io/guide/structural-directives#microsyntax)

These microsyntax mechanisms are also available to you when you write your own structural directives. The Angular microsyntax lets you configure a directive in a compact, friendly string.
