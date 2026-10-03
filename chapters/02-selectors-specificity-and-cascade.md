# 02. Selectors, specificity, and the cascade

[Back to notes index](../README.md)

| Previous | Notes index | Next |
| --- | --- | --- |
| [Previous: Foundations and CSS syntax](./01-foundations-and-css-syntax.md) | [Notes index](../README.md) | [Next: Values, units, and colors](./03-values-units-and-colors.md) |

## Selectors match elements

A selector describes which elements a rule applies to. Prefer classes for reusable visual roles and semantic HTML elements for broad defaults. IDs are useful for document references and JavaScript hooks, but ID selectors are often too strong for reusable styling.

```html
<article class="card">
    <h2 class="card__title">CSS notes</h2>
    <p>Patterns I want to remember.</p>
    <a href="/notes">Open notes</a>
</article>
```

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

Useful selector forms include:

| Selector | Matches |
| --- | --- |
| `p` | Every paragraph element |
| `.card` | Elements with the class `card` |
| `#main` | The element with ID `main` |
| `[disabled]` | Elements that have a `disabled` attribute |
| `[type="email"]` | Elements with that exact attribute value |
| `[href^="https"]` | Elements whose href starts with the given text |
| `a, button` | Links and buttons |
| `article p` | Paragraphs anywhere inside an article |
| `article > p` | Paragraphs that are direct children of an article |
| `h2 + p` | A paragraph immediately after an h2 |
| `h2 ~ p` | Paragraph siblings after an h2 |

Combinators express relationships in the document tree. A descendant selector uses a space, a child selector uses `>`, an adjacent sibling uses `+`, and a general sibling uses `~`. A selector that depends on long chains of markup is harder to reuse and more likely to break when the HTML changes.

## Specificity is a comparison weight

When competing declarations have already reached the specificity step of the cascade, selectors are compared in three columns:

1. ID selectors
2. Class selectors, attribute selectors, and pseudo-classes
3. Type selectors and pseudo-elements

For example:

```css
p { color: navy; }                  /* 0-0-1 */
.notice { color: darkgreen; }       /* 0-1-0 */
article p.notice { color: maroon; } /* 0-1-2 */
#summary { color: purple; }         /* 1-0-0 */
```

A selector with an ID weight beats selectors with only classes or element names, even if those selectors contain many components. Specificity is not ordinary arithmetic: one ID column outranks any number of class or type entries.

The pseudo-classes `:is()`, `:not()`, and `:has()` take the specificity of their most specific argument. The `:where()` pseudo-class always contributes zero specificity. These rules can keep selectors expressive without making them unnecessarily difficult to override.

## Specificity is only one cascade step

A matching selector does not automatically win because it looks more specific. The browser first considers whether a rule applies, then origin and importance, cascade layer, specificity, scoping proximity where relevant, and source order.

Normal declarations in later cascade layers override normal declarations in earlier layers. Unlayered normal author styles outrank layered normal author styles. The order reverses for important declarations. Specificity is compared only after the earlier cascade steps have selected the relevant origin and layer.

```css
@layer reset, components, utilities;

@layer components {
    .card { color: navy; }
}

@layer utilities {
    .text-muted { color: #475569; }
}
```

If an element has both classes, the later `utilities` layer wins for `color`, even when the component selector has more specificity within its own layer. Declare the layer order near the top of a stylesheet so it is clear.

## Inheritance and initial values

Some properties, such as `color` and `font-family`, normally inherit from a parent. Others, such as `margin` and `border`, do not. A declaration directly matching an element takes precedence over a value inherited from an ancestor.

Every property has an initial value defined by CSS. The keywords `inherit`, `initial`, `unset`, and `revert` let a declaration use an inherited value, the initial value, a property-dependent choice, or an earlier cascade origin. Use these reset keywords only when their effect is clear.

## Fix a conflict without adding more weight

When a declaration is not applied, inspect the element in developer tools. The Styles panel shows matching rules and crossed-out declarations. Find which selector, layer, or origin supplied the winning value.

Prefer these fixes:

- Remove a conflicting declaration that is no longer needed.
- Use one shared class or component scope for the intended style.
- Put related rules in a planned cascade layer.
- Keep selector specificity low and consistent.
- Adjust source order when selectors have equal cascade position and weight.
- Use `!important` only for a deliberate override that cannot be handled cleanly another way.

A stylesheet full of IDs and `!important` values becomes difficult to extend because every later change has to fight the existing rules.

## Try it

1. Give one element two classes that set the same property.
2. Add a type selector that also sets the property.
3. Move the declarations into two cascade layers and change the layer order.
4. Inspect the element and identify the winning rule.
5. Replace a `:where(.card)` selector with `.card` and compare its specificity.

## Common mistakes

- Assuming the longest selector always wins.
- Comparing specificity before checking origin, importance, or layer.
- Adding `!important` without finding the original conflicting rule.
- Styling every repeated component by a long descendant chain.
- Expecting a non-inherited property to flow from a parent.
- Forgetting that an unlayered normal declaration outranks layered normal declarations from the same origin.
- Treating `:is()`, `:not()`, `:has()`, and `:where()` as if they all add specificity the same way.

## Official references

- [CSS selectors and combinators](https://developer.mozilla.org/en-US/docs/Web/CSS/Guides/Selectors/Selectors_and_combinators)
- [Introduction to the CSS cascade](https://developer.mozilla.org/en-US/docs/Web/CSS/Guides/Cascade/Introduction)
- [Specificity](https://developer.mozilla.org/en-US/docs/Web/CSS/Guides/Cascade/Specificity)
- [Cascade layers](https://developer.mozilla.org/en-US/docs/Web/CSS/Guides/Cascade/Cascade_layers)
- [The `:where()` pseudo-class](https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Selectors/%3Awhere)

| Previous | Notes index | Next |
| --- | --- | --- |
| [Previous: Foundations and CSS syntax](./01-foundations-and-css-syntax.md) | [Notes index](../README.md) | [Next: Values, units, and colors](./03-values-units-and-colors.md) |
