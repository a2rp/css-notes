# 06. Backgrounds, borders, and shadows

[Back to notes index](../README.md)

| Previous | Notes index | Next |
| --- | --- | --- |
| [Previous: Typography and text](./05-typography-and-text.md) | [Notes index](../README.md) | [Next: Flexbox layout](./07-flexbox-layout.md) |

## Background color and images

Use `background-color` for a flat surface. A background image is appropriate for decoration or an image that does not carry essential content. If the image conveys information, use an HTML `<img>` with meaningful alternative text.

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

Multiple background images are comma-separated. The first image is painted above the next one, so the gradient overlay appears above the photograph. The background color is painted below the image layers and can show through transparent areas.

`cover` scales a background image until the box is fully covered, which may crop the image. `contain` keeps the whole image visible, which can leave empty space. Use `background-position` to choose the crop focus.

For meaningful content, use an image element:

```html
<img class="profile-photo" src="profile.jpg" alt="Ashish Ranjan">
```

```css
.profile-photo {
    width: 12rem;
    aspect-ratio: 1;
    object-fit: cover;
    object-position: center 35%;
    border-radius: 50%;
}
```

The `object-fit` property controls how image or video content fills its own box. It is often a better choice than a CSS background when the image is part of the document content.

## Gradients are background images

A gradient can be used where an image is accepted, such as in `background-image`. It does not need a separate image file:

```css
.notice {
    background-color: #0f766e;
    background-image: linear-gradient(135deg, #0f766e, #164e63);
}
```

Keeping a solid `background-color` provides a fallback if a browser does not understand a newer image value. Linear, radial, and conic gradients have different directions and shapes. Use enough contrast between foreground content and every part of a decorative background.

## Borders and corners

The `border` shorthand combines width, style, and color. The style is required for a visible border:

```css
.card {
    border: 1px solid #cbd5e1;
    border-radius: 0.75rem;
}

.card--selected {
    border-color: currentColor;
}
```

`currentColor` uses the element's computed text color. It can keep icons and outlines aligned with the current text color without repeating a color value.

Use different radii only when the design needs them. Very large radii can make rectangular content harder to scan. Rounded corners clip backgrounds, but they do not guarantee that overflowing child content is clipped. If content should be clipped to the rounded shape, consider `overflow: clip` and check that focus indicators remain visible.

## Shadows add depth

A shadow takes horizontal and vertical offsets, blur, optional spread, and a color:

```css
.card {
    box-shadow: 0 0.5rem 1.5rem rgb(15 23 42 / 0.12);
}

.inset-field {
    box-shadow: inset 0 1px 2px rgb(15 23 42 / 0.12);
}
```

Shadows may be stacked with comma-separated values. Use them to communicate elevation or focus only where it helps. Strong shadows on every element can make a page noisy and can reduce contrast around edges.

Do not use a box shadow as the only keyboard focus indicator. A clear `outline` is designed for focus and does not affect layout:

```css
a:focus-visible,
button:focus-visible {
    outline: 3px solid #f97316;
    outline-offset: 3px;
}
```

Focus and interaction styling are discussed further in the accessibility and pseudo-class chapters.

## Understand the background shorthand

The `background` shorthand can set color, image, position, size, repeat, origin, clip, and attachment. Because it resets omitted components to their initial values, a later shorthand may erase a value set earlier in a longhand declaration. Use longhand properties when you only need to change one aspect.

## Try it

1. Add a gradient over a photograph and change the first color's opacity.
2. Change `background-size` from `cover` to `contain`.
3. Compare an image used as a background with the same image in an `<img>`.
4. Remove `border-style` from a border declaration and inspect the result.
5. Check that text remains legible over every part of the background.

## Common mistakes

- Using a background image for meaningful content and losing its alternative text.
- Assuming `cover` shows the entire image.
- Forgetting that the first background layer is on top.
- Writing a border width and color without a border style.
- Replacing an accessible focus outline with a subtle shadow.
- Applying the `background` shorthand and accidentally resetting a longhand value.
- Using shadows so heavily that boundaries become harder to read.

## Official references

- [Backgrounds and borders](https://developer.mozilla.org/en-US/docs/Learn_web_development/Core/Styling_basics/Backgrounds_and_borders)
- [CSS backgrounds and borders](https://developer.mozilla.org/en-US/docs/Web/CSS/Guides/Backgrounds_and_borders)
- [Resizing background images](https://developer.mozilla.org/en-US/docs/Web/CSS/Guides/Backgrounds_and_borders/Resizing_background_images)
- [Using CSS gradients](https://developer.mozilla.org/en-US/docs/Web/CSS/Guides/Images/Using_gradients)
- [The `object-fit` property](https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Properties/object-fit)

| Previous | Notes index | Next |
| --- | --- | --- |
| [Previous: Typography and text](./05-typography-and-text.md) | [Notes index](../README.md) | [Next: Flexbox layout](./07-flexbox-layout.md) |
