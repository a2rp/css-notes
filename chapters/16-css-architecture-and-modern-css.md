# 16. CSS architecture and modern CSS

[Back to notes index](../README.md)

| Previous | Notes index | Next |
| --- | --- | --- |
| [Previous: Debugging, performance, and browser tools](./15-debugging-performance-and-browser-tools.md) | [Notes index](../README.md) | [Notes index](../README.md) |

## Organize styles around clear responsibilities

A stylesheet is easier to change when each rule has a clear place and purpose. Separate reset rules, shared tokens, base element styles, layout, components, and small utilities. Keep related styles close to the component or feature that owns them when the project structure supports it.

One possible file layout is:

~~~text
styles/
    reset.css
    tokens.css
    base.css
    layout.css
    components/
        button.css
        card.css
    utilities.css
~~~

Small projects may not need this many files. Start with a few useful boundaries and split files when it improves navigation or ownership. Avoid creating a file for every selector.

## Control precedence with cascade layers

Cascade layers let a project define broad precedence groups. Declare their order near the start of the stylesheet:

~~~css
@layer reset, base, layout, components, utilities;

@layer reset {
    *,
    *::before,
    *::after {
        box-sizing: border-box;
    }
}

@layer base {
    body {
        margin: 0;
        color: #172033;
        font-family: system-ui, sans-serif;
    }
}

@layer components {
    .button {
        border: 0;
        border-radius: 0.5rem;
        padding: 0.75rem 1rem;
    }
}
~~~

For normal declarations, later layers have higher priority than earlier layers. Specificity and source order are considered within a layer. Normal unlayered author declarations outrank normal declarations inside layers, so keep the policy consistent instead of mixing layered and unlayered component styles by accident.

Layers can help organize third-party styles and application overrides without escalating selector specificity. They do not remove the need to understand the cascade.

## Keep selectors easy to override

Prefer selectors that describe a component and its state without encoding a long path through the document.

~~~css
.notice {
    padding: 1rem;
    border-inline-start: 0.25rem solid currentColor;
}

.notice--warning {
    color: #7c2d12;
    background: #ffedd5;
}

.notice[hidden] {
    display: none;
}
~~~

A selector such as `.page main .content article.notice` ties a style to many ancestors. If the markup changes, the style can stop matching. Lower specificity makes component variations easier to express and reduces the need for `!important`.

Use a consistent naming approach for components and variants. Names should help a reader identify what a class represents without describing its exact pixel appearance.

## Scope component styles

Components should own their visual rules and avoid accidental effects on unrelated markup. A component class is often sufficient for a clear boundary. The `@scope` rule can provide an explicit selector boundary in browsers that support it:

~~~css
@scope (.profile-card) {
    img {
        display: block;
        max-width: 100%;
    }

    h2 {
        margin-block: 0 0.5rem;
    }
}
~~~

Rules inside this scope match descendants of `.profile-card`. Check current browser support before relying on a newer feature, and keep a fallback when the component must work in older browsers.

Do not assume visual isolation makes a component accessible. The document structure, accessible names, focus behavior, and reading order still come from the markup and interaction design.

## Use logical properties for writing direction

Logical properties describe a position in the text flow rather than assuming left-to-right writing. This lets the same component adapt to right-to-left languages and vertical writing modes.

~~~css
.card {
    padding-block: 1rem;
    padding-inline: 1.25rem;
    border-inline-start: 0.25rem solid #0f766e;
    margin-block-end: 1rem;
}
~~~

Use `inline` for the direction text normally flows across and `block` for the direction it stacks. Prefer properties such as `margin-inline` and `inset-block-start` when the intent is about the reading flow. Physical properties such as `margin-left` remain useful when the design truly refers to a physical side.

## Make components respond to their container

A viewport media query responds to the page width. A container query responds to the space available to a component, which is useful when the same component appears in different parts of a page.

~~~css
.project-list {
    container-type: inline-size;
}

.project-card {
    display: grid;
    gap: 1rem;
}

@container (min-width: 36rem) {
    .project-card {
        grid-template-columns: 10rem 1fr;
        align-items: center;
    }
}
~~~

