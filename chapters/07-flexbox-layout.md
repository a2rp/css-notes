# 07. Flexbox layout

[Back to notes index](../README.md)

| Previous | Notes index | Next |
| --- | --- | --- |
| [Previous: Backgrounds, borders, and shadows](./06-backgrounds-borders-and-shadows.md) | [Notes index](../README.md) | [Next: Grid layout](./08-grid-layout.md) |

## Use Flexbox for one-dimensional layout

Flexbox arranges direct children along one main axis, either a row or a column. It is useful for navigation bars, toolbars, button groups, centered content, and rows of cards that may wrap.

Set `display: flex` on the parent. Its direct children become flex items:

```html
<nav class="site-nav" aria-label="Main navigation">
    <a class="site-nav__brand" href="/">Study notes</a>
    <div class="site-nav__links">
        <a href="/css">CSS</a>
        <a href="/html">HTML</a>
        <a href="/javascript">JavaScript</a>
    </div>
</nav>
```

```css
.site-nav {
    display: flex;
    align-items: center;
    justify-content: space-between;
    gap: 1rem;
    padding: 1rem;
}

.site-nav__links {
    display: flex;
    flex-wrap: wrap;
    gap: 0.75rem 1rem;
}
```

## Understand the axes

The main axis follows `flex-direction`. In a row, it runs in the inline direction. In a column, it runs in the block direction. The cross axis is perpendicular to the main axis.

- `justify-content` distributes or aligns items along the main axis.
- `align-items` aligns items along the cross axis.
- `align-self` changes cross-axis alignment for one item.
- `align-content` aligns multiple flex lines when wrapping creates extra cross-axis space.
- `gap` sets space between items and flex lines.

Because the axes depend on direction and writing mode, avoid memorizing `justify-content` as always horizontal. Ask which axis is main for the current `flex-direction`.

## Direction and wrapping

The default direction is `row`. Use `column` when items should stack. Reversed directions change visual order without changing the order for screen readers or keyboard focus, so avoid them when visual and reading order must match.

Flex items stay on one line by default. They can wrap when the parent has `flex-wrap: wrap`:

```css
.card-list {
    display: flex;
    flex-wrap: wrap;
    gap: 1rem;
}

.card {
    flex: 1 1 16rem;
}
```

Each card begins around 16rem, can grow to use available space, and can shrink when needed. The exact result depends on free space and the other items. Use Grid when the layout needs rows and columns to line up as a two-dimensional system.

## Grow, shrink, and basis

The `flex` shorthand combines three values:

```css
.sidebar {
    flex: 0 0 16rem;
}

.main-content {
    flex: 1 1 0;
    min-width: 0;
}
```

- `flex-grow` distributes positive free space.
- `flex-shrink` controls how items surrender space when the row is too small.
- `flex-basis` provides the initial main size before free space is distributed.

The shorthand `flex: 1` is a common equal-growth pattern, but its basis is zero-like and its items do not necessarily behave like their intrinsic content widths. Use `flex-basis` or a width constraint when the initial size matters.

Flex items have an automatic minimum size based on their content in many situations. A long word or wide child may keep an item from shrinking. `min-width: 0` or `min-height: 0` can allow the item to fit, while the content itself still needs a safe wrapping or overflow rule.

## Align a group and a single item

```css
.toolbar {
    display: flex;
    align-items: center;
    justify-content: space-between;
    gap: 1rem;
}

.toolbar__actions {
    display: flex;
    align-items: center;
    gap: 0.5rem;
}
```

Use `justify-content: center` to center a group along the main axis. Use `margin-inline-start: auto` on one item when it should take up the remaining inline space:

```css
.toolbar__account {
    margin-inline-start: auto;
}
```

Margins can be easier than choosing `space-between` when only one item should move away from the rest.

## Try it

1. Make a row of three items with different text lengths.
2. Toggle `flex-wrap` and resize the browser.
3. Change `flex-direction` to `column` and observe which axis each alignment property affects.
4. Give one item a long URL and test `min-width: 0` with `overflow-wrap`.
5. Replace `space-between` with `gap` and compare the edge spacing.

## Common mistakes

- Setting `justify-content` when you meant to align on the cross axis.
- Forgetting that the axes rotate when `flex-direction` changes.
- Using `align-content` on a single line and expecting it to move the items.
- Reordering important content visually while leaving a confusing reading order.
- Expecting flex items to wrap without enabling `flex-wrap`.
- Using percentage widths and gaps that add up to more than the available width.
- Choosing Flexbox for a layout whose rows and columns need to align independently.

## Official references

- [CSS flexible box layout](https://developer.mozilla.org/en-US/docs/Web/CSS/Guides/Flexible_box_layout)
- [Basic concepts of Flexbox](https://developer.mozilla.org/en-US/docs/Web/CSS/Guides/Flexible_box_layout/Basic_concepts)
- [Aligning items in a flex container](https://developer.mozilla.org/en-US/docs/Web/CSS/Guides/Flexible_box_layout/Aligning_items)
- [Controlling flex item ratios](https://developer.mozilla.org/en-US/docs/Web/CSS/Guides/Flexible_box_layout/Controlling_flex_item_ratios)
- [Wrapping flex items](https://developer.mozilla.org/en-US/docs/Web/CSS/Guides/Flexible_box_layout/Wrapping_items)

| Previous | Notes index | Next |
| --- | --- | --- |
| [Previous: Backgrounds, borders, and shadows](./06-backgrounds-borders-and-shadows.md) | [Notes index](../README.md) | [Next: Grid layout](./08-grid-layout.md) |
