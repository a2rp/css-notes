# 08. Grid layout

[Back to notes index](../README.md)

| Previous | Notes index | Next |
| --- | --- | --- |
| [Previous: Flexbox layout](./07-flexbox-layout.md) | [Notes index](../README.md) | [Next: Positioning and stacking context](./09-positioning-and-stacking-context.md) |

## Use Grid for two-dimensional layout

CSS Grid controls rows and columns together. Use it for page structure, dashboards, image galleries, and card collections where items should line up in both dimensions. Flexbox is usually simpler for a single row or column.

Set `display: grid` on the parent. Its direct children become grid items:

```css
.card-grid {
    display: grid;
    grid-template-columns: repeat(3, minmax(0, 1fr));
    gap: 1rem;
}
```

The three equal columns are tracks. `1fr` distributes a share of remaining space after fixed and intrinsic sizes are considered. `minmax(0, 1fr)` gives each track a zero minimum so long content does not force a column wider than its share. Put `min-width: 0` on an item when its own min-content size still causes overflow.

## Make a responsive grid

The `repeat()` function can create as many columns as fit a minimum size:

```css
.card-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(min(100%, 16rem), 1fr));
    gap: 1rem;
}
```

The grid keeps columns at least 16rem when space allows and shares available space among them. The `min(100%, 16rem)` part prevents a minimum track wider than a very narrow container.

`auto-fit` collapses empty repeated tracks after items are placed, allowing existing columns to expand. `auto-fill` keeps the empty tracks in the layout, reserving their space. For a common card collection where the visible cards should use all available width, `auto-fit` is often convenient.

## Define tracks and gaps

`grid-template-columns` and `grid-template-rows` define the explicit grid. Track sizes can use fixed lengths, percentages, intrinsic keywords, `fr`, and sizing functions such as `minmax()`.

```css
.dashboard {
    display: grid;
    grid-template-columns: minmax(14rem, 1fr) 3fr;
    grid-template-rows: auto 1fr auto;
    gap: 1rem 1.5rem;
}
```

The first `gap` value sets row spacing and the second sets column spacing. Use `row-gap`, `column-gap`, or the `gap` shorthand to adjust them.

Items placed beyond the explicit tracks create implicit tracks. Give implicit tracks a size when the default is not suitable:

```css
.gallery {
    display: grid;
    grid-template-columns: repeat(4, minmax(0, 1fr));
    grid-auto-rows: minmax(8rem, auto);
}
```

## Place items by lines or named areas

Grid lines are numbered from the start edge. An item can span a range of columns:

```css
.featured-card {
    grid-column: span 2;
}
```

Named areas describe the larger layout in a readable way:

```css
.page-layout {
    display: grid;
    grid-template-columns: minmax(0, 1fr) 18rem;
    grid-template-areas:
        "header header"
        "main sidebar"
        "footer footer";
    gap: 1rem;
}

.page-header { grid-area: header; }
.page-main { grid-area: main; }
.page-sidebar { grid-area: sidebar; }
.page-footer { grid-area: footer; }
```

Each row string describes one row, and each name must form a rectangle in the grid. A period marks an empty cell. The named area belongs to the grid container; items opt into an area with `grid-area`.

Change the template at a breakpoint while preserving the same semantic source order:

```css
@media (max-width: 48rem) {
    .page-layout {
        grid-template-columns: minmax(0, 1fr);
        grid-template-areas:
            "header"
            "main"
            "sidebar"
            "footer";
    }
}
```

CSS placement changes visual layout, not screen-reader reading order. Keep HTML order sensible and avoid using Grid to create a misleading sequence.

## Align grid items

Grid uses the shared box-alignment properties:

- `justify-items` aligns items inside their grid areas along the inline axis.
- `align-items` aligns items along the block axis.
- `justify-content` and `align-content` align the entire grid when it is smaller than its container.
- `place-items` combines `align-items` and `justify-items`.

Use `stretch`, `start`, `end`, or `center` based on the content. The default alignment often stretches items to fill their grid areas.

## Try it

1. Create a three-column grid with `repeat(3, 1fr)`.
2. Add `minmax()` and replace the fixed count with `auto-fit`.
3. Add a long URL to a card and test for overflow.
4. Place one card across two columns.
5. Rebuild a header, main area, sidebar, and footer with named areas, then stack them at a narrow width.

## Common mistakes

- Using `1fr` without considering a long min-content item.
- Creating columns with percentages plus gaps that exceed the container.
- Expecting `auto-fit` and `auto-fill` to behave identically when there are empty tracks.
- Leaving implicit rows with an unexpectedly small or large size.
- Giving an area name a non-rectangular shape.
- Visually reordering important content away from its HTML reading order.
- Choosing Grid for a simple one-dimensional row that Flexbox can express more clearly.

## Official references

- [CSS Grid layout](https://developer.mozilla.org/en-US/docs/Learn_web_development/Core/CSS_layout/Grids)
- [Basic concepts of Grid layout](https://developer.mozilla.org/en-US/docs/Web/CSS/Guides/Grid_layout/Basic_concepts)
- [Grid template areas](https://developer.mozilla.org/en-US/docs/Web/CSS/Guides/Grid_layout/Grid_template_areas)
- [Grid auto-placement](https://developer.mozilla.org/en-US/docs/Web/CSS/Guides/Grid_layout/Auto-placement)
- [The `repeat()` function](https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Values/repeat)

| Previous | Notes index | Next |
| --- | --- | --- |
| [Previous: Flexbox layout](./07-flexbox-layout.md) | [Notes index](../README.md) | [Next: Positioning and stacking context](./09-positioning-and-stacking-context.md) |
