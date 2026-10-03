# 14. Accessibility and inclusive CSS

[Back to notes index](../README.md)

| Previous | Notes index | Next |
| --- | --- | --- |
| [Previous: Custom properties and CSS functions](./13-custom-properties-and-css-functions.md) | [Notes index](../README.md) | [Next: Debugging, performance, and browser tools](./15-debugging-performance-and-browser-tools.md) |

## CSS can support access, but it cannot replace meaning

CSS can improve contrast, focus visibility, text scaling, layout flexibility, and motion preferences. It cannot make a meaningless document semantic or create keyboard behavior for an element that is not an interactive control. Start with meaningful HTML, then make its presentation work for more people.

Do not hide content, reverse reading order, or communicate an error only through color. Check the page with a keyboard, browser zoom, high contrast settings, and a screen reader when possible.

## Preserve visible keyboard focus

Keyboard users need to see which control has focus. Keep the browser's outline or provide a clear replacement:

```css
:where(a, button, input, select, textarea, summary):focus-visible {
    outline: 3px solid #f97316;
    outline-offset: 3px;
}

section[id],
h2[id] {
    scroll-margin-block-start: 5rem;
}
```

The `:focus-visible` pseudo-class lets browsers decide when a visible focus indicator is appropriate. Do not remove outlines globally. Check that the focus ring is not clipped by `overflow: hidden` or hidden behind a sticky header.

A focus style should be visible against both the control and the surrounding background. Avoid using a thin low-contrast shadow as the only indicator.

## Check text and control contrast

For WCAG 2.2 Level AA, normal text generally needs at least a 4.5:1 contrast ratio against its background. Large text generally needs at least 3:1. Meaningful visual information for user interface components and graphics generally needs at least 3:1 against adjacent colors. Check the actual color pairs, including hover, focus, disabled, error, and placeholder states.

Do not make color the only way to distinguish states. Pair color with text, an icon, an underline, a border, or another clear shape:

```css
.field-error {
    color: #b91c1c;
    border-inline-start: 0.25rem solid currentColor;
    padding-inline-start: 0.75rem;
}

.status--success::before {
    content: "Success: ";
    font-weight: 700;
}
```

The word in the second example is generated content, so a real text label in the HTML is more dependable when the status is essential.

## Let content grow and zoom

Avoid fixed heights on text, navigation, and controls if the content may wrap or users may enlarge it. Use relative units for type and spacing, allow flex and grid items to shrink, and test at high browser zoom:

```css
.notice {
    min-height: 3rem;
    height: auto;
    padding: 0.75rem 1rem;
    overflow-wrap: anywhere;
}

.page {
    width: min(100% - 2rem, 70rem);
    margin-inline: auto;
}
```

Do not disable browser zoom. A layout that uses flexible sizing and natural document flow is more likely to remain usable with larger text or translated content.

## Make controls easy to find and activate

Interactive targets should have enough size and separation. WCAG 2.2 Level AA sets a 24 by 24 CSS pixel minimum target size or spacing exceptions for undersized targets. Larger controls are often easier to use, especially on touchscreens.

```css
.icon-button {
    display: inline-grid;
    min-width: 2.75rem;
    min-height: 2.75rem;
    place-items: center;
    padding: 0.5rem;
}
```

A CSS rule cannot make a decorative span behave like a button. Use a real `<button>` or link for the action so keyboard and assistive technology behavior is present.

## Support forced colors

In forced-colors mode, the browser uses a limited user-selected palette and may override author colors. Let that mode work instead of forcing a brand palette:

```css
@media (forced-colors: active) {
    .icon-button {
        color: ButtonText;
        background: ButtonFace;
        border: 1px solid ButtonText;
    }

    .selected-item {
        outline: 2px solid Highlight;
    }
}
```

System color keywords such as `Canvas`, `CanvasText`, `ButtonFace`, `ButtonText`, and `Highlight` follow the user's selected palette. Avoid `forced-color-adjust: none` unless there is a specific essential visual reason and the result has been carefully tested.

## Honor motion and contrast preferences

Use `prefers-reduced-motion` to remove non-essential movement and transitions. The previous chapter shows a complete motion example. A higher-contrast preference can also be used to strengthen borders or focus indicators where supported:

```css
@media (prefers-contrast: more) {
    .card {
        border: 2px solid currentColor;
    }

    :where(a, button, input):focus-visible {
        outline-width: 4px;
    }
}
```

Always provide a usable base style when a browser does not support a preference query. Do not make an important state available only through animation or a color change.

## Keep visually hidden text available

Sometimes an icon button needs a readable name while its visible label is omitted. Use a visually hidden utility that keeps the text in the accessibility tree:

```css
.visually-hidden:not(:focus, :active) {
    position: absolute;
    width: 1px;
    height: 1px;
    padding: 0;
    margin: -1px;
    overflow: hidden;
    clip-path: inset(50%);
    white-space: nowrap;
    border: 0;
}
```

Use `display: none` or the HTML `hidden` attribute only when the content should be absent from both visual presentation and the accessibility tree. Do not use clipping as a way to hide entire sections or required instructions.

## Accessibility review

- Tab through the page and confirm focus is visible and follows a useful order.
- Zoom in and check that text, controls, and navigation still fit.
- Check text and interface contrast with a contrast tool.
- Confirm links are distinguishable without color alone.
- Enable forced colors and reduced motion in the operating system.
- Check that errors and status changes have text in the HTML.
- Inspect focus at the top and bottom of the page when sticky elements are present.
- Test with real content, including long labels and translated strings.

## Common mistakes

- Removing focus outlines because they look different from the design.
- Using a red or green color change as the only status signal.
- Hiding essential content at narrow widths or with `display: none`.
- Fixing a text box to a height that clips zoomed content.
- Forcing custom colors that erase the user's high contrast palette.
- Using CSS visual order that disagrees with keyboard and reading order.
- Treating a visual CSS improvement as a replacement for semantic HTML and keyboard behavior.

## Official references

- [CSS and JavaScript accessibility](https://developer.mozilla.org/en-US/docs/Learn_web_development/Core/Accessibility/CSS_and_JavaScript)
- [Color contrast](https://developer.mozilla.org/en-US/docs/Web/Accessibility/Guides/Understanding_WCAG/Perceivable/Color_contrast)
- [The `forced-colors` media feature](https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/At-rules/%40media/forced-colors)
- [The `prefers-contrast` media feature](https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/At-rules/%40media/prefers-contrast)
- [WCAG 2.2 contrast minimum](https://www.w3.org/WAI/WCAG22/Understanding/contrast-minimum.html)
- [WCAG 2.2 non-text contrast](https://www.w3.org/WAI/WCAG22/understanding/non-text-contrast.html)
- [WCAG 2.2 target size minimum](https://www.w3.org/WAI/WCAG22/Understanding/target-size-minimum)

| Previous | Notes index | Next |
| --- | --- | --- |
| [Previous: Custom properties and CSS functions](./13-custom-properties-and-css-functions.md) | [Notes index](../README.md) | [Next: Debugging, performance, and browser tools](./15-debugging-performance-and-browser-tools.md) |
