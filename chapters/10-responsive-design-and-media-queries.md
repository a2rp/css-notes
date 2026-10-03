# 10. Responsive design and media queries

[Back to notes index](../README.md)

| Previous | Notes index | Next |
| --- | --- | --- |
| [Previous: Positioning and stacking context](./09-positioning-and-stacking-context.md) | [Notes index](../README.md) | [Next: Pseudo-classes, pseudo-elements, and forms](./11-pseudo-classes-elements-and-forms.md) |

## Build flexible layouts first

Responsive design lets content adapt to the space and capabilities available. Start with semantic HTML, fluid widths, flexible images, and Grid or Flexbox. Add a breakpoint when the content needs a different arrangement, not just because a particular device has a familiar width.

The viewport meta element tells mobile browsers to use the device width for layout:

```html
<meta name="viewport" content="width=device-width, initial-scale=1">
```

Without it, a phone may render a wide virtual page and scale it down, making text and controls unnecessarily small.

A fluid content column can fit narrow screens and stop growing on wide ones:

```css
.page {
    width: min(100% - 2rem, 72rem);
    margin-inline: auto;
}

img,
video {
    max-width: 100%;
    height: auto;
}
```

## Add a breakpoint where content needs it

A media query applies rules when a condition matches. A mobile-first layout starts with the simplest narrow-screen arrangement, then adds columns when there is enough room:

```css
.article-layout {
    display: grid;
    grid-template-columns: minmax(0, 1fr);
    gap: 2rem;
}

@media (min-width: 52rem) {
    .article-layout {
        grid-template-columns: minmax(0, 1fr) 18rem;
    }
}
```

The breakpoint is based on when the article and sidebar fit comfortably. It is not tied to a brand or device model. Resize the page continuously and adjust the breakpoint where the content starts to feel crowded.

Media queries can also respond to print, orientation, color scheme, pointer capabilities, and user preferences. Use a feature query when the design truly needs to adapt to that condition.

## Use intrinsic layout before more breakpoints

Grid can create as many columns as fit without a viewport query:

```css
.resource-list {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(min(100%, 17rem), 1fr));
    gap: 1rem;
}
```

This pattern responds to the space available in the grid container. Use a media query when the overall page arrangement changes, and intrinsic sizing when repeated items can naturally flow into available space.

## Use container queries for reusable components

A media query responds to the viewport. A container query responds to a named or nearest eligible container, so a component can adapt to its own allocated width:

```css
.profile-card-list {
    container-type: inline-size;
}

.profile-card {
    display: grid;
    gap: 1rem;
}

@container (min-width: 34rem) {
    .profile-card {
        grid-template-columns: 8rem minmax(0, 1fr);
        align-items: center;
    }
}
```

The query changes the card based on the width of the container that establishes the query context. Container queries are useful for components reused in sidebars, main columns, and standalone pages. Use viewport media queries for page-level changes.

## Respect print and motion preferences

Print styles can remove controls and preserve readable contrast:

```css
@media print {
    nav,
    .screen-only {
        display: none;
    }

    body {
        color: black;
        background: white;
    }

    a {
        color: inherit;
        text-decoration: underline;
    }
}
```

For motion-related changes, respond to the user's reduced-motion preference. The animation chapter covers a full example. Media queries can also adapt a transition:

```css
.card {
    transition: transform 160ms ease;
}

@media (prefers-reduced-motion: reduce) {
    .card {
        transition: none;
    }
}
```

Do not remove content or functionality based only on a media query for screen width. A narrow viewport does not mean the user has a different input device or fewer needs.

## Test responsive behavior

- Resize the browser gradually instead of checking only a few named device sizes.
- Test long headings, URLs, labels, and translated text.
- Check browser zoom and increased text size.
- Use keyboard navigation at narrow and wide widths.
- Inspect horizontal scrolling and clipped focus outlines.
- Test print output if people need a paper or PDF copy.
- Use developer tools to inspect media query and container query matches.

## Common mistakes

- Designing to specific phone and tablet models instead of content needs.
- Hiding useful content because the screen is narrow.
- Setting fixed widths that overflow a small viewport.
- Relying only on a media query when an intrinsic Grid pattern is enough.
- Using a container query without creating an eligible query container.
- Forgetting viewport metadata in the HTML head.
- Testing only at one viewport size or browser zoom level.

## Official references

- [Responsive web design](https://developer.mozilla.org/en-US/docs/Learn_web_development/Core/CSS_layout/Responsive_Design)
- [Media query fundamentals](https://developer.mozilla.org/en-US/docs/Learn_web_development/Core/CSS_layout/Media_queries)
- [CSS media queries](https://developer.mozilla.org/en-US/docs/Web/CSS/Guides/Media_queries)
- [Container queries](https://developer.mozilla.org/en-US/docs/Web/CSS/Guides/Containment/Container_queries)
- [The `prefers-reduced-motion` media feature](https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/At-rules/%40media/prefers-reduced-motion)

| Previous | Notes index | Next |
| --- | --- | --- |
| [Previous: Positioning and stacking context](./09-positioning-and-stacking-context.md) | [Notes index](../README.md) | [Next: Pseudo-classes, pseudo-elements, and forms](./11-pseudo-classes-elements-and-forms.md) |
