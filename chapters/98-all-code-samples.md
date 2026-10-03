# 98. All code samples

[Back to notes index](../README.md)

| Previous | Notes index | Next |
| --- | --- | --- |
| [Previous: CSS architecture and modern CSS](./16-css-architecture-and-modern-css.md) | [Notes index](../README.md) | [Next: Complete questions and answers](./99-complete-q-and-a.md) |

## How to use this reference
Collected 105 code examples from 16 core chapters.


This chapter collects every fenced code example from the 16 core chapters. Each entry links to its source chapter so the surrounding explanation is easy to find. Examples are grouped by their original chapter and section.

## 1. 01. Foundations and CSS syntax: What CSS controls

[Source chapter](./01-foundations-and-css-syntax.md)

```css
p {
    color: #334155;
    line-height: 1.6;
}
```

## 2. 01. Foundations and CSS syntax: Connect an external stylesheet

[Source chapter](./01-foundations-and-css-syntax.md)

```html
<!doctype html>
<html lang="en">
<head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <title>CSS notes</title>
    <link rel="stylesheet" href="styles.css">
</head>
<body>
    <main>
        <h1>Learning CSS</h1>
        <p>Small style changes can make content easier to read.</p>
        <a href="#details">Read the details</a>
    </main>
</body>
</html>
```

## 3. 01. Foundations and CSS syntax: Connect an external stylesheet

[Source chapter](./01-foundations-and-css-syntax.md)

```css
body {
    margin: 0;
    font-family: system-ui, sans-serif;
    color: #1f2937;
    background: #f8fafc;
}

main {
    width: min(100% - 2rem, 42rem);
    margin-inline: auto;
    padding-block: 3rem;
}

a {
    color: #075985;
}
```

## 4. 01. Foundations and CSS syntax: Selectors and declarations

[Source chapter](./01-foundations-and-css-syntax.md)

```html
<p class="notice">Your changes have been saved.</p>
```

## 5. 01. Foundations and CSS syntax: Selectors and declarations

[Source chapter](./01-foundations-and-css-syntax.md)

```css
p {
    line-height: 1.5;
}

.notice {
    padding: 1rem;
    border: 1px solid #64748b;
    background-color: #f1f5f9;
}
```

## 6. 01. Foundations and CSS syntax: Selectors and declarations

[Source chapter](./01-foundations-and-css-syntax.md)

```css
h1,
h2,
h3 {
    font-family: Georgia, serif;
}
```

## 7. 01. Foundations and CSS syntax: Whitespace, comments, and invalid values

[Source chapter](./01-foundations-and-css-syntax.md)

```css
/* Keep the reading column comfortable on wide screens. */
.article {
    max-width: 68ch;
}
```

## 8. 02. Selectors, specificity, and the cascade: Selectors match elements

[Source chapter](./02-selectors-specificity-and-cascade.md)

```html
<article class="card">
    <h2 class="card__title">CSS notes</h2>
    <p>Patterns I want to remember.</p>
    <a href="/notes">Open notes</a>
</article>
```

## 9. 02. Selectors, specificity, and the cascade: Selectors match elements

[Source chapter](./02-selectors-specificity-and-cascade.md)

```css
/* Type selector */
article {
    display: block;
}

/* Class selector */
.card {
    padding: 1rem;
}

/* Descendant selector */
.card a {
    color: #075985;
}

/* Attribute selector */
a[href^="/"] {
    text-decoration-thickness: 0.08em;
}
```

## 10. 02. Selectors, specificity, and the cascade: Specificity is a comparison weight

[Source chapter](./02-selectors-specificity-and-cascade.md)

```css
p { color: navy; }                  /* 0-0-1 */
.notice { color: darkgreen; }       /* 0-1-0 */
article p.notice { color: maroon; } /* 0-1-2 */
#summary { color: purple; }         /* 1-0-0 */
```

