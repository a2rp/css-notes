# 03. Values, units, and colors

[Back to notes index](../README.md)

| Previous | Notes index | Next |
| --- | --- | --- |
| [Previous: Selectors, specificity, and the cascade](./02-selectors-specificity-and-cascade.md) | [Notes index](../README.md) | [Next: The box model and layout flow](./04-box-model-and-layout-flow.md) |

## A property accepts specific value types

Every CSS property has a grammar that describes the values it accepts. For example, `color` accepts colors, `width` accepts lengths and percentages, and `opacity` accepts a number in a range. If a value does not match the property's grammar, the browser ignores that declaration.

```css
.card {
    width: 32rem;
    opacity: 0.96;
    color: rgb(30 41 59);
    border-color: transparent;
}
```

A number and its unit are written together: `24px`, not `24 px`. Zero may be written without a unit for a length, as in `margin: 0`.

## Choose a unit based on what should scale

| Unit | Relative to | Common use |
| --- | --- | --- |
| `px` | A CSS pixel | Thin borders and precise small details |
| `rem` | The root element's font size | Type scales, spacing, and component dimensions |
| `em` | The element's font size, or parent size when setting font size | Local sizing tied to text |
| `%` | A property-specific containing size | Flexible widths and proportional values |
| `vw`, `vh` | The viewport width or height | Viewport-aware sizing |
| `svh`, `lvh`, `dvh` | Small, large, or dynamic viewport height | Mobile viewport-aware sections |
| `ch` | The width of the zero glyph in the current font | Text measure and form fields |
| `cqi`, `cqw` | A query container's inline size or width | Reusable components sized by their container |

Use `rem` for values that should respond to the user's root text size. Use `em` when a component's internal spacing should grow with its text. Use percentages when the design is proportional to a containing block, but check the property's definition because the reference differs by property.

Viewport height can change as mobile browser controls appear and disappear. The newer `svh`, `lvh`, and `dvh` units describe small, large, and dynamic viewport sizes. A fallback can help older browsers:

```css
.hero {
    min-height: 100vh;
    min-height: 100svh;
}
```

## Use fluid values with boundaries

`calc()` combines values in a supported expression. `min()` chooses the smallest argument, `max()` chooses the largest, and `clamp()` keeps a value between a minimum and maximum:

```css
.page {
    width: min(100% - 2rem, 72rem);
    margin-inline: auto;
}

h1 {
    font-size: clamp(2rem, 1.2rem + 3vw, 4rem);
}
```

The heading can grow with the viewport but cannot become smaller than `2rem` or larger than `4rem`. Fluid sizing works best when it preserves readable limits. Do not use viewport units alone for body text because the text could become too small or too large.

For a component that should adapt to its own width instead of the whole browser window, define a container and use a container query unit:

```css
.card-list {
    container-type: inline-size;
}

.card {
    padding: clamp(1rem, 4cqi, 2rem);
}
```

Here `cqi` is a percentage of the query container's inline size. Container query units are most useful when a component appears in different layout regions.

## Common color formats

CSS supports named colors, hexadecimal notation, RGB, HSL, and newer perceptual color spaces such as OKLCH:

```css
.palette {
    color: darkslategray;
    border-color: #475569;
    background-color: rgb(248 250 252);
}

.button {
    background-color: hsl(205 75% 32%);
    color: oklch(98% 0.01 250);
}
```

Hex colors can use three or six digits, with an optional alpha component in four or eight digit forms. RGB describes red, green, and blue channels. HSL describes hue, saturation, and lightness. OKLCH describes perceived lightness, chroma, and hue, which can make it easier to adjust a palette consistently. Check browser support when a project has to support older browsers.

Use the same format consistently within a palette and name repeated colors with custom properties:

```css
:root {
    --color-text: #172033;
    --color-muted: #475569;
    --color-surface: #ffffff;
    --color-accent: #075985;
}
```

The custom property chapter covers reusable values in more depth.

## Unitless values

Some properties accept numbers without units. For example, `line-height: 1.5` is a multiplier of the element's font size. It is often better than a fixed pixel line height because it scales with text:

```css
.article {
    font-size: 1rem;
    line-height: 1.65;
}
```

Other common unitless values include `font-weight: 600`, `opacity: 0.5`, and `z-index: 2`. Check the property reference instead of assuming a unit is required.

## Try it

1. Set a content column to a maximum width in `rem` or `ch`.
2. Add horizontal padding that remains at least `1rem` on narrow screens.
3. Change a heading from a fixed size to `clamp()`.
4. Resize the browser and check the smallest and largest values.
5. Replace one repeated color with a custom property.

## Common mistakes

- Adding a space between a number and its unit.
- Using `em` without accounting for nested font-size inheritance.
- Assuming a percentage always refers to the parent's width.
- Using only `100vh` for a mobile full-height section.
- Making body text depend entirely on viewport width.
- Assuming a color with a similar hue has the same contrast.
- Using an advanced color function without checking the project's browser support.

## Official references

- [CSS values and units](https://developer.mozilla.org/en-US/docs/Web/CSS/Guides/Values_and_units)
- [The length type](https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Values/length)
- [Numeric data types](https://developer.mozilla.org/en-US/docs/Web/CSS/Guides/Values_and_units/Numeric_data_types)
- [CSS color values](https://developer.mozilla.org/en-US/docs/Web/CSS/ color_value)
- [Container queries](https://developer.mozilla.org/en-US/docs/Web/CSS/Guides/Containment/Container_queries)

| Previous | Notes index | Next |
| --- | --- | --- |
| [Previous: Selectors, specificity, and the cascade](./02-selectors-specificity-and-cascade.md) | [Notes index](../README.md) | [Next: The box model and layout flow](./04-box-model-and-layout-flow.md) |