The element with `container-type` establishes a query container for its descendants. Check that it has the right available width and that its children do not force it wider.

Container queries should respond to a real layout need. A media query may be simpler when the whole page changes at a viewport breakpoint.

## Share grid sizing with subgrid

A nested grid can use `subgrid` to align its tracks with a parent grid. This is useful when repeated cards need headings, details, or actions to line up across columns.

~~~css
.directory {
    display: grid;
    grid-template-columns: repeat(3, minmax(0, 1fr));
    gap: 1rem;
}

.directory-card {
    display: grid;
    grid-row: span 3;
    grid-template-rows: subgrid;
    gap: 0.75rem;
}
~~~

Subgrid sizing depends on the parent tracks and the rows the child spans. Test long and short content together, and provide a simpler layout for browsers that do not support the feature if needed.

Keep the source order meaningful. Do not use grid placement to create a visual order that conflicts with keyboard or screen-reader order.

## Use CSS nesting with restraint

Native nesting can keep closely related states near a component:

~~~css
.button {
    color: white;
    background: #0f766e;

    &:hover {
        background: #115e59;
    }

    &:focus-visible {
        outline: 3px solid #f97316;
        outline-offset: 3px;
    }

    &.button--quiet {
        color: #172033;
        background: #e2e8f0;
    }
}
~~~

Nesting is useful for a component's states. Deep nesting can create selectors with higher specificity and make rules difficult to locate. Keep nesting shallow and check target browser support when needed.

## Choose a naming and reuse strategy

A project can use plain class names, a naming convention such as Block Element Modifier, CSS Modules, or another build-time boundary. Each approach can work when used consistently.

- Use names that express purpose, such as `.search-form` or `.card__title`.
- Keep component state explicit, such as `.is-open` or `.button--quiet`.
- Put shared values in custom properties when several components use them.
- Keep one-off declarations local when a shared abstraction would add indirection.
- Remove unused rules when a component is removed.

A component should not require many unrelated global selectors to look correct. Make its key layout and state rules easy to find.

## Handle third-party styles

If external CSS is part of the project, decide where it belongs in the cascade. Importing it into a named layer can make application layers easier to manage:

~~~css
@import url("./vendor.css") layer(vendor);
@layer reset, vendor, base, components, utilities;
~~~

Check import ordering rules and the package's own assumptions. Third-party styles may contain unlayered rules or higher priority declarations, which can change how overrides behave. Inspect the computed result rather than adding increasingly specific selectors.

## Modern CSS still needs fallbacks and testing

Newer features can simplify layout, but browser support and content shape matter. Use feature queries where fallback behavior is useful:

~~~css
.card-list {
    display: flex;
    flex-wrap: wrap;
    gap: 1rem;
}

@supports (display: grid) {
    .card-list {
        display: grid;
        grid-template-columns: repeat(auto-fit, minmax(min(100%, 18rem), 1fr));
    }
}
~~~

Test narrow and wide containers, long text, missing images, keyboard focus, zoom, and right-to-left direction where relevant. A rule that works with sample content may fail with real content.

## A maintainable CSS review

Before merging a stylesheet change, check:

- Each rule has a clear component, layout, or base responsibility.
- Layer order is deliberate and unlayered styles are understood.
- Selectors remain short and can be overridden without `!important`.
- Logical properties are used where the design follows text direction.
- Components work in the containers where they are actually used.
- DOM reading order still matches the visual and keyboard order.
- Newer features have appropriate support checks or fallbacks.
- Repeated values and unused rules are handled consistently.

## Further reading

- [MDN: Cascade layers](https://developer.mozilla.org/en-US/docs/Learn_web_development/Core/Styling_basics/Cascade_layers)
- [MDN: @scope](https://developer.mozilla.org/en-US/docs/Web/CSS/@scope)
- [MDN: Container queries](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_containment/Container_queries)
- [MDN: Subgrid](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_grid_layout/Subgrid)
- [MDN: CSS nesting](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_nesting)
- [MDN: Logical properties](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_logical_properties_and_values)