## 11. 02. Selectors, specificity, and the cascade: Specificity is only one cascade step

[Source chapter](./02-selectors-specificity-and-cascade.md)

```css
@layer reset, components, utilities;

@layer components {
    .card { color: navy; }
}

@layer utilities {
    .text-muted { color: #475569; }
}
```

## 12. 03. Values, units, and colors: A property accepts specific value types

[Source chapter](./03-values-units-and-colors.md)

```css
.card {
    width: 32rem;
    opacity: 0.96;
    color: rgb(30 41 59);
    border-color: transparent;
}
```

## 13. 03. Values, units, and colors: Choose a unit based on what should scale

[Source chapter](./03-values-units-and-colors.md)

```css
.hero {
    min-height: 100vh;
    min-height: 100svh;
}
```

## 14. 03. Values, units, and colors: Use fluid values with boundaries

[Source chapter](./03-values-units-and-colors.md)

```css
.page {
    width: min(100% - 2rem, 72rem);
    margin-inline: auto;
}

h1 {
    font-size: clamp(2rem, 1.2rem + 3vw, 4rem);
}
```

## 15. 03. Values, units, and colors: Use fluid values with boundaries

[Source chapter](./03-values-units-and-colors.md)

```css
.card-list {
    container-type: inline-size;
}

.card {
    padding: clamp(1rem, 4cqi, 2rem);
}
```

## 16. 03. Values, units, and colors: Common color formats

[Source chapter](./03-values-units-and-colors.md)

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

## 17. 03. Values, units, and colors: Common color formats

[Source chapter](./03-values-units-and-colors.md)

```css
:root {
    --color-text: #172033;
    --color-muted: #475569;
    --color-surface: #ffffff;
    --color-accent: #075985;
}
```

## 18. 03. Values, units, and colors: Unitless values

[Source chapter](./03-values-units-and-colors.md)

```css
.article {
    font-size: 1rem;
    line-height: 1.65;
}
```

## 19. 04. The box model and layout flow: Prefer border-box sizing

[Source chapter](./04-box-model-and-layout-flow.md)

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

## 20. 04. The box model and layout flow: Prefer border-box sizing

[Source chapter](./04-box-model-and-layout-flow.md)

```css
.article {
    width: min(100% - 2rem, 68ch);
    margin-inline: auto;
}
```

## 21. 04. The box model and layout flow: Normal flow places block and inline boxes

[Source chapter](./04-box-model-and-layout-flow.md)

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

## 22. 04. The box model and layout flow: Control overflow deliberately

[Source chapter](./04-box-model-and-layout-flow.md)

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

## 23. 04. The box model and layout flow: Use logical properties for writing direction

[Source chapter](./04-box-model-and-layout-flow.md)

```css
.page-section {
    padding-block: 2rem;
    padding-inline: 1rem;
    border-inline-start: 0.25rem solid #0f766e;
}
```

## 24. 05. Typography and text: Start with a readable type system

[Source chapter](./05-typography-and-text.md)

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

## 25. 05. Typography and text: Set size, weight, and line height

[Source chapter](./05-typography-and-text.md)

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

## 26. 05. Typography and text: Use text properties for meaning and hierarchy

[Source chapter](./05-typography-and-text.md)

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

## 27. 05. Typography and text: Wrap text without hiding content

[Source chapter](./05-typography-and-text.md)

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

## 28. 05. Typography and text: Use the font shorthand carefully

[Source chapter](./05-typography-and-text.md)

```css
.title {
    font: italic 600 1.25rem / 1.3 system-ui, sans-serif;
}
```

## 29. 05. Typography and text: Provide responsive reading sizes

[Source chapter](./05-typography-and-text.md)

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

## 30. 06. Backgrounds, borders, and shadows: Background color and images

[Source chapter](./06-backgrounds-borders-and-shadows.md)

