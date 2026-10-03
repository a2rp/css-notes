# 13. Custom properties and CSS functions

[Back to notes index](../README.md)

| Previous | Notes index | Next |
| --- | --- | --- |
| [Previous: Transforms, transitions, and animations](./12-transforms-transitions-and-animations.md) | [Notes index](../README.md) | [Next: Accessibility and inclusive CSS](./14-accessibility-and-inclusive-css.md) |

## Reuse values with custom properties

Custom properties are declared with names that begin with two hyphens. They participate in the cascade and inheritance, so a component can override a value for its descendants:

```css
:root {
    --color-text: #172033;
    --color-surface: #ffffff;
    --color-accent: #0f766e;
    --space-card: 1.25rem;
    --radius-card: 0.75rem;
}

.card {
    padding: var(--space-card);
    color: var(--color-text);
    background: var(--color-surface);
    border-radius: var(--radius-card);
}

.card--quiet {
    --color-surface: #f1f5f9;
}
```

A property declared on `:root` is available across the document. Names are case-sensitive. Choose names for meaning and use, such as `--color-accent`, rather than where the value happened to appear, such as `--blue-3`.

A custom property can be local to a component when it should vary by instance. Local values inherit to descendants unless registered otherwise.

## Use var() fallbacks

The `var()` function reads a custom property and can provide a fallback when that custom property is unavailable:

```css
.button {
    color: var(--button-text, white);
    background-color: var(--button-background, #0f766e);
    border-color: var(--button-border, currentColor);
}
```

A fallback can itself contain another `var()` call. It is not a type checker for the consuming property. If a custom property exists but expands to a value that is invalid for the property, the browser does not necessarily use the fallback. Keep token values compatible with the properties that consume them.

## Calculate and constrain values

CSS math functions help combine a fixed value with an available size:

```css
.content {
    width: calc(100% - 2rem);
    max-width: 72rem;
    margin-inline: auto;
}

.section {
    padding-inline: clamp(1rem, 4vw, 3rem);
}

.card-grid {
    grid-template-columns: repeat(auto-fit, minmax(min(100%, 16rem), 1fr));
}
```

- `calc()` combines values such as `100% - 2rem`.
- `min()` chooses the smallest expression.
- `max()` chooses the largest expression.
- `clamp(minimum, preferred, maximum)` keeps the preferred value within bounds.

For addition and subtraction, include spaces around the operator. The values need to form a valid type for the property. Use these functions to reduce unnecessary breakpoints, but check extreme viewport sizes and zoom.

## Mix colors with color-mix()

The `color-mix()` function can mix two colors in a chosen color space. It is useful for derived states when the supported color space and browser baseline fit the project:

```css
:root {
    --brand: oklch(52% 0.12 185);
    --brand-soft: color-mix(in oklab, var(--brand), white 82%);
}

.badge {
    color: var(--brand);
    background-color: var(--brand-soft);
}
```

A perceptual space such as Oklab can give more even-looking mixes than simple channel arithmetic. Use a solid fallback before an advanced color expression when older browsers are in scope:

```css
.badge {
    background-color: #e6f2ef;
    background-color: color-mix(in oklab, var(--brand), white 82%);
}
```

The second declaration is ignored when unsupported, leaving the first value in place.

## Register a typed custom property

The `@property` at-rule can specify a syntax, inheritance behavior, and an initial value. This lets the browser understand the type and can allow the property to animate:

```css
@property --progress {
    syntax: "<number>";
    inherits: false;
    initial-value: 0;
}

.progress-bar {
    transform: scaleX(var(--progress));
    transform-origin: left;
}
```

Registered properties are useful for values that need a defined type or interpolation. Use plain custom properties for most design tokens. Check browser support for `@property` when supporting older engines.

## Build a simple theme

A theme can override the values in a scoped selector:

```css
:root {
    color-scheme: light;
    --surface: #ffffff;
    --text: #172033;
}

[data-theme="dark"] {
    color-scheme: dark;
    --surface: #111827;
    --text: #f8fafc;
}

body {
    color: var(--text);
    background-color: var(--surface);
}
```

The `color-scheme` property also informs the browser which built-in control palette is suitable. A theme still needs to check text, borders, focus indicators, and images for sufficient contrast.

## Try it

1. Replace three repeated spacing values with custom properties.
2. Override one token inside a card class and check descendant inheritance.
3. Add a fallback to a custom property, then test the missing-property case.
4. Resize the page and see how `clamp()` behaves at its minimum and maximum.
5. Add the solid color fallback before `color-mix()`.

## Common mistakes

- Creating a token for every one-off value and making the system harder to understand.
- Assuming custom properties are global when they are declared on a local selector.
- Assuming `var()` fallbacks validate the final property value.
- Using incompatible units in a calculation.
- Forgetting operator spacing in `calc()` addition and subtraction.
- Using a new color function without a fallback when older browsers matter.
- Treating a dark theme as only a background and text color change.

## Official references

- [Using CSS custom properties](https://developer.mozilla.org/en-US/docs/Web/CSS/Guides/Cascading_variables/Using_custom_properties)
- [The `var()` function](https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Values/var)
- [CSS math functions](https://developer.mozilla.org/en-US/docs/Web/CSS/Guides/Values_and_units/Using_math_functions)
- [The `clamp()` function](https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Values/clamp)
- [The `color-mix()` function](https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Values/color_value/color-mix)
- [The `@property` at-rule](https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/At-rules/%40property)

| Previous | Notes index | Next |
| --- | --- | --- |
| [Previous: Transforms, transitions, and animations](./12-transforms-transitions-and-animations.md) | [Notes index](../README.md) | [Next: Accessibility and inclusive CSS](./14-accessibility-and-inclusive-css.md) |
