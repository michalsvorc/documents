# Accessibility

Overview:

* [WCAG 2 Checklist - WebAIM](https://webaim.org/standards/wcag/checklist)
* [Accessibility - Google developers](https://developers.google.com/web/fundamentals/accessibility)
* [Accessible to all -
  web.dev](https://web.dev/accessible/#create-a-design-and-css-that-supports-users-with-different-needs)

Libraries:

* [Accessibility test suites - Google
  developers](https://developers.google.com/web/fundamentals/accessibility/how-to-review#automate_the_process)

Impairments fall into four broad buckets: visual, motor, hearing, and cognitive.

## ARIA

* [Introduction to ARIA - Google
  developers](https://developers.google.com/web/fundamentals/accessibility/semantics-aria)
* [ARIA - MDN](https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA)
* [Roles - MDN](https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA/Roles)
* [ARIA Authoring Practices - W3](https://www.w3.org/TR/wai-aria-practices-1.1/)


Many of the ARIA widgets were later incorporated into HTML5, and developers should prefer using the correct semantic
HTML element over using ARIA, if such an element exists. For instance, native elements have built-in keyboard
accessibility, roles and states. 

A standard HTML `<input type="checkbox">` element doesn't need an additional role="checkbox" ARIA attribute to be
correctly announced.

But there are times when a simple layout and native HTML won't do the job.

ARIA enables developers to describe their widgets in more detail by adding special attributes to the markup. Designed to
fill the gap between standard HTML tags and the desktop-style controls found in dynamic web applications, ARIA provides
roles and states that describe the behavior of most familiar UI widgets.

Although ARIA allows us to subtly (or even radically) modify the accessibility tree for any element on the page, that is
the only thing it changes. ARIA doesn't augment any of the element's inherent behavior; it won't make the element
focusable or give it keyboard event listeners. That is still part of our development task.

The ARIA specification is split up into three different types of attributes: roles, states, and properties. 

### Labels

* [ARIA Labels and Relationships - Google
  developers](https://developers.google.com/web/fundamentals/accessibility/semantics-aria/aria-labels-and-relationships)

* `aria-label`: Allows us to specify a string to be used as the accessible label. This overrides any other native
  labeling mechanism, such as a label element.
* `aria-labelledby`: Allows us to specify the ID of another element in the DOM as an element's label. aria-labelledby
  may be used on any element, not just labelable elements.
* `aria-describedby`: Provides an accessible description in the same way that aria-labelledby provides a label. Like
  aria-labelledby, aria-describedby may reference elements that are otherwise not visible, whether hidden from the DOM,
  or hidden from assistive technology users.
* `aria-owns`: This attribute allows us to tell assistive technology that an element that is separate in the DOM should
  be treated as a child of the current element, or to rearrange existing child elements into a different order. 

### Hidden content

* [Hiding and Updating Content - Google
  developers](https://developers.google.com/web/fundamentals/accessibility/semantics-aria/hiding-and-updating-content)
* [Techniques for hiding content - WebAIM](https://webaim.org/techniques/css/invisiblecontent/#techniques)

Anything that has a CSS style of `visibility: hidden` or `display: none` or uses the HTML5 `hidden` attribute will also
be hidden from assistive technology users.

However, an element that is not visually rendered but not explicitly hidden is still included in the accessibility tree.
One common technique is to include screen reader only text CSS class.

Finally, ARIA provides a mechanism for excluding content from assistive technology that is not visually hidden, using
the `aria-hidden` attribute. Applying this attribute to an element effectively removes it and all of its descendants
from the accessibility tree. The only exceptions are elements referred to by an `aria-labelledby` or `aria-describedby`
attribute.

### Updating content

* [Hiding and Updating Content - Google
  developers](https://developers.google.com/web/fundamentals/accessibility/semantics-aria/hiding-and-updating-content)

`aria-live` lets developers mark a part of the page as "live" in the sense that updates should be communicated to users
immediately regardless of the page position, rather than if they just happen to explore that part of the page. 

When an element has an aria-live attribute, the part of the page containing it and its descendants is called a live
region. For example, a live region might be a status message that appears as a result of a user action. 

aria-live has three allowable values:

* `aria-live="polite"` tells assistive technology to alert the user to this change when it has finished whatever it is
  currently doing.
* `aria-live="assertive"` tells assistive technology to interrupt whatever it's doing and alert the user to this change
  immediately.
* `aria-live="off"` tells assistive technology to temporarily suspend aria-live interruptions.

## Tabindex 

* [Tabindex - MDN](https://developer.mozilla.org/en-US/docs/Web/HTML/Global_attributes/tabindex)
* [Using tabindex - Google
  developers](https://developers.google.com/web/fundamentals/accessibility/focus/using-tabindex)

The tabindex global attribute indicates that its element can be focused, and where it participates in sequential
keyboard navigation (usually with the Tab key, hence the name).

* `tabindex="0"`: Inserts an element into the natural tab order. The element can be focused by pressing the Tab key, and
  the element can be focused by calling its focus() method.
* `tabindex="-1"`: Removes an element from the natural tab order, but the element can still be focused by calling its
  focus() method.
* `tabindex="5"`: Any tabindex greater than 0 jumps the element to the front of the natural tab order. If there are
  multiple elements with a tabindex greater than 0, the tab order starts from the lowest value that is greater than zero
  and works its way up.

Using a tabindex greater than 0 is considered an anti-pattern. This is particularly true of non-input elements like
headers, images, or article titles. Adding tabindex to those kinds of elements is counter-productive. If possible, it's
best to arrange your source code so the DOM sequence provides a logical tab order.