```css
.hero {
    color: white;
    background-color: #123047;
    background-image:
        linear-gradient(rgb(9 25 40 / 0.78), rgb(9 25 40 / 0.18)),
        url("../images/coast.jpg");
    background-position: center;
    background-size: cover;
    background-repeat: no-repeat;
}
```

## 31. 06. Backgrounds, borders, and shadows: Background color and images

[Source chapter](./06-backgrounds-borders-and-shadows.md)

```html
<img class="profile-photo" src="profile.jpg" alt="Ashish Ranjan">
```

## 32. 06. Backgrounds, borders, and shadows: Background color and images

[Source chapter](./06-backgrounds-borders-and-shadows.md)

```css
.profile-photo {
    width: 12rem;
    aspect-ratio: 1;
    object-fit: cover;
    object-position: center 35%;
    border-radius: 50%;
}
```

## 33. 06. Backgrounds, borders, and shadows: Gradients are background images

[Source chapter](./06-backgrounds-borders-and-shadows.md)

```css
.notice {
    background-color: #0f766e;
    background-image: linear-gradient(135deg, #0f766e, #164e63);
}
```

## 34. 06. Backgrounds, borders, and shadows: Borders and corners

[Source chapter](./06-backgrounds-borders-and-shadows.md)

```css
.card {
    border: 1px solid #cbd5e1;
    border-radius: 0.75rem;
}

.card--selected {
    border-color: currentColor;
}
```

## 35. 06. Backgrounds, borders, and shadows: Shadows add depth

[Source chapter](./06-backgrounds-borders-and-shadows.md)

```css
.card {
    box-shadow: 0 0.5rem 1.5rem rgb(15 23 42 / 0.12);
}

.inset-field {
    box-shadow: inset 0 1px 2px rgb(15 23 42 / 0.12);
}
```

## 36. 06. Backgrounds, borders, and shadows: Shadows add depth

[Source chapter](./06-backgrounds-borders-and-shadows.md)

```css
a:focus-visible,
button:focus-visible {
    outline: 3px solid #f97316;
    outline-offset: 3px;
}
```

## 37. 07. Flexbox layout: Use Flexbox for one-dimensional layout

[Source chapter](./07-flexbox-layout.md)

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

## 38. 07. Flexbox layout: Use Flexbox for one-dimensional layout

[Source chapter](./07-flexbox-layout.md)

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

## 39. 07. Flexbox layout: Direction and wrapping

[Source chapter](./07-flexbox-layout.md)

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

## 40. 07. Flexbox layout: Grow, shrink, and basis

[Source chapter](./07-flexbox-layout.md)

```css
.sidebar {
    flex: 0 0 16rem;
}

.main-content {
    flex: 1 1 0;
    min-width: 0;
}
```

## 41. 07. Flexbox layout: Align a group and a single item

[Source chapter](./07-flexbox-layout.md)

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

## 42. 07. Flexbox layout: Align a group and a single item

[Source chapter](./07-flexbox-layout.md)

```css
.toolbar__account {
    margin-inline-start: auto;
}
```

## 43. 08. Grid layout: Use Grid for two-dimensional layout

[Source chapter](./08-grid-layout.md)

```css
.card-grid {
    display: grid;
    grid-template-columns: repeat(3, minmax(0, 1fr));
    gap: 1rem;
}
```

## 44. 08. Grid layout: Make a responsive grid

[Source chapter](./08-grid-layout.md)

```css
.card-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(min(100%, 16rem), 1fr));
    gap: 1rem;
}
```

## 45. 08. Grid layout: Define tracks and gaps

[Source chapter](./08-grid-layout.md)

```css
.dashboard {
    display: grid;
    grid-template-columns: minmax(14rem, 1fr) 3fr;
    grid-template-rows: auto 1fr auto;
    gap: 1rem 1.5rem;
}
```

## 46. 08. Grid layout: Define tracks and gaps

[Source chapter](./08-grid-layout.md)

