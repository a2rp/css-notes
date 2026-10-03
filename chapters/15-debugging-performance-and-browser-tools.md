# 15. Debugging, performance, and browser tools

[Back to notes index](../README.md)

| Previous | Notes index | Next |
| --- | --- | --- |
| [Previous: Accessibility and inclusive CSS](./14-accessibility-and-inclusive-css.md) | [Notes index](../README.md) | [Next: CSS architecture and modern CSS](./16-css-architecture-and-modern-css.md) |

## Start with evidence

Browser developer tools show which rules match an element, which declarations win, the computed result, the box dimensions, and the layout relationships. Use them to test a cause before changing the stylesheet.

A reliable debugging loop is:

1. Reproduce the issue at a known viewport size.
2. Inspect the element and its ancestors.
3. Check matched rules, computed values, and box dimensions.
4. Change one value temporarily to test a fix.
5. Verify nearby viewport sizes and interaction states.
6. Move the confirmed change into the source and remove temporary styles.

A declaration can be valid CSS and still lose in the cascade, target the wrong element, or be constrained by a parent.

## Trace the cascade

The Styles panel marks declarations that lost in the cascade. The active value might come from a stylesheet, media query, inheritance, or browser default. The Computed panel shows the final value. Expand a property to see which declaration supplied it.

~~~css
.card {
    color: #172033;
}

.page .card {
    color: #334155;
}

.card {
    color: #0f766e;
}
~~~

For an element matching all three selectors, `.page .card` has greater specificity than either single-class selector, so the final color is `#334155`. Source order resolves a tie only after origin, importance, cascade layer, and specificity have been considered.

Find why a rule lost before adding another selector or `!important`. A new override can hide the original cause and make future changes harder.

## Inspect the box and layout

The box model view shows content, padding, border, and margin. Compare the diagram with the rendered dimensions. If the element is larger than its declared width, check whether padding and borders are added outside that width.

~~~css
*,
*::before,
*::after {
    box-sizing: border-box;
}

.panel {
    width: 20rem;
    padding: 1.5rem;
    border: 1px solid #cbd5e1;
}
~~~

For flex and grid containers, enable the layout overlay and inspect the container before changing each child. Track sizes, `gap`, flex basis, and minimum sizes can constrain the result.

~~~css
.results {
    display: grid;
    grid-template-columns: repeat(3, minmax(0, 1fr));
    gap: 1rem;
}

.result {
    min-width: 0;
    overflow-wrap: anywhere;
}
~~~

If long text forces a column wider than expected, inspect the track and the child's minimum size. `minmax(0, 1fr)` and `min-width: 0` let the content shrink; `overflow-wrap` handles long unbroken values.

## Debug responsive behavior

Use device emulation to test viewport widths, device pixel ratios, and touch behavior. Resize through the range around each breakpoint because a layout can fail between common phone and desktop sizes.

~~~css
.article {
    width: min(100% - 2rem, 70rem);
    margin-inline: auto;
}

@media (min-width: 48rem) {
    .article {
        width: min(100% - 4rem, 70rem);
    }
}
~~~

When a media query appears inactive, check the viewport width, whether the stylesheet loaded, and whether a later rule overrides it. Also inspect the rendered page width. A fixed-width child can cause overflow on a narrow screen.

A temporary outline can reveal unexpected dimensions:

~~~css
.debug * {
    outline: 1px solid rgb(255 0 0 / 35%);
}
~~~

Remove diagnostic styles after finding the cause. Do not hide page overflow as a substitute for fixing the element that extends past the viewport.

## Find the source of overflow

Run this in the browser Console while the page is overflowing. It reports elements whose right edge extends beyond the viewport:

~~~js
const viewportWidth = document.documentElement.clientWidth;

const overflowing = [...document.querySelectorAll("*")].filter((element) => {
    return element.getBoundingClientRect().right > viewportWidth;
});

console.table(
    overflowing.map((element) => ({
        element,
        right: Math.round(element.getBoundingClientRect().right),
        width: Math.round(element.getBoundingClientRect().width),
    })),
);
~~~

Inspect the reported elements in the Elements panel. Common causes include fixed widths, unbroken text, positioned decoration, oversized images, and grid tracks that cannot shrink.

## Check invalid CSS and loaded files

The browser ignores a declaration when its property or value is invalid. Check the Styles panel and Console for parse errors, then confirm that the stylesheet URL succeeded in the Network panel.

~~~css
.heading {
    font-size: 2rem;
    font-size: clamp(1.75rem, 4vw, 3rem);
}
~~~

