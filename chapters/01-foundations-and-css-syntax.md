# 01. Foundations and CSS syntax

[Back to notes index](../README.md)

| Previous | Notes index | Next |
| --- | --- | --- |
| Notes start | [Notes index](../README.md) | [Next: Selectors, specificity, and the cascade](./02-selectors-specificity-and-cascade.md) |

## What CSS controls

CSS describes how a structured document should look and behave on screen or in other media. HTML gives a page its content and meaning. CSS controls presentation such as color, spacing, type, layout, and motion.

A browser reads the HTML into a document tree, loads applicable stylesheets, matches selectors to elements, resolves competing declarations, and paints the result. A CSS rule is a selector followed by a declaration block:

```css
p {
    color: #334155;
    line-height: 1.6;
}
```

Here, `p` is the selector. The braces contain declarations. Each declaration has a property, a colon, a value, and usually a semicolon. The browser applies both declarations to matching paragraph elements.

## Connect an external stylesheet

Create two files in one folder. Put the HTML structure in `index.html`:

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

Put the styles in the linked `styles.css` file:

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

The `href` path is relative to the HTML file. If the stylesheet is in a folder named `css`, use `href="css/styles.css"`. The `rel="stylesheet"` attribute tells the browser what relationship the linked file has to this page.

An external file is a good default because it keeps structure and presentation separate and can be reused by multiple pages. A `<style>` block in the document is useful for a small page-specific example. A `style` attribute applies declarations to one element, but it becomes difficult to maintain when used for many elements.

## Selectors and declarations

Selectors choose the elements a rule can affect. You will study selector types in the next chapter. For now, compare a type selector with a class selector:

```html
<p class="notice">Your changes have been saved.</p>
```

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

The type selector styles paragraphs. The class selector styles any element whose class list contains `notice`. An element can match more than one rule, so its final style can combine declarations from several places.

You can group selectors that share the same declarations:

```css
h1,
h2,
h3 {
    font-family: Georgia, serif;
}
```

Commas separate a selector list. A space has a different meaning: it selects a descendant. Selector details and how competing rules are resolved belong to the next chapter.

## Whitespace, comments, and invalid values

Whitespace and line breaks make CSS easier to read. A declaration block can be written on one line, but one declaration per line is easier to review and edit. A semicolon after the final declaration is optional, but keeping it avoids mistakes when adding another declaration.

Comments explain why a rule exists or mark a section:

```css
/* Keep the reading column comfortable on wide screens. */
.article {
    max-width: 68ch;
}
```

Browsers recover from many CSS errors. If a property name or value is invalid, the browser usually ignores that declaration and continues parsing the rest of the stylesheet. This means a page can partly work even when one declaration is misspelled. Use the browser developer tools to find ignored declarations.

## Try it in the browser

1. Save the two example files in the same folder.
2. Open `index.html` in a browser.
3. Change the body background and the main width.
4. Open developer tools and inspect the paragraph.
5. Temporarily misspell `line-height`, then check which declaration the browser crossed out or ignored.

The goal is to connect a CSS declaration to the visible result and to the browser's computed styles.

## Common mistakes

- Saving the stylesheet under a different name from the `href` value.
- Using a path relative to the wrong folder.
- Forgetting a closing brace or quote.
- Missing a colon between a property and its value.
- Assuming every valid property accepts every value.
- Adding more declarations before checking whether the selector matches the intended elements.
- Using inline styles for an entire site and making shared changes difficult.

## Quick reference

| Part | Example | Purpose |
| --- | --- | --- |
| Selector | `.notice` | Chooses elements |
| Property | `background-color` | Names the feature to change |
| Value | `#f1f5f9` | Sets the chosen feature |
| Declaration | `color: #1f2937;` | Assigns a value to a property |
| Rule | `.notice { padding: 1rem; }` | Applies declarations to matching elements |
| Stylesheet link | `<link rel="stylesheet" href="styles.css">` | Loads an external CSS file |

## Official references

- [What is CSS?](https://developer.mozilla.org/en-US/docs/Learn_web_development/Core/Styling_basics/What_is_CSS)
- [Getting started with CSS](https://developer.mozilla.org/en-US/docs/Learn_web_development/Core/Styling_basics/Getting_started)
- [CSS syntax](https://developer.mozilla.org/en-US/docs/Web/CSS/Guides/Syntax)
- [HTML link element](https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/link)

| Previous | Notes index | Next |
| --- | --- | --- |
| Notes start | [Notes index](../README.md) | [Next: Selectors, specificity, and the cascade](./02-selectors-specificity-and-cascade.md) |