```css
.gallery {
    display: grid;
    grid-template-columns: repeat(4, minmax(0, 1fr));
    grid-auto-rows: minmax(8rem, auto);
}
```

## 47. 08. Grid layout: Place items by lines or named areas

[Source chapter](./08-grid-layout.md)

```css
.featured-card {
    grid-column: span 2;
}
```

## 48. 08. Grid layout: Place items by lines or named areas

[Source chapter](./08-grid-layout.md)

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

## 49. 08. Grid layout: Place items by lines or named areas

[Source chapter](./08-grid-layout.md)

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

## 50. 09. Positioning and stacking context: Use relative positioning as an anchor

[Source chapter](./09-positioning-and-stacking-context.md)

```html
<article class="card">
    <span class="card__badge">New</span>
    <h2>CSS layout notes</h2>
</article>
```

## 51. 09. Positioning and stacking context: Use relative positioning as an anchor

[Source chapter](./09-positioning-and-stacking-context.md)

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

## 52. 09. Positioning and stacking context: Sticky elements need a threshold

[Source chapter](./09-positioning-and-stacking-context.md)

```css
.section-nav {
    position: sticky;
    inset-block-start: 0;
    z-index: 10;
    background: white;
}
```

## 53. 09. Positioning and stacking context: Understand stacking contexts

[Source chapter](./09-positioning-and-stacking-context.md)

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

## 54. 10. Responsive design and media queries: Build flexible layouts first

[Source chapter](./10-responsive-design-and-media-queries.md)

```html
<meta name="viewport" content="width=device-width, initial-scale=1">
```

## 55. 10. Responsive design and media queries: Build flexible layouts first

[Source chapter](./10-responsive-design-and-media-queries.md)

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

## 56. 10. Responsive design and media queries: Add a breakpoint where content needs it

[Source chapter](./10-responsive-design-and-media-queries.md)

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

## 57. 10. Responsive design and media queries: Use intrinsic layout before more breakpoints

[Source chapter](./10-responsive-design-and-media-queries.md)

```css
.resource-list {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(min(100%, 17rem), 1fr));
    gap: 1rem;
}
```

## 58. 10. Responsive design and media queries: Use container queries for reusable components

[Source chapter](./10-responsive-design-and-media-queries.md)

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

## 59. 10. Responsive design and media queries: Respect print and motion preferences

[Source chapter](./10-responsive-design-and-media-queries.md)

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

## 60. 10. Responsive design and media queries: Respect print and motion preferences

[Source chapter](./10-responsive-design-and-media-queries.md)

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

## 61. 11. Pseudo-classes, pseudo-elements, and forms: Select elements by state with pseudo-classes

[Source chapter](./11-pseudo-classes-elements-and-forms.md)

```css
a:hover {
    color: #0f766e;
}

button:focus-visible {
    outline: 3px solid #f97316;
    outline-offset: 3px;
}

input:disabled {
    cursor: not-allowed;
    opacity: 0.65;
}

.menu-item:first-child {
    border-block-start: 0;
}
```

## 62. 11. Pseudo-classes, pseudo-elements, and forms: Use pseudo-elements for generated decoration

[Source chapter](./11-pseudo-classes-elements-and-forms.md)

```css
.external-link::after {
    content: "!�";
    font-size: 0.85em;
}

.article li::marker {
    color: #0f766e;
}

.article p::selection {
    color: white;
    background: #0f766e;
}
```

## 63. 11. Pseudo-classes, pseudo-elements, and forms: Keep form controls understandable

[Source chapter](./11-pseudo-classes-elements-and-forms.md)

```html
<form>
    <label for="email">Email address</label>
    <input id="email" name="email" type="email" autocomplete="email" required>
    <p class="field-hint">We will send the confirmation to this address.</p>
    <button type="submit">Continue</button>
</form>
```

## 64. 11. Pseudo-classes, pseudo-elements, and forms: Keep form controls understandable

[Source chapter](./11-pseudo-classes-elements-and-forms.md)

