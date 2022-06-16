
# &lt;ng-{tag}>

Read more: [freecodecamp.org](https://www.freecodecamp.org/news/everything-you-need-to-know-about-ng-template-ng-content-ng-container-and-ngtemplateoutlet-4b7b51223691)

## [&lt;ng-template>](https://angular.io/guide/structural-directives#the-ng-template)

Used as a placeholder for structural directives. If there is no structural directive and you merely wrap some elements in a &lt;ng-template>, those elements disappear.

```js

&lt;div *ngIf="true">

    Truth

&lt;/div>

&lt;ng-template [ngIf]="true">

    Truth

&lt;/ng-template>

```

## [&lt;ng-container>](https://angular.io/guide/structural-directives#group-sibling-elements-with-ng-container)

The Angular &lt;ng-container> is a grouping element that doesn't interfere with styles or layout because Angular doesn't put it in the DOM. We should use &lt;ng-container> when we just want to apply multiple structural directives (nested in each other) without introducing any extra element in our DOM.

## [&lt;ng-content>](https://angular.io/guide/lifecycle-hooks#content-projection)

 You use the &lt;ng-content>&lt;/ng-content> tag as a placeholder (slot) for that dynamic content, then when the template is parsed Angular will replace that placeholder tag with your content.

### [Microsyntax](https://angular.io/guide/structural-directives#microsyntax)

These microsyntax mechanisms are also available to you when you write your own structural directives. The Angular microsyntax lets you configure a directive in a compact, friendly string. 

