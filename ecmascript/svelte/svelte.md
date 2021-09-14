# Svelte

Svelte converts your app into ideal JavaScript at build time, rather than interpreting your application code at run
time. 

## Reactive declarations

Some parts of a component's state need to be computed from other parts, and recomputed whenever they change. For these,
we have reactive declarations. They look like this:

let count = 0; \ $: doubled = count * 2;

We're not limited to declaring reactive values — we can also run arbitrary statements. 

```js
$: {...}
$: if (...) {}
```

## Props

Pass props to child component:

```js
// App.svelte
<Nested answer={42}/>
```

Mark props with `export let <prop>;` statement in child component. \
```js
// Nested.svelte

<script>

export let answer;

</script>

<p>The answer is {answer}</p>
```

We can specify [default values](https://svelte.dev/tutorial/default-values) and use [spread operator](https://svelte.dev/tutorial/spread-props) for props \

`$$props`:  reference all the props that were passed into a component, not recommended \


Keep in mind: 

```js

// `current` is updated whenever the prop value changes...

export let current;

// ...but `initial` is fixed upon initialisation

const initial = current;

```

## Conditional logic

- `#` character always indicates a block opening tag.
- `/` character always indicates a block closing tag.
- `:` character, as in `{:else}`, indicates a block continuation tag. 


```html
{#if statement}

{:else}

{/if}
```

## Loops

```html
{#each items as item, index}
```

If you prefer, you can use destructuring - `each items as { id, name }`.

[Logic / Keyed each blocks • Svelte Tutorial](https://svelte.dev/tutorial/keyed-each-blocks)

specify a unique identifier for the each block. The (thing.id) tells Svelte how to figure out what changed.

```html
{#each things as thing (thing.id)}

<Thing current={thing.color}/>

{/each}
```

## Async/await

Promise based

```html
{#await promise}

<p>...waiting</p>

{:then number}

<p>The number is {number}</p>

{:catch error}

<p style="color: red">{error.message}</p>

{/await}
```

## Events

You can listen to any event on an element with the on: directive.

```html
<div on:HTMLevent={handleEvent}>
```

### [Events / Event modifiers • Svelte Tutorial](https://svelte.dev/tutorial/event-modifiers)

```html

<button on:click|once={handleClick}>Click me</button>

```

### [Events / Component events • Svelte Tutorial](https://svelte.dev/tutorial/component-events)

Unlike DOM events, component events don't bubble. If you want to listen to an event on some deeply nested component, the
intermediate components must [forward the event](https://svelte.dev/tutorial/event-forwarding).

## @html

render HTML directly into a component. 

```js
<script>

	let string = `this string contains some <strong>HTML!!!</strong>`;

</script>

<p>{@html  string}</p>
```

Svelte doesn't perform any sanitization of the expression inside {@html ...} before it gets inserted into the DOM. In
other words, if you use this feature it's critical that you manually escape HTML that comes from sources you don't
trust, otherwise you risk exposing your users to XSS attacks.