```css
input,
select,
textarea,
button {
    font: inherit;
}

input,
select,
textarea {
    max-width: 100%;
    padding: 0.65rem 0.75rem;
    border: 1px solid #64748b;
    border-radius: 0.35rem;
}

input:focus-visible,
select:focus-visible,
textarea:focus-visible,
button:focus-visible {
    outline: 3px solid #f97316;
    outline-offset: 2px;
}

input:invalid {
    border-color: #b91c1c;
}

input[type="checkbox"],
input[type="radio"] {
    accent-color: #0f766e;
}
```

## 65. 11. Pseudo-classes, pseudo-elements, and forms: Make hover optional

[Source chapter](./11-pseudo-classes-elements-and-forms.md)

```css
.button:hover {
    background-color: #134e4a;
}

.button:focus-visible {
    outline: 3px solid #f97316;
    outline-offset: 3px;
}

.button:active {
    transform: translateY(1px);
}
```

## 66. 12. Transforms, transitions, and animations: Transform without changing document flow

[Source chapter](./12-transforms-transitions-and-animations.md)

```css
.icon {
    transform: translateY(-0.1rem) rotate(-8deg);
    transform-origin: center;
}

.card:hover {
    transform: translateY(-0.2rem);
}
```

## 67. 12. Transforms, transitions, and animations: Transition between state values

[Source chapter](./12-transforms-transitions-and-animations.md)

```css
.button {
    color: white;
    background-color: #0f766e;
    transform: translateY(0);
    transition:
        background-color 160ms ease,
        transform 160ms ease;
}

.button:hover {
    background-color: #115e59;
    transform: translateY(-2px);
}
```

## 68. 12. Transforms, transitions, and animations: Define repeated motion with keyframes

[Source chapter](./12-transforms-transitions-and-animations.md)

```css
@keyframes progress-pulse {
    0% {
        opacity: 0.55;
        transform: scaleX(0.35);
    }

    100% {
        opacity: 1;
        transform: scaleX(1);
    }
}

.progress-indicator {
    transform-origin: left;
    animation: progress-pulse 800ms ease-in-out infinite alternate;
}
```

## 69. 12. Transforms, transitions, and animations: Respect reduced motion

[Source chapter](./12-transforms-transitions-and-animations.md)

```css
.panel {
    transition: opacity 180ms ease, transform 180ms ease;
}

@media (prefers-reduced-motion: reduce) {
    .panel {
        transition: none;
    }

    .progress-indicator {
        animation: none;
    }
}
```

## 70. 13. Custom properties and CSS functions: Reuse values with custom properties

[Source chapter](./13-custom-properties-and-css-functions.md)

```css
:root {
    --color-text: #172033;
    --color-surface: #ffffff;
    --color-accent: #0f766e;
    --space-card: 1.25rem;
    --radius-card: 0.75rem;
}

.card {
    padding: var(--space-card);
    color: var(--color-text);
    background: var(--color-surface);
    border-radius: var(--radius-card);
}

.card--quiet {
    --color-surface: #f1f5f9;
}
```

## 71. 13. Custom properties and CSS functions: Use var() fallbacks

[Source chapter](./13-custom-properties-and-css-functions.md)

```css
.button {
    color: var(--button-text, white);
    background-color: var(--button-background, #0f766e);
    border-color: var(--button-border, currentColor);
}
```

## 72. 13. Custom properties and CSS functions: Calculate and constrain values

[Source chapter](./13-custom-properties-and-css-functions.md)

```css
.content {
    width: calc(100% - 2rem);
    max-width: 72rem;
    margin-inline: auto;
}

.section {
    padding-inline: clamp(1rem, 4vw, 3rem);
}

.card-grid {
    grid-template-columns: repeat(auto-fit, minmax(min(100%, 16rem), 1fr));
}
```

## 73. 13. Custom properties and CSS functions: Mix colors with color-mix()

