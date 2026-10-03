# 09. Positioning and stacking context

[Back to notes index](../README.md)

| Previous | Notes index | Next |
| --- | --- | --- |
| [Previous: Grid layout](./08-grid-layout.md) | [Notes index](../README.md) | [Next: Responsive design and media queries](./10-responsive-design-and-media-queries.md) |

## Position elements with a clear purpose

The `position` property changes how an element is placed relative to normal document flow or to another reference box.

| Value | Behavior |
| --- | --- |
| `static` | Default normal-flow placement; inset offsets do not apply |
| `relative` | Stays in flow and can be offset from its normal position |
| `absolute` | Removed from normal flow and positioned within a containing block |
| `fixed` | Removed from normal flow and usually positioned relative to the viewport |
| `sticky` | Stays in flow until it reaches an inset threshold in its scroll container |

Positioned layout is useful for small local overlaps, badges, sticky headings, and fixed controls. Use Flexbox or Grid for the main page layout.

## Use relative positioning as an anchor

A relatively positioned element keeps its original layout space. Its visual box can be offset without moving neighboring items. It also commonly establishes a containing block for an absolutely positioned child:

```html
<article class="card">
    <span class="card__badge">New</span>
    <h2>CSS layout notes</h2>
</article>
```

```css
.card {
    position: relative;
    padding: 1.5rem;
    border: 1px solid #cbd5e1;
}

.card__badge {
    position: absolute;
    inset-block-start: 0.75rem;
    inset-inline-end: 0.75rem;
}
```

The badge is positioned relative to the card's padding box. Inset properties such as `inset-block-start` and `inset-inline-end` express logical directions. Physical `top`, `right`, `bottom`, and `left` are also available.

## Absolute and fixed elements leave normal flow

An absolutely positioned item does not reserve space where it appears. Other content lays out as if the item were absent. Its containing block is usually the nearest ancestor that establishes one, often a positioned ancestor. If there is no such ancestor, it uses the initial containing block.

A fixed item is usually positioned relative to the viewport and stays there while the document scrolls. Transforms and some containment properties on ancestors can establish a containing block for fixed descendants, changing the expected reference.

Use a fixed element carefully. It can cover content at high zoom or on a short screen. Provide enough page space for fixed headers or controls, and ensure keyboard focus is not hidden underneath them.

## Sticky elements need a threshold

A sticky item behaves like a relatively positioned item until it reaches the configured inset threshold. At least one inset value on the relevant axis must be non-auto:

```css
.section-nav {
    position: sticky;
    inset-block-start: 0;
    z-index: 10;
    background: white;
}
```

Sticky positioning is constrained by its containing block and follows the nearest ancestor with a scrolling mechanism. An ancestor with `overflow: hidden`, `auto`, or `scroll` can change which container the sticky element follows, even if that ancestor is not the one visibly scrolling. Check ancestor overflow when a sticky header does not stick to the viewport as expected.

## Understand stacking contexts

The `z-index` property sets a stack level within a stacking context. A larger number does not necessarily place an element above every element on the page. A child cannot escape the stacking order of its parent context.

A stacking context can be created by the root element, positioned elements with a non-auto `z-index`, fixed or sticky positioning, opacity below one, transforms, filters, isolation, and other properties. The exact rules depend on the property.

```css
.page-header {
    position: sticky;
    inset-block-start: 0;
    z-index: 20;
}

.card {
    position: relative;
    z-index: 1;
}

.card__menu {
    position: absolute;
    z-index: 2;
}
```

Keep a small, intentional scale for interface layers, such as base content, sticky navigation, popovers, and dialogs. When a large z-index does not work, inspect the ancestors for stacking contexts instead of increasing the number without limit.

## Try it

1. Add a badge to a card using a relative parent and absolute child.
2. Add a sticky navigation bar and give it a non-auto inset.
3. Put an overflow value on a parent and observe how the sticky behavior changes.
4. Set `opacity: 0.9` on one parent and test the stacking of its child.
5. Remove `position: relative` from the card and see which containing block the badge uses.

## Common mistakes

- Positioning a child absolutely without establishing the intended containing block.
- Expecting an absolute element to reserve space in normal flow.
- Using `z-index` as if all elements belonged to one global stack.
- Forgetting that opacity and transforms can create stacking contexts.
- Setting sticky positioning without a non-auto inset.
- Adding overflow to an ancestor and unintentionally changing sticky behavior.
- Fixing the main layout with offsets instead of Grid or Flexbox.

## Official references

- [Positioning](https://developer.mozilla.org/en-US/docs/Learn_web_development/Core/CSS_layout/Positioning)
- [The `position` property](https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Properties/position)
- [Layout and the containing block](https://developer.mozilla.org/en-US/docs/Web/CSS/Guides/Display/Containing_block)
- [Stacking context](https://developer.mozilla.org/en-US/docs/Web/CSS/Guides/Positioned_layout/Stacking_context)
- [Understanding `z-index`](https://developer.mozilla.org/en-US/docs/Web/CSS/Guides/Positioned_layout/Understanding_z-index)

| Previous | Notes index | Next |
| --- | --- | --- |
| [Previous: Grid layout](./08-grid-layout.md) | [Notes index](../README.md) | [Next: Responsive design and media queries](./10-responsive-design-and-media-queries.md) |
