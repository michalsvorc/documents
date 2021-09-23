# CSS

* [MDN](https://developer.mozilla.org/en-US/docs/Web/CSS)

Reference:

* [Full reference - MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/Reference)
* [Selectors - MDN](https://developer.mozilla.org/en-US/docs/Learn/CSS/Building_blocks/Selectors#reference_table_of_selectors)
* [Values and units - MDN](https://developer.mozilla.org/en-US/docs/Learn/CSS/Building_blocks/Values_and_units)
* [Web fonts - MDN](https://developer.mozilla.org/en-US/docs/Learn/CSS/Styling_text/Web_fonts)
* [Layout - MDN](https://developer.mozilla.org/en-US/docs/Learn/CSS/CSS_layout)
* [Functions - MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Functions)
* [Media queries - MDN](https://developer.mozilla.org/en-US/docs/Learn/CSS/CSS_layout/Media_queries)
* [Pseudo elements - MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/Pseudo-elements)
* [Pseudo classes - MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/Pseudo-classes)

## Viewport 

* [MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/Viewport_concepts)

A viewport represents the area in computer graphics being currently viewed. In web browser terms, it is generally the
same as the browser window, excluding the UI, menu bar, etc. That is the part of the document you are viewing.

The web contains two viewports, the *layout viewport* and the *visual viewport*.

The visual viewport is the part of the web page that is currently visible in the browser and can change. When the user
pinch-zooms the page, pops open a dynamic keyboard, or when a previously hidden address bar becomes visible, the visual
viewport shrinks but the layout viewport is unchanged.

### Viewport units

* `vw`: % of the viewport's width.
* `vh`: % of the viewport's height.
* `vmin`: % of the viewport's smaller dimension.
* `vmax`: % of the viewport's larger dimension.

### Mobile Viewports

* [MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/Viewport_concepts#Mobile_Viewports)

```html
<meta name="viewport" content="width=device-width">
```

The width property controls the size of the viewport. It should preferably be set to device-width, which is the width of
the screen in CSS pixels at a scale of 100%. There are other properties, including maximum-scale, minimum-scale, and
user-scalable, which control whether users can zoom the page in or out, but the default values are the best for
accessibility and user experience, so these can be omitted.

## CSS Grid

* [Reference - MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Grid_Layout#Reference)
* [Basic Concepts - MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Grid_Layout/Basic_Concepts_of_Grid_Layout)
* [Realizing common layouts - MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Grid_Layout/Realizing_common_layouts_using_CSS_Grid_Layout)

CSS Grid Layout is a two-dimensional layout method enabling the laying out of content in rows and columns.

A grid container's child elements could position themselves so they actually overlap and layer, similar to CSS
positioned elements.

A CSS grid is defined using the `display: grid` property; you can define columns and rows on your grid using
the `grid-template-rows` and `grid-template-columns` properties.

When defining grid tracks using `grid-template-columns` and `grid-template-rows` you may use any length unit, and also
the flex unit, `fr` which indicates a portion of the available space in the grid container.

The `fr` unit distributes available space, not all space. Therefore, if one of your tracks has something large inside it,
there will be less free space to share.

### Lines

* [MDN](https://developer.mozilla.org/en-US/docs/Glossary/Grid_Lines)

Grid lines are created when you define tracks in the explicit grid using CSS Grid Layout. 

Having created a grid, you can place items onto the grid by line number. We can arrange things in accordance with these
lines by specifying the start and end line.

We do this using the following properties:

* grid-column-start
* grid-column-end
* grid-row-start
* grid-row-end

You can also use the shorthand properties:

* grid-column
* grid-row

These let you specify the start and end lines at once, separated by a forward slash `/`:

`grid-column: 1 / 3;`

The lines created in the explicit grid can be named, by adding the name in square brackets before or after the track
sizing information. When placing an item, you can then use these names instead of the line number

### Tracks

* [MDN](https://developer.mozilla.org/en-US/docs/Glossary/Grid_Tracks)

A grid track is the space between two adjacent grid lines. They are defined in the explicit grid by using the
`grid-template-columns` and `grid-template-rows` properties or the shorthand grid or grid-template properties.

The *explicit grid* is the one that you create using `grid-template-columns` or `grid-template-rows`.

The *implicit grid* is created when content is placed outside of that grid, such as into our rows. By default, tracks
created in the implicit grid are auto sized, which in general means that they're large enough to accomodate their
content. If you wish to give implicit grid tracks a size, you can use the `grid-auto-rows` and `grid-auto-columns`
properties.

You can repeat all or merely a section of your track listing using the CSS `repeat` function.

### Gaps

* [MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/gap)

The gap CSS property sets the gaps (gutters) between rows and columns. It is a shorthand for `row-gap` and `column-gap`.

### Grid areas

* [MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/grid-template-areas)

An alternative way to arrange items on your grid is to use the grid-template-areas property and give the various
elements of your design a name.

The `grid-template-areas` CSS property specifies named grid areas, establishing the cells in the grid and assigning them
names.

The rules for grid-template-areas are as follows:

* You need to have every cell of the grid filled.
* To span across two cells, repeat the name.
* To leave a cell empty, use a . (period).
* Areas must be rectangular — you can’t have an L-shaped area for example.
* Areas can't be repeated in different locations.

### minmax()

* [MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/minmax())

The `minmax()` function lets us set a minimum and maximum size for a track, for example, minmax(100px, auto). The minimum
size is 100 pixels, but the maximum is auto, which will expand to accomodate more content.

### fit-content()

* [MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/fit-content())

The `fit-content()` CSS function clamps a given size to an available size according to the formula min(maximum size,
max(minimum size, argument)).

## Flexbox

* [MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Flexible_Box_Layout)
* [Reference - MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Flexible_Box_Layout#reference)
* [Playground](https://flexbox.tech/)

CSS Flexible Box Layout is a module of CSS that defines a CSS box model optimized for user interface design, and the
layout of items in one dimension.

In the flex layout model, the children of a flex container can be laid out in any direction, and can “flex” their sizes,
either growing to fill unused space or shrinking to avoid overflowing the parent.

### Flex container

Create flex container with `display: flex` property.

* [flex-direction](https://developer.mozilla.org/en-US/docs/Web/CSS/flex-direction)

The `flex-direction` CSS property sets how flex items are placed in the flex container defining the *main axis* and the
direction (normal or reversed).

`flex-direction: row | row-reverse | column | column-reverse`

* [flex-wrap](https://developer.mozilla.org/en-US/docs/Web/CSS/flex-wrap)

The `flex-wrap` CSS property sets whether flex items are forced onto one line or can wrap onto multiple lines.

`flex-wrap: nowrap | wrap | wrap-reverse`

* [justify-content](https://developer.mozilla.org/en-US/docs/Web/CSS/justify-content)

The CSS `justify-content` property defines how the browser distributes space between and around content items along the
*main axis* of a flex container, and the inline axis of a grid container.

`justify-content: normal | <content-distribution> | <overflow-position>? [ <content-position> | left | right ]`

* [align-items](https://developer.mozilla.org/en-US/docs/Web/CSS/align-items)

The CSS `align-items` property sets the `align-self` value on all direct children as a group. In Flexbox, it controls
the alignment of items on the *cross axis*. 

`align-items: normal | stretch | <baseline-position> | [ <overflow-position>? <self-position> ]`

* [align-content](https://developer.mozilla.org/en-US/docs/Web/CSS/align-content)

The CSS `align-content` property sets the distribution of space between and around content items along a flexbox's
*cross axis* or a grid's block axis.

`align-content: normal | <baseline-position> | <content-distribution> | <overflow-position>? <content-position>`

### Flex container

* [order](https://developer.mozilla.org/en-US/docs/Web/CSS/order)

The `order` CSS property sets the order (by integer) to lay out an item in a flex or grid container. Items in a
container are sorted by ascending order value and then by their source code order.

* [flex-grow](https://developer.mozilla.org/en-US/docs/Web/CSS/flex-grow)
* [flex-shrink](https://developer.mozilla.org/en-US/docs/Web/CSS/flex-shrink)

The `flex-grow` CSS property sets the flex grow factor of a flex item's main size. This property specifies how much of
the remaining space in the flex container should be assigned to the item (the flex grow factor).

The `flex-shrink` CSS property sets the flex shrink factor of a flex item. If the size of all flex items is larger than
the flex container, items shrink to fit according to flex-shrink.

* [align-self](https://developer.mozilla.org/en-US/docs/Web/CSS/align-self)

The `align-self` CSS property overrides a grid or flex item's align-items value. In Grid, it aligns the item inside the
grid area. In Flexbox, it aligns the item on the *cross axis*.

* [flex-basis](https://developer.mozilla.org/en-US/docs/Web/CSS/flex-basis)

The `flex-basis` CSS property sets the initial main size of a flex item. It sets the size of the content box unless
otherwise set with box-sizing.

## Multiple-column layout

* [MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Columns)

We enable multicol by using one of two properties: `column-count` or `column-width`. The column-count property takes a
number as its value and creates that number of columns.

## Box model

* [MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Box_Model)

The Box Model specification defines a set of keywords that refer to the edges of each part of the box, these are used as
keyword values in CSS including as a value for the `box-sizing` property.

The `box-sizing` CSS property sets how the total width and height of an element is calculated.

* `content-box`: Default. The edge of the content area of the box.
* `padding-box`: The edge of the padding of the box, if there is no padding on a side then this is the same as
  content-box.
* `border-box`: The edge of the border of the box, if there is no border on a side then this is the same as padding-box.
* `margin-box`: The edge of the margin of the box, if there is no margin on a side then this is the same as border-box.
* `stroke-box`: In SVG refers to the stroke bounding box, in CSS treated as content-box.
* `view-box`: In SVG refers to the nearest SVG viewport element’s origin box, which is a rectangle with the width and
  height of the initial SVG user coordinate system established by the viewBox attribute for that element. In CSS treated
  as border-box.

## Images

* [MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Images)

* [object-fit](https://developer.mozilla.org/en-US/docs/Web/CSS/object-fit)

The `object-fit` CSS property sets how the content of a replaced element, such as an `<img>` or `<video>`, should be
resized to fit its container.

* [object-position](https://developer.mozilla.org/en-US/docs/Web/CSS/object-position)

The `object-position` CSS property specifies the alignment of the selected replaced element's contents within the
element's box. Areas of the box which aren't covered by the replaced element's object will show the element's
background.

