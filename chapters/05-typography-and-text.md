# 05. Typography and text

[Back to notes index](../README.md)

| Previous | Notes index | Next |
| --- | --- | --- |
| [Previous: The box model and layout flow](./04-box-model-and-layout-flow.md) | [Notes index](../README.md) | [Next: Backgrounds, borders, and shadows](./06-backgrounds-borders-and-shadows.md) |

## Start with a readable type system

Typography affects how quickly people can read and understand a page. Begin with a dependable font stack, a comfortable text measure, and line spacing that works at the chosen font size.

```css
:root {
    font-family: system-ui, sans-serif;
    color: #1e293b;
}

body {
    margin: 0;
    font-size: 1rem;
    line-height: 1.6;
}

.article {
    max-width: 68ch;
    margin-inline: auto;
    padding: 2rem 1rem;
}
```

The generic family at the end of the `font-family` list is a fallback. Common families include `serif`, `sans-serif`, `monospace`, and `system-ui`. Quote font names that contain spaces. A user's device may not have a particular font installed, so always provide a useful fallback.

The `ch` unit is based on the width of the zero glyph in the current font. It is a convenient starting point for controlling the line length of text, but the ideal measure depends on the font and content.

## Set size, weight, and line height

Use a consistent scale for headings and body text. A fluid heading can respond to available space while staying within readable limits:

```css
h1 {
    max-width: 18ch;
    margin-block: 0 1rem;
    font-size: clamp(2.25rem, 1.5rem + 3vw, 4rem);
    font-weight: 700;
    line-height: 1.05;
    letter-spacing: -0.03em;
    text-wrap: balance;
}

p {
    max-width: 68ch;
    line-height: 1.65;
}
```

A unitless `line-height` is multiplied by the element's font size and is generally a reliable default. A fixed line-height can become too tight when text size changes. Headings often use a tighter line height than body copy because they are larger.

Use `font-weight` for emphasis rather than simulating bold with color. Use a weight that exists in the selected font; browsers may synthesize a missing weight. If the text must remain readable when fonts fail to load, the fallback family should have a similar character width.

## Use text properties for meaning and hierarchy

`text-align` controls inline alignment inside a block. `text-decoration` draws a line such as an underline, and `text-transform` changes visual capitalization without changing the original text content.

```css
a {
    color: #075985;
    text-decoration-line: underline;
    text-decoration-thickness: 0.08em;
    text-underline-offset: 0.18em;
}

.eyebrow {
    font-size: 0.8rem;
    font-weight: 700;
    letter-spacing: 0.08em;
    text-transform: uppercase;
}
```

Keep the actual heading text meaningful in HTML. Do not rely on `text-transform: uppercase` to provide the only indication that a label is important. Underlines help users recognize links, so avoid removing them unless another clear, consistent visual cue remains.

## Wrap text without hiding content

Most text wraps at spaces. A long URL, identifier, or unbroken string can overflow its container. Use `overflow-wrap` when a long token must be allowed to break:

```css
.message {
    overflow-wrap: anywhere;
}

h2 {
    text-wrap: balance;
}

.article-copy {
    text-wrap: pretty;
}
```

`text-wrap: balance` can improve short headings by distributing words across lines. `text-wrap: pretty` may improve paragraph endings in supported browsers. The default wrapping remains a sensible fallback if a browser does not support those values. Avoid `white-space: nowrap` for content that needs to fit on small screens.

Use `text-overflow: ellipsis` only when truncating content is an intentional interface choice and the complete text remains available in an accessible or discoverable way. It does not create overflow by itself. A one-line ellipsis generally requires a constrained box, `overflow: hidden`, and `white-space: nowrap`.

## Use the font shorthand carefully

The `font` shorthand can set style, weight, size, line height, and family in a compact declaration:

```css
.title {
    font: italic 600 1.25rem / 1.3 system-ui, sans-serif;
}
```

The font size and family are required when using this shorthand. A shorthand resets omitted longhand values to their initial values, so it can unintentionally reset other font settings. Use longhand properties when clarity or partial overrides matter more.

## Provide responsive reading sizes

Respect a user's text zoom and do not lock all text into pixels. Relative sizes such as `rem` allow the type scale to follow the root size. Check at narrow widths, with browser zoom, and with longer translated text.

```css
body {
    font-size: 1rem;
    line-height: 1.6;
}

small,
.caption {
    font-size: 0.875rem;
    line-height: 1.5;
}

h2 {
    font-size: clamp(1.5rem, 1.2rem + 1.2vw, 2.25rem);
}
```

Small text should remain readable and have enough contrast. Do not use spacing or all-capitals as the only way to distinguish a section.

## Try it

1. Try a system font stack and then a serif stack.
2. Change the article width from `90ch` to `65ch`.
3. Increase browser zoom and observe whether line height still feels comfortable.
4. Add `text-wrap: balance` to a multi-line heading.
5. Test a long unbroken URL with `overflow-wrap: anywhere`.

## Common mistakes

- Specifying a single font with no fallback.
- Setting body text to a fixed pixel size that ignores root text scaling.
- Using the same tight line height for body text and large headings.
- Removing link underlines without providing another consistent cue.
- Using `white-space: nowrap` and causing small-screen overflow.
- Using text transformations to change content meaning.
- Truncating important information with an ellipsis.

## Official references

- [Fundamental text and font styling](https://developer.mozilla.org/en-US/docs/Learn_web_development/Core/Text_styling/Fundamentals)
- [The `font-family` property](https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Properties/font-family)
- [The `line-height` property](https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Properties/line-height)
- [The `text-wrap` property](https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Properties/text-wrap)
- [Wrapping and breaking text](https://developer.mozilla.org/en-US/docs/Web/CSS/Guides/Text/Wrapping_breaking_text)

| Previous | Notes index | Next |
| --- | --- | --- |
| [Previous: The box model and layout flow](./04-box-model-and-layout-flow.md) | [Notes index](../README.md) | [Next: Backgrounds, borders, and shadows](./06-backgrounds-borders-and-shadows.md) |