[Source chapter](./13-custom-properties-and-css-functions.md)

```css
:root {
    --brand: oklch(52% 0.12 185);
    --brand-soft: color-mix(in oklab, var(--brand), white 82%);
}

.badge {
    color: var(--brand);
    background-color: var(--brand-soft);
}
```

## 74. 13. Custom properties and CSS functions: Mix colors with color-mix()

[Source chapter](./13-custom-properties-and-css-functions.md)

```css
.badge {
    background-color: #e6f2ef;
    background-color: color-mix(in oklab, var(--brand), white 82%);
}
```

## 75. 13. Custom properties and CSS functions: Register a typed custom property

[Source chapter](./13-custom-properties-and-css-functions.md)

```css
@property --progress {
    syntax: "<number>";
    inherits: false;
    initial-value: 0;
}

.progress-bar {
    transform: scaleX(var(--progress));
    transform-origin: left;
}
```

## 76. 13. Custom properties and CSS functions: Build a simple theme

[Source chapter](./13-custom-properties-and-css-functions.md)

```css
:root {
    color-scheme: light;
    --surface: #ffffff;
    --text: #172033;
}

[data-theme="dark"] {
    color-scheme: dark;
    --surface: #111827;
    --text: #f8fafc;
}

body {
    color: var(--text);
    background-color: var(--surface);
}
```

## 77. 14. Accessibility and inclusive CSS: Preserve visible keyboard focus

[Source chapter](./14-accessibility-and-inclusive-css.md)

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

## 78. 14. Accessibility and inclusive CSS: Check text and control contrast

[Source chapter](./14-accessibility-and-inclusive-css.md)

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

## 79. 14. Accessibility and inclusive CSS: Let content grow and zoom

[Source chapter](./14-accessibility-and-inclusive-css.md)

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

## 80. 14. Accessibility and inclusive CSS: Make controls easy to find and activate

[Source chapter](./14-accessibility-and-inclusive-css.md)

```css
.icon-button {
    display: inline-grid;
    min-width: 2.75rem;
    min-height: 2.75rem;
    place-items: center;
    padding: 0.5rem;
}
```

## 81. 14. Accessibility and inclusive CSS: Support forced colors

[Source chapter](./14-accessibility-and-inclusive-css.md)

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

## 82. 14. Accessibility and inclusive CSS: Honor motion and contrast preferences

[Source chapter](./14-accessibility-and-inclusive-css.md)

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

## 83. 14. Accessibility and inclusive CSS: Keep visually hidden text available

[Source chapter](./14-accessibility-and-inclusive-css.md)

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

## 84. 15. Debugging, performance, and browser tools: Trace the cascade

[Source chapter](./15-debugging-performance-and-browser-tools.md)

```css
.card {
    color: #172033;
}

.page .card {
    color: #334155;
}

.card {
    color: #0f766e;
}
```

## 85. 15. Debugging, performance, and browser tools: Inspect the box and layout

[Source chapter](./15-debugging-performance-and-browser-tools.md)

```css
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
```

## 86. 15. Debugging, performance, and browser tools: Inspect the box and layout

[Source chapter](./15-debugging-performance-and-browser-tools.md)

```css
.results {
    display: grid;
    grid-template-columns: repeat(3, minmax(0, 1fr));
    gap: 1rem;
}

.result {
    min-width: 0;
    overflow-wrap: anywhere;
}
```

## 87. 15. Debugging, performance, and browser tools: Debug responsive behavior

[Source chapter](./15-debugging-performance-and-browser-tools.md)

```css
.article {
    width: min(100% - 2rem, 70rem);
    margin-inline: auto;
}

@media (min-width: 48rem) {
    .article {
        width: min(100% - 4rem, 70rem);
    }
}
```

## 88. 15. Debugging, performance, and browser tools: Debug responsive behavior

[Source chapter](./15-debugging-performance-and-browser-tools.md)

