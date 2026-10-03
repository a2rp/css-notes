# 04. The box model and layout flow

[Back to notes index](../README.md)

| Previous | Notes index | Next |
| --- | --- | --- |
| [Previous: Values, units, and colors](./03-values-units-and-colors.md) | [Notes index](../README.md) | [Next: Typography and text](./05-typography-and-text.md) |

## Every element has a box

The box model describes the space around an element's content:

1. Content holds text, images, or child elements.
2. Padding is inside the border and surrounds the content.
3. Border surrounds padding and content.
4. Margin is outside the border and separates the box from neighbors.

With the default `content-box` sizing, `width` sets only the content width. A 300px content box with 20px padding on each side and 2px borders is 344px wide:

`300 + 20 + 20 + 2 + 2 = 344`

This can make columns wider than expected.

## Prefer border-box sizing

With `box-sizing: border-box`, the declared width includes content, padding, and border. A common reset applies this sizing to every element and its pseudo-elements:

```css
*,
*::before,
*::after {
    box-sizing: border-box;
}

.card {
    width: 20rem;
    padding: 1.25rem;
    border: 2px solid #94a3b8;
}
```

The card remains 20rem wide. Its content area becomes smaller to make room for padding and border. Margins are still outside the declared width.

Use `min-width`, `max-width`, `min-height`, and `max-height` when an element needs boundaries rather than a rigid size. A content column often works well with a maximum width and fluid available space:

```css
.article {
    width: min(100% - 2rem, 68ch);
    margin-inline: auto;
}
```

## Normal flow places block and inline boxes

Normal flow is the browser's default layout. Block boxes generally start on a new line and stack along the block direction. Inline boxes participate in a line of text and wrap with it.

| Display value | Typical behavior |
| --- | --- |
| `block` | Starts on a new line and accepts width and height |
| `inline` | Flows within text; width and height do not apply in the usual way |
| `inline-block` | Flows inline while accepting width and height |
| `none` | Removes the element and its layout space |
| `flow-root` | Creates a block box with a new formatting context |

Semantic elements have browser defaults. Headings and paragraphs are block-level by default; links and spans are inline by default. CSS can change the display type, but semantic HTML should still describe the content's role.

```css
.tag {
    display: inline-block;
    padding: 0.25rem 0.6rem;
    border: 1px solid currentColor;
    border-radius: 999px;
}

[hidden] {
    display: none;
}
```

`visibility: hidden` hides an element but keeps its space in the layout. `display: none` removes its box from layout. Choose based on the intended behavior.

## Margin and padding do different work

Padding adds space inside the border. It enlarges the clickable or colored area of an element. Margin adds space outside the border and separates neighboring boxes.

Vertical margins between some adjacent block boxes can collapse. When a 32px bottom margin meets a 20px top margin, the visible gap is usually 32px rather than 52px. Horizontal margins do not collapse this way.

Margin collapsing can also happen between a parent and its first or last in-flow child. If that behavior is surprising, inspect the box model in developer tools or establish a formatting context intentionally, for example with `display: flow-root`. Avoid adding arbitrary padding just to hide an unexplained collapse.

## Control overflow deliberately

Overflow occurs when content is larger than the box that contains it. The default `visible` value lets content extend outside. `auto` allows scrolling when needed, while `hidden` clips content and can still allow programmatic scrolling. `clip` clips content without creating a scroll container.

```css
.code-example {
    max-width: 100%;
    overflow: auto;
}

.avatar {
    width: 4rem;
    aspect-ratio: 1;
    overflow: clip;
    border-radius: 50%;
}
```

Avoid setting a fixed height on text containers unless overflow is handled. Users may increase text size, translate the content, or use a narrow viewport.

## Use logical properties for writing direction

Physical properties such as `margin-left` name a screen edge. Logical properties describe the writing direction: `margin-inline-start` means the start side of the inline direction, and `padding-block` affects the block direction.

```css
.page-section {
    padding-block: 2rem;
    padding-inline: 1rem;
    border-inline-start: 0.25rem solid #0f766e;
}
```

Logical properties work more naturally with right-to-left text and vertical writing modes. They also describe layout intent more clearly in many components.

## Inspect the box model

Select an element in browser developer tools and inspect its computed styles. The box model diagram shows content, padding, border, and margin. Change a declaration temporarily in the Styles panel and observe the page before changing the source file.

## Try it

1. Add a fixed width, padding, and border to a box.
2. Compare its rendered size with `content-box` and `border-box`.
3. Add paragraphs with different vertical margins and observe the gap.
4. Put long text inside a fixed-width box and try `overflow: auto`.
5. Change physical margins to logical inline and block properties.

## Common mistakes

- Forgetting that padding and border add to a `content-box` width.
- Using margin when the background should extend behind the space.
- Expecting an inline element to obey width and height like a block.
- Setting a fixed height that clips larger text.
- Assuming adjacent vertical margins always add together.
- Using `overflow: hidden` as a general fix without checking clipped focus rings or content.
- Treating `display: none` and `visibility: hidden` as identical.

## Official references

- [The box model](https://developer.mozilla.org/en-US/docs/Learn_web_development/Core/Styling_basics/Box_model)
- [CSS box model](https://developer.mozilla.org/en-US/docs/Web/CSS/Guides/Box_model)
- [Block and inline layout in normal flow](https://developer.mozilla.org/en-US/docs/Web/CSS/Guides/Display/Block_and_inline_layout)
- [Flow layout and overflow](https://developer.mozilla.org/en-US/docs/Web/CSS/Guides/Display/Flow_layout_and_overflow)
- [The `box-sizing` property](https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Properties/box-sizing)

| Previous | Notes index | Next |
| --- | --- | --- |
| [Previous: Values, units, and colors](./03-values-units-and-colors.md) | [Notes index](../README.md) | [Next: Typography and text](./05-typography-and-text.md) |
