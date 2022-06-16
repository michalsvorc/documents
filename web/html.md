# HTML

- [MDN](https://developer.mozilla.org/en-US/docs/Web/HTML)
- [Reference - MDN](https://developer.mozilla.org/en-US/docs/Web/HTML/Reference)

Topics:

- [Common solutions- MDN](https://developer.mozilla.org/en-US/docs/Learn/HTML/Howto)

## Text

- [`<dl>`: The Description list element](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/dl)
  - [`<dt>`: The Description title element](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/dt)
  - [`<dd>`: The Description details element](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/dd)

The `<dl>` HTML element represents a description list. The element encloses a list of groups of terms (specified using
the `<dt>` element) and descriptions (provided by `<dd>` elements). Common uses for this element are to implement a
glossary or to display metadata (a list of key-value pairs).

- [`<blockquote>`: The Block Quotation element](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/blockquote)

The `<blockquote>` HTML element indicates that the enclosed text is an extended quotation. Usually, this is rendered
visually by indentation (see Notes for how to change it). A URL for the source of the quotation may be given using the
`cite` attribute, while a text representation of the source can be given using the `<cite>` element.

- [`<cite>`: The Citation element](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/cite)

The `<cite>` HTML element is used to describe a reference to a cited creative work, and must include the title of that
work.

- [`<q>`: The Inline Quotation element](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/q)

This element is intended for short quotations that don't require paragraph breaks; for long quotations use the
`<blockquote>` element.

- [`<address>`: The Contact Address element](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/address)

- [`<time>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/time)

The `<time>` HTML element represents a specific period in time. It may include the `datetime` attribute to translate
dates into machine-readable format, allowing for better search engine results or custom features such as reminders.

- [`<abbr>`: The Abbreviation element](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/abbr)

The `<abbr>` HTML element represents an abbreviation or acronym; the optional title attribute can provide an expansion
or description for the abbreviation.

- [`<dfn>`: The Definition element](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/dfn)

The `<dfn>` HTML element is used to indicate the term being defined within the context of a definition phrase or
sentence.

- [`<mark>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/mark)

The `<mark>` HTML element represents text which is marked or highlighted for reference or notation purposes, due to the
marked passage's relevance or importance in the enclosing context.

- [`<data>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/data)

The `<data>` HTML element links a given piece of content with a machine-readable translation. If the content is time- or
date-related, the `<time>` element must be used.

- [`<wbr>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/wbr)

The `<wbr>` HTML element represents a word break opportunity—a position within text where the browser may optionally
break a line, though its line-breaking rules would not otherwise create a break at that location.

## Representing computer code

There are a number of elements available for marking up computer code using HTML:

- `<code>`: For marking up generic pieces of computer code.
- `<pre>`: For retaining whitespace (generally code blocks) — if you use indentation or excess whitespace inside your
  text, browsers will ignore it and you will not see it on your rendered page. If you wrap the text in `<pre></pre>`
  tags however, your whitespace will be rendered identically to how you see it in your text editor.
- `<var>`: For specifically marking up variable names.
- `<kbd>`: For marking up keyboard (and other types of) input entered into the computer.
- `<samp>`: For marking up the output of a computer program.
- `<output>`: The `<output>` HTML element is a container element into which a site or app can inject the results of a
  calculation or the outcome of a user action. The `<output>` value, name, and contents are NOT submitted during form
  submission.

## Meters and progress bars

- [`<progress>`: The Progress Indicator element](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/progress)

The `<progress>` HTML element displays an indicator showing the completion progress of a task, typically displayed as a
progress bar.

- [`<meter>`: The HTML Meter element](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/meter)

The `<meter>` HTML element represents either a scalar value within a known range or a fractional value.

## Datalist

- [`<datalist>`: The HTML Data List element](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/datalist)

The `<datalist>` HTML element contains a set of `<option>` elements that represent the permissible or recommended
options available to choose from within other controls. The `<datalist>` provides a list of predefined values to suggest
to the user for this input. Any values in the list that are not compatible with the type are not included in the
suggested options.

See also the `<input>` element, and more specifically its list attribute.

## Link types

- [MDN](https://developer.mozilla.org/en-US/docs/Web/HTML/Link_types)

- [`<a>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/a)

The `<a>` HTML element (or anchor element), with its href attribute, creates a hyperlink to web pages, files, email
addresses, locations in the same page, or anything else a URL can address.

- [`<area>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/area)

The `<area>` HTML element defines an area inside an image map that has predefined clickable areas. An image map allows
geometric areas on an image to be associated with hypertext link. This element is used only within a `<map>` element.

- [`<link>`: The External Resource Link element](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/link)

The `<link>` HTML element specifies relationships between the current document and an external resource. This element is
most commonly used to link to stylesheets, but is also used to establish site icons (both "favicon" style icons and
icons for the home screen and apps on mobile devices) among other things.

## Multimedia

- [Media type and format guide - MDN](https://developer.mozilla.org/en-US/docs/Web/Media/Formats)
- [Multimedia and Embedding - MDN](https://developer.mozilla.org/en-US/docs/Learn/HTML/Multimedia_and_embedding)

- The `<area>` HTML element defines an area inside an image map that has predefined clickable areas. An image map allows
  geometric areas on an image to be associated with Hyperlink.
- The `<audio>` HTML element is used to embed sound content in documents. It may contain one or more audio sources,
  represented using the src attribute or the source element: the browser will choose the most suitable one. It can also
  be the destination for streamed media, using a MediaStream.
- The `<img>` HTML element embeds an image into the document.
- The `<map>` HTML element is used with area elements to define an image map (a clickable link area).
- The `<track>` HTML element is used as a child of the media elements, audio and video. It lets you specify timed text
  tracks (or time-based data), for example to automatically handle subtitles. The tracks are formatted in WebVTT format
  (.vtt files) — Web Video Text Tracks.
- The `<video>` HTML element embeds a media player which supports video playback into the document. You can use
  `<video>` for audio content as well, but the audio element may provide a more appropriate user experience.

## Interactive elements

- The `<details>` HTML element creates a disclosure widget in which information is visible only when the widget is
  toggled into an "open" state. A summary or label must be provided using the summary element.
- The `<summary>` HTML element specifies a summary, caption, or legend for a details element's disclosure box. Clicking
  the `<summary>` element toggles the state of the parent `<details>` element open and closed.
- The `<dialog>` HTML element represents a dialog box or other interactive component, such as a dismissible alert,
  inspector, or subwindow.
- The `<menu>` HTML element is a semantic alternative to ul. It represents an unordered list of items (represented by li
  elements), each of these represent a link or other command that the user can activate.

## Embedded content

- The `<embed>` HTML element embeds external content at the specified point in the document. This content is provided by
  an external application or other source of interactive content such as a browser plug-in.
- The `<iframe>` HTML element represents a nested browsing context, embedding another HTML page into the current one.
- The `<object>` HTML element represents an external resource, which can be treated as an image, a nested browsing
  context, or a resource to be handled by a plugin.
- The `<param>` HTML element defines parameters for an object element.
- The `<picture>` HTML element contains zero or more source elements and one img element to offer alternative versions
  of an image for different display/device scenarios.
- The `<portal>` HTML element enables the embedding of another HTML page into the current one for the purposes of
  allowing smoother navigation into new pages.
- The `<source>` HTML element specifies multiple media resources for the picture, the audio element, or the video
  element. It is an empty element, meaning that it has no content and does not have a closing tag. It is commonly used
  to offer the same media content in multiple file formats in order to provide compatibility with a broad range of
  browsers given their differing support for image file formats and media file formats.

## Tables

- [MDN](https://developer.mozilla.org/en-US/docs/Learn/HTML/Tables)

### Adding a caption

- [MDN](https://developer.mozilla.org/en-US/docs/Learn/HTML/Tables/Advanced#adding_a_caption_to_your_table_with_caption)

You can give your table a caption by putting it inside a `<caption>` element and nesting that inside the `<table>`
element. The caption is meant to contain a description of the table contents. The summary attribute can also be used on
the `<table>` element to provide a description. We'd recommend using the `<caption>` element instead.

### Adding a structure

`<thead>`, `<tfoot>`, and `<tbody>` elements don't make the table any more accessible to screenreader users, and don't
result in any visual enhancement on their own. They are however very useful for styling and layout.

### Providing common styling to columns

- [MDN](https://developer.mozilla.org/en-US/docs/Learn/HTML/Tables/Basics#providing_common_styling_to_columns)

HTML has a method of defining styling information for an entire column of data all in one place - the `<col>` and
`<colgroup>` elements.

## Forms

- [MDN](https://developer.mozilla.org/en-US/docs/Learn/Forms)

The `<form>` element formally defines a form and attributes that determine the form's behavior.

### Form element

- [MDN](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/form)

- The `action` attribute defines the location (URL) where the form's collected data should be sent when it is submitted.
- The `method` attribute defines which HTTP method to send the data with (usually get or post).

It is possible to use the `:valid` and `:invalid` CSS pseudo-classes to style a `<form>` element based on whether or not
the elements inside the form are valid.

### Structure

- [MDN](https://developer.mozilla.org/en-US/docs/Learn/Forms/How_to_structure_a_web_form)
- [Fieldset - MDN](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/fieldset)
- [Legend - MDN](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/legend)
- [Label - MDN](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/label)

The `<fieldset>` element is a convenient way to create groups of widgets that share the same purpose, for styling and
semantic purposes.

You can label a `<fieldset>` by including a `<legend>` element just below the opening `<fieldset>` tag. The text content
of the `<legend>` formally describes the purpose of the `<fieldset>` it is included inside.

In addition to the `<fieldset>` element, it's also common practice to use HTML titles (e.g. `<h1>`, `<h2>`) and
sectioning (e.g. `<section>`) to structure complex forms.

With the `<label>` associated correctly with the `<input>` via its `for` attribute (which contains the `<input>`
element's `id` attribute), a screenreader will read out accesibility text. Labels are also clickable.

### Built-in form validation

- [MDN](https://developer.mozilla.org/en-US/docs/Learn/Forms/Form_validation)

Validation attributes:

- `required`: Specifies whether a form field needs to be filled in before the form can be submitted.
- `minlength` and `maxlength`: Specifies the minimum and maximum length of textual data (strings)
- `min` and `max`: Specifies the minimum and maximum values of numerical input types
- `type`: Specifies whether the data needs to be a number, an email address, or some other specific preset type.
- `pattern`: Specifies a regular expression that defines a pattern the entered data needs to follow.

### Input types

- [Basic native form controls - MDN](https://developer.mozilla.org/en-US/docs/Learn/Forms/Basic_native_form_controls)
- [`<input>`: The Input (Form Input) element](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input)

The common input types button, checkbox, file, hidden, image, password, radio, reset, submit, and text.

All basic text controls share some common behaviors:

- They can be marked as `readonly` (the user cannot modify the input value but it is still sent with the rest of the
  form data) or `disabled` (the input value can't be modified and is never sent with the rest of the form data).
- They can have a `placeholder`; this is text that appears inside the text input box that should be used to briefly
  describe the purpose of the box.
- They can be constrained in `size` (the physical size of the box) and `maxlength` (the maximum number of characters
  that can be entered into the box).
- They can benefit from `spell checking` (using the `spellcheck` attribute), if the browser supports it.

Common attributes:

- autofocus: This Boolean attribute lets you specify that the element should automatically have input focus when the
  page loads.
- disabled: This Boolean attribute indicates that the user cannot interact with the element.
- name: The name of the element; this is submitted with the form data.
- value: The element's initial value.

#### Name attribute

- [MDN](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input#attr-name)

A string specifying a name for the input control. This name is submitted along with the control's value when the form
data is submitted.

Consider the name a required attribute (even though it's not). If an input has no name specified, or name is empty, the
input's value is not submitted with the form! (Disabled controls, unchecked radio buttons, unchecked checkboxes, and
reset buttons are also not sent.)

Only one radio button in a same-named group of radio buttons can be checked at a time.

#### Buttons

- [MDN](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/button)

- submit: Sends the form data to the server. For `<button>` elements, omitting the type attribute (or an invalid value
  of type) results in a submit button.
- reset: Resets all form widgets to their default values. Not good for UX.
- button: Buttons that have no automatic effect but can be customized using JavaScript code.

#### Hidden content

- [MDN](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input/hidden)

Another original text control is the `hidden` input type. This is used to create a form control that is invisible to the
user, but is still sent to the server along with the rest of the form data once submitted - for example you might want
to submit a timestamp to the server stating when an order was placed.

#### Required fields

- [Multiple labels, required - MDN](https://developer.mozilla.org/en-US/docs/Learn/Forms/How_to_structure_a_web_form#multiple_labels)

Marking input required:

```html
<label for="username">Name: <abbr title="required" aria-label="required">*</abbr></label>
<input id="username" type="text" name="username" />
```

### Submitting

- [MDN](https://developer.mozilla.org/en-US/docs/Learn/Forms/Sending_and_retrieving_form_data)
- [Button - MDN](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/button)

Use `<button type="submit">`. You can also use the `<input>` element with the corresponding type to produce a button,
for example `<input type="submit">`. The main advantage of the `<button>` element is that the `<input>` element only
allows plain text in its label whereas the `<button>` element allows full HTML content, allowing more complex, creative
button content.

### Styling with pseudo classes

- [MDN](https://developer.mozilla.org/en-US/docs/Learn/Forms/UI_pseudo-classes)

- `:hover`: Selects an element only when it is being hovered over by a mouse pointer.
- `:focus`: Selects an element only when it is focused (i.e. by being tabbed to via the keyboard).
- `:active`: selects an element only when it is being activated (i.e. while it is being clicked on, or when the
  Return/Enter key is being pressed down in the case of a keyboard activation).
- `:required` and `:optional`: Targets required or optional form controls.
- `:valid` and `:invalid`, and `:in-range` and `:out-of-range`: Target form controls that are valid/invalid according to
  form validation constraints set on them, or in-range/out-of-range.
- `:enabled` and `:disabled`, and `:read-only` and `:read-write`: Target enabled or disabled form controls (e.g. with
  the disabled HTML attribute set), and read-write or read-only form controls (e.g. with the readonly HTML attribute
  set).
- `:checked`, `:indeterminate`, and `:default`: Respectively target checkboxes and radio buttons that are checked, in an
  indeterminate state (neither checked or not checked), and the default selected option when the page loads (e.g. an
  `<input type="checkbox">` with the checked attribute set, or an `<option>` element with the selected attribute set).

## CORS

- [The crossorigin attribute - MDN](https://developer.mozilla.org/en-US/docs/Web/HTML/Attributes/crossorigin)
- [CORS enables image - MDN](https://developer.mozilla.org/en-US/docs/Web/HTML/CORS_enabled_image)

The crossorigin attribute, valid on the `<audio>`, `<img>`, `<link>`, `<script>`, and `<video>` elements, provides
support for CORS, defining how the element handles crossorigin requests, thereby enabling the configuration of the CORS
requests for the element's fetched data. Depending on the element, the attribute can be a CORS settings attribute.

## Link types: preload

- [MDN](https://developer.mozilla.org/en-US/docs/Web/HTML/Link_types/preload)

The `preload` value of the `<link>` element's `rel` attribute lets you declare fetch requests in the HTML's `<head>`,
specifying resources that your page will need very soon, which you want to start loading early in the page lifecycle,
before browsers' main rendering machinery kicks in. This ensures they are available earlier and are less likely to block
the page's render, improving performance.