```css
.debug * {
    outline: 1px solid rgb(255 0 0 / 35%);
}
```

## 89. 15. Debugging, performance, and browser tools: Find the source of overflow

[Source chapter](./15-debugging-performance-and-browser-tools.md)

```js
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
```

## 90. 15. Debugging, performance, and browser tools: Check invalid CSS and loaded files

[Source chapter](./15-debugging-performance-and-browser-tools.md)

```css
.heading {
    font-size: 2rem;
    font-size: clamp(1.75rem, 4vw, 3rem);
}
```

## 91. 15. Debugging, performance, and browser tools: Avoid repeated layout reads and writes

[Source chapter](./15-debugging-performance-and-browser-tools.md)

```js
const cards = [...document.querySelectorAll(".card")];

const heights = cards.map((card) => card.getBoundingClientRect().height);

cards.forEach((card, index) => {
    card.style.setProperty("--measured-height", String(heights[index]) + "px");
});
```

## 92. 15. Debugging, performance, and browser tools: Containment and long pages

[Source chapter](./15-debugging-performance-and-browser-tools.md)

```css
.independent-widget {
    contain: layout paint;
}
```

## 93. 15. Debugging, performance, and browser tools: Containment and long pages

[Source chapter](./15-debugging-performance-and-browser-tools.md)

```css
.long-section {
    content-visibility: auto;
    contain-intrinsic-size: auto 36rem;
}
```

## 94. 15. Debugging, performance, and browser tools: Keep animation work focused

[Source chapter](./15-debugging-performance-and-browser-tools.md)

```css
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
```

## 95. 15. Debugging, performance, and browser tools: Check browser support

[Source chapter](./15-debugging-performance-and-browser-tools.md)

```css
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
```

## 96. 16. CSS architecture and modern CSS: Organize styles around clear responsibilities

[Source chapter](./16-css-architecture-and-modern-css.md)

```text
styles/
    reset.css
    tokens.css
    base.css
    layout.css
    components/
        button.css
        card.css
    utilities.css
```

## 97. 16. CSS architecture and modern CSS: Control precedence with cascade layers

[Source chapter](./16-css-architecture-and-modern-css.md)

```css
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
```

## 98. 16. CSS architecture and modern CSS: Keep selectors easy to override

[Source chapter](./16-css-architecture-and-modern-css.md)

```css
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
```

## 99. 16. CSS architecture and modern CSS: Scope component styles

[Source chapter](./16-css-architecture-and-modern-css.md)

```css
@scope (.profile-card) {
    img {
        display: block;
        max-width: 100%;
    }

    h2 {
        margin-block: 0 0.5rem;
    }
}
```

## 100. 16. CSS architecture and modern CSS: Use logical properties for writing direction

[Source chapter](./16-css-architecture-and-modern-css.md)

```css
.card {
    padding-block: 1rem;
    padding-inline: 1.25rem;
    border-inline-start: 0.25rem solid #0f766e;
    margin-block-end: 1rem;
}
```

## 101. 16. CSS architecture and modern CSS: Make components respond to their container

[Source chapter](./16-css-architecture-and-modern-css.md)

```css
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
```

## 102. 16. CSS architecture and modern CSS: Share grid sizing with subgrid

[Source chapter](./16-css-architecture-and-modern-css.md)

```css
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
```

## 103. 16. CSS architecture and modern CSS: Use CSS nesting with restraint

[Source chapter](./16-css-architecture-and-modern-css.md)

```css
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
```

## 104. 16. CSS architecture and modern CSS: Handle third-party styles

[Source chapter](./16-css-architecture-and-modern-css.md)

```css
@import url("./vendor.css") layer(vendor);
@layer reset, vendor, base, components, utilities;
```

## 105. 16. CSS architecture and modern CSS: Modern CSS still needs fallbacks and testing

[Source chapter](./16-css-architecture-and-modern-css.md)

```css
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
```

