# 11. Pseudo-classes, pseudo-elements, and forms

[Back to notes index](../README.md)

| Previous | Notes index | Next |
| --- | --- | --- |
| [Previous: Responsive design and media queries](./10-responsive-design-and-media-queries.md) | [Notes index](../README.md) | [Next: Transforms, transitions, and animations](./12-transforms-transitions-and-animations.md) |

## Select elements by state with pseudo-classes

A pseudo-class adds a condition to a selector. It can describe interaction, document position, or a form control's state.

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

Common structural pseudo-classes include `:first-child`, `:last-child`, `:nth-child()`, and `:only-child`. Common interaction and input states include `:hover`, `:focus`, `:focus-visible`, `:checked`, `:disabled`, `:required`, `:valid`, and `:invalid`.

Use `:focus-visible` to provide a clear focus indicator when the browser determines it is needed. Keep a visible focus style for keyboard users. Do not remove the browser outline without replacing it with a clear indicator.

## Use pseudo-elements for generated decoration

A pseudo-element styles a specific part of an element or creates a generated box:

```css
.external-link::after {
    content: "!—";
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

`::before` and `::after` create generated content and require a `content` value. Use them for decoration such as an icon or divider. Do not put essential instructions, labels, or information only in generated content because it may not be available in every assistive technology or copy-and-paste flow.

Other useful pseudo-elements include `::marker` for list markers, `::placeholder` for placeholder text, and `::selection` for selected text. Placeholder text is not a replacement for a visible label.

## Keep form controls understandable

Start with semantic HTML, labels, and native controls. Style the control without removing the platform's useful behavior:

```html
<form>
    <label for="email">Email address</label>
    <input id="email" name="email" type="email" autocomplete="email" required>
    <p class="field-hint">We will send the confirmation to this address.</p>
    <button type="submit">Continue</button>
</form>
```

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

Do not rely on red border color alone to explain an error. Provide readable error text and associate it with the field when the page behavior allows. Native browser validation can help, but server-side validation is still required for submitted data.

The `accent-color` property can tint supported native controls without removing their native appearance. If a custom checkbox or radio is necessary, test keyboard interaction, focus, checked state, contrast, forced colors, and assistive technology behavior.

## Make hover optional

A hover state is useful feedback for a mouse or trackpad, but touchscreens do not have reliable hover. Provide equivalent focus and active states where appropriate:

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

The control should remain understandable and usable when no hover style is available.

## Try it

1. Tab through the form and check every focus state.
2. Add `:checked` styling to a checkbox.
3. Change the email to an invalid value and submit the form.
4. Select text and style its `::selection`.
5. Disable hover styling in developer tools and confirm the control still has clear feedback.

## Common mistakes

- Removing focus outlines without a visible replacement.
- Showing important instructions only with `::before` or `::after`.
- Using placeholder text instead of a label.
- Indicating invalid state with color only.
- Styling a form based on `:invalid` before the user has had a chance to enter data.
- Replacing native controls with custom visuals without rebuilding their keyboard behavior.
- Depending on hover for an essential action.

## Official references

- [Pseudo-classes](https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Selectors/Pseudo-classes)
- [Pseudo-elements](https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Selectors/Pseudo-elements)
- [The `:focus-visible` pseudo-class](https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Selectors/%3Afocus-visible)
- [Styling UI states in forms](https://developer.mozilla.org/en-US/docs/Learn_web_development/Extensions/Forms/UI_pseudo-classes)
- [The `accent-color` property](https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Properties/accent-color)

| Previous | Notes index | Next |
| --- | --- | --- |
| [Previous: Responsive design and media queries](./10-responsive-design-and-media-queries.md) | [Notes index](../README.md) | [Next: Transforms, transitions, and animations](./12-transforms-transitions-and-animations.md) |