The first declaration is a fallback for browsers without `clamp()`. Browsers that support it use the second declaration. When neither value is valid, the property follows inheritance or its initial value.

If a recent change does not appear, confirm the response content and cache state before refreshing. This distinguishes a CSS issue from a stale file or incorrect URL.

## Understand rendering cost

A visual change can trigger style recalculation, layout, paint, and compositing. The work depends on the property and the affected page.

- Changing `color` usually needs paint but does not change geometry.
- Changing `width` or `font-size` can require layout and paint.
- Changing `transform` or `opacity` may be handled by compositing, but promotion is not guaranteed and layers use memory.

Treat these as common patterns, not universal rules. Record the interaction in the Performance panel to find long tasks, repeated layout, large paint areas, or expensive style recalculation. Measure on a representative device before optimizing.

## Avoid repeated layout reads and writes

Reading geometry after changing layout can force the browser to calculate layout immediately. Repeating a write, read, write, read pattern may cause extra synchronous work.

~~~js
const cards = [...document.querySelectorAll(".card")];

const heights = cards.map((card) => card.getBoundingClientRect().height);

cards.forEach((card, index) => {
    card.style.setProperty("--measured-height", String(heights[index]) + "px");
});
~~~

This reads all heights first, then writes all values. Prefer one update pass and let the browser batch work. Use JavaScript measurements only when the interface needs them, and check their cost in the Performance panel.

## Containment and long pages

Containment can limit how far some layout, style, or paint work affects surrounding content. It changes layout behavior, so apply it only when a component can safely be isolated.

~~~css
.independent-widget {
    contain: layout paint;
}
~~~

For long pages, `content-visibility: auto` lets the browser skip rendering work for sections that are far from the viewport:

~~~css
.long-section {
    content-visibility: auto;
    contain-intrinsic-size: auto 36rem;
}
~~~

The intrinsic size is an estimate while content is skipped and helps reduce scroll jumps. Test anchor navigation, find-in-page, assistive technology, and size changes with the actual content. Do not use these properties to hide information.

## Keep animation work focused

Prefer `transform` and `opacity` for motion when they fit the effect. Animating `top`, `left`, `width`, or `height` can cause repeated layout.

~~~css
.notice {
    opacity: 0;
    transform: translateY(0.5rem);
    transition:
        opacity 180ms ease,
        transform 180ms ease;
}

.notice.is-visible {
    opacity: 1;
    transform: translateY(0);
}

@media (prefers-reduced-motion: reduce) {
    .notice {
        transition: none;
    }
}
~~~

Use `will-change` only when profiling shows a specific element needs it. Remove the hint when the interaction ends. Applying it everywhere can consume memory and create unnecessary layers.

## Check browser support

Test the exact properties and values in browsers your users need. A rule can parse correctly but still be unsupported in a target browser. Use a feature query when a useful fallback exists:

~~~css
.card-list {
    display: block;
}

@supports (display: grid) {
    .card-list {
        display: grid;
        grid-template-columns: repeat(auto-fit, minmax(16rem, 1fr));
        gap: 1rem;
    }
}
~~~

Feature queries check whether a browser understands a declaration. They do not confirm that the result is accessible or visually correct.

## Investigation checklist

Before closing a CSS issue, confirm that:

- The issue is reproducible at a recorded viewport and browser.
- The winning declaration and its source are understood.
- Parent layout, intrinsic sizing, and box dimensions are checked.
- Nearby viewport widths and interaction states work.
- Keyboard focus remains visible.
- Console errors and failed stylesheet requests are resolved.
- Performance has been measured when the page felt slow.
- Temporary declarations and diagnostic styles are removed.

## Browser panels

- **Elements or Inspector:** inspect markup, matched rules, computed values, and layout.
- **Console:** check errors and run a small diagnostic script.
- **Network:** confirm stylesheets and assets loaded and inspect their responses.
- **Performance:** record interactions and locate slow rendering work.
- **Rendering tools:** inspect paint, layout shifts, and viewport behavior where supported.

## Further reading

- [Chrome DevTools: CSS features reference](https://developer.chrome.com/docs/devtools/css/)
- [Chrome DevTools: Performance panel](https://developer.chrome.com/docs/devtools/performance/)
- [MDN: Web performance](https://developer.mozilla.org/en-US/docs/Web/Performance)
- [MDN: content-visibility](https://developer.mozilla.org/en-US/docs/Web/CSS/content-visibility)
- [MDN: @supports](https://developer.mozilla.org/en-US/docs/Web/CSS/@supports)
