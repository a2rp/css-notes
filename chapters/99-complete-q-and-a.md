# 99. Complete CSS questions and answers

[Back to notes index](../README.md)

| Previous | Notes index | Next |
| --- | --- | --- |
| [Previous: All code samples](./98-all-code-samples.md) | [Notes index](../README.md) | End of notes |

## Foundations

### 1. What does CSS do?

CSS describes how a document is presented. It controls visual properties such as color, spacing, typography, layout, and motion. HTML provides the document structure and meaning.

### 2. What is a CSS rule?

A rule has a selector and a declaration block. The selector identifies elements. Each declaration pairs a property with a value, such as a text color or margin.

### 3. How can CSS be added to a page?

A page can load an external stylesheet with a link element, include rules in a style element, or apply a style attribute to one element. External stylesheets are usually easiest to reuse and maintain.

### 4. What is the difference between a property and a value?

A property names what is being changed, such as color or display. A value specifies the chosen setting, such as navy or grid.

### 5. What is inheritance?

Some properties pass computed values from an element to its descendants. Text color and font family commonly inherit. Margins and borders generally do not.

### 6. What are initial, inherit, unset, and revert?

Initial uses a property's initial value. Inherit takes the parent's computed value. Unset behaves like inherit for inherited properties and initial for other properties. Revert returns to the value established by an earlier cascade origin.

### 7. Why do browsers have default styles?

Browsers supply baseline presentation for common HTML elements so documents remain usable without a custom stylesheet. A reset or normalization stylesheet can adjust those defaults, but should preserve useful behavior.

## Selectors and the cascade

### 8. What is a selector?

A selector is a pattern that identifies elements for a rule. It can match by element name, class, ID, attribute, relationship, state, or a combination of these.

### 9. When should a class be used instead of an ID selector?

Use classes for reusable styling and component states. IDs should be unique in a document and are often better suited to fragment targets and scripting relationships than reusable style rules.

### 10. How is selector specificity compared?

Specificity is compared by selector categories, including IDs, classes and attributes, and type selectors. The cascade first considers origin, importance, and layer. Specificity and then source order resolve later comparisons.

### 11. Does a later rule always win?

No. Source order breaks ties after the earlier cascade decisions. A later declaration can lose to a declaration with higher priority or specificity.

### 12. What does the universal selector match?

The universal selector matches elements in its scope. It is often used in a small reset, for example to apply box sizing consistently.

### 13. What is the difference between a descendant and child combinator?

A descendant combinator matches at any depth below an element. A child combinator matches only direct children.

### 14. What do :is(), :where(), and :not() do?

They group or exclude selector patterns. The specificity of :is() and :not() comes from their most specific argument. :where() always contributes zero specificity.

### 15. Why should !important be used sparingly?

It changes the priority of a declaration and makes ordinary overrides harder. Prefer fixing selector scope, layer order, or source organization so the cascade remains predictable.

### 16. What are cascade layers?

Layers group declarations into named precedence levels. They provide a deliberate order for broad rules such as reset, base, components, and utilities.

## Values and sizing

### 17. What is the difference between px, rem, and em?

A CSS pixel is a reference unit, not necessarily one physical screen pixel. Rem is based on the root font size. Em is based on the current element's font size for most properties, and can compound through nested elements.

### 18. When should percentages be used?

Percentages are useful when a value should relate to another size, such as a child's width relative to its containing block. The reference depends on the property, so check how that property defines percentages.

### 19. What do vw and vh measure?

They are viewport-relative units. Newer small, large, and dynamic viewport units help express behavior around mobile browser controls. Test the result on actual narrow screens.

### 20. What does calc() do?

It calculates a value from compatible CSS values, such as subtracting fixed padding from a percentage width. Spaces around addition and subtraction operators are required.

### 21. What do min(), max(), and clamp() do?

Min chooses the smallest supplied value, max chooses the largest, and clamp keeps a preferred value within a minimum and maximum. They can create fluid sizing without many breakpoints.

### 22. How should colors be written?

CSS supports named colors, hexadecimal, RGB, HSL, Lab, and other color forms. Choose formats that make the desired adjustment clear, and verify actual contrast between foreground and background.

## Box model and flow

### 23. What is the box model?

Each element has a content box, padding, border, and margin. The box sizing model determines how the declared width and height relate to those parts.

### 24. What does box-sizing: border-box change?

It includes padding and border within the declared width and height. This makes component sizing more predictable, especially when a layout has multiple columns.

### 25. What is margin collapsing?

In some block layout cases, adjacent vertical margins combine into one margin instead of adding together. Flex and grid items do not collapse margins in the same way.

### 26. What is normal flow?

Normal flow is the browser's default placement of in-flow content. Blocks generally stack, while inline content flows within lines. Positioning and layout systems can change this behavior.

### 27. What is the difference between overflow: hidden and overflow: auto?

Hidden clips overflowing content and does not provide a user-controlled scroll area. Auto creates scrolling when overflow requires it. Both can affect focus visibility and sticky positioning, so choose based on the component's purpose.

### 28. Why can a child overflow its container?

It may have a fixed width, unbroken text, large intrinsic dimensions, a minimum size, or positioned content. Inspect the child and its ancestors before hiding overflow.

### 29. What is intrinsic sizing?

Intrinsic sizing uses an element's content or natural dimensions to determine its size. Images, long text, and minimum content sizes can affect grid, flex, and block layouts.

## Layout and positioning

### 30. When is Flexbox useful?

Flexbox is useful for arranging items along one primary axis, with flexible growth, shrinkage, wrapping, and alignment. It is common for navigation rows, toolbars, and aligned controls.

### 31. What does flex: 1 mean?

It is shorthand that allows an item to grow and shrink and gives it a zero basis in the common one-number form. Neighboring items, minimum sizes, and available space still affect its final size.

### 32. What is the difference between justify-content and align-items?

They align items along different axes based on the layout direction. In a row flex container, justify-content handles the main horizontal axis and align-items handles the cross axis.

### 33. When is CSS Grid useful?

Grid is useful for two-dimensional layouts with rows and columns, explicit tracks, and alignment between both axes. It also works well for responsive collections of repeated cards.

### 34. What does minmax() do in Grid?

It sets a minimum and maximum size for a track. A zero minimum, as in minmax(0, 1fr), lets a flexible track shrink below its automatic minimum when content would otherwise force overflow.

### 35. What is the difference between auto-fit and auto-fill?

Both repeat tracks to fit available space. Auto-fill retains empty tracks when there is room for more columns. Auto-fit collapses empty tracks so existing items can expand.

### 36. What does position: relative do?

It keeps an element in normal flow and allows offsets relative to its original position. It also commonly establishes the containing block for absolutely positioned descendants.

### 37. What does position: absolute do?

It removes the element from normal flow and positions it relative to its containing block. The containing block often comes from a positioned ancestor.

### 38. How does sticky positioning work?

A sticky element participates in flow, then sticks relative to its scroll container after reaching an inset threshold. An ancestor's overflow and the available scroll space can prevent the expected behavior.

### 39. What is a stacking context?

A stacking context is a group of elements painted together in a defined order. Properties such as positioned z-index, opacity below one, and transforms can create new contexts. A large z-index cannot escape its parent stacking context.

## Responsive and modern CSS

### 40. What is responsive design?

Responsive design lets a page adapt to available space and user settings. Fluid sizing, flexible layouts, media queries, and content-aware components all contribute.

### 41. How should breakpoints be chosen?

Choose breakpoints where the content or layout needs to change, not only at a list of popular device widths. Test gradually across the width range around the change.

### 42. What is the difference between a media query and a container query?

A media query responds to viewport or user environment features. A container query responds to the size or state of a marked ancestor container.

### 43. What is a mobile-first stylesheet?

It starts with styles for a narrow or constrained viewport, then adds rules as more space becomes available. It is a useful approach, but the design should follow content needs rather than a slogan.

### 44. What is a feature query?

A feature query checks whether the browser supports a CSS declaration. It can apply an enhanced layout while retaining a simpler fallback.

### 45. What are logical properties?

Logical properties express spacing and positioning relative to writing direction and text flow. They help components adapt to right-to-left and vertical writing modes.

### 46. What does subgrid do?

Subgrid lets a nested grid use tracks from its parent grid. It can align repeated component content across shared rows or columns.

### 47. What are cascade layers useful for?

They establish a deliberate order between groups of normal declarations. This can make resets, vendor CSS, components, and utilities easier to manage.

### 48. Should modern CSS features always replace older techniques?

No. Use a newer feature when it solves a real need, check support for target browsers, and provide a reasonable fallback when the feature is essential to the experience.

## Text, backgrounds, and forms

### 49. Why include fallback fonts?

A fallback stack gives the browser alternatives when the preferred font is unavailable. It also helps keep text readable while a web font loads or fails.

### 50. What does line-height control?

It controls the height of a line box and affects readability and vertical rhythm. Unitless values usually scale naturally with the element's font size.

### 51. How can long words avoid breaking a layout?

Use wrapping behavior such as overflow-wrap where breaking a long value is acceptable. Also check the width and minimum size of the containing layout track.

### 52. How do background-size: cover and contain differ?

Cover scales an image until the area is filled, which may crop part of it. Contain shows the full image, which may leave empty space.

### 53. Should form controls be fully restyled?

Only when the design needs it and the control remains usable. Preserve clear labels, focus indicators, contrast, states, and platform behavior. Test with keyboard and assistive technology.

### 54. What are pseudo-classes and pseudo-elements?

Pseudo-classes select elements in a state or relationship, such as hover or focus. Pseudo-elements style a part of an element or generated presentation, such as its first line.

### 55. When should generated content be used?

It is appropriate for decorative presentation, such as a visual marker. Do not put essential information only in generated content because access and selection behavior can vary.

### 56. What is the difference between :focus and :focus-visible?

Focus matches a focused element. Focus-visible lets the browser apply visible focus styling when it determines the user benefits from an indicator, commonly during keyboard navigation.

## Accessibility and motion

### 57. What text contrast is generally required for WCAG AA?

Normal text generally needs a contrast ratio of at least 4.5 to 1. Large text generally needs at least 3 to 1. Check the applicable standard and the actual colors used.

### 58. Can color alone communicate an error?

It should not. Pair color with text, an icon, a shape, or another visible cue so the state is understandable without color perception.

### 59. Why must keyboard focus remain visible?

Keyboard users need to identify which control will receive input. Keep the browser outline or provide a clear replacement with sufficient contrast.

### 60. What does prefers-reduced-motion do?

It detects a user setting requesting less motion. Use it to remove or reduce nonessential animation and transitions.

### 61. What does forced-colors mode do?

It lets the operating system apply a restricted palette, often for contrast or accessibility needs. Test that controls, borders, and state indicators remain visible.

### 62. Can CSS make an inaccessible document semantic?

No. CSS changes presentation. Correct structure, labels, accessible names, keyboard interaction, and document meaning belong in HTML and application behavior.

### 63. Should small text be fixed at a pixel size?

Avoid preventing users from resizing text. Relative units and layouts that tolerate zoom help content remain readable.

### 64. What should be checked after changing visual order?

Compare visual order with DOM reading order and keyboard navigation order. CSS placement should not confuse users who navigate by document structure.

## Custom properties, debugging, and architecture

### 65. How do custom properties differ from preprocessor variables?

Custom properties participate in the browser cascade and can vary by element at runtime. Preprocessor variables are generally replaced before the browser receives the stylesheet.

### 66. What does a var() fallback do?

It supplies a value when the referenced custom property is missing or invalid as a custom property. It does not necessarily rescue a value that exists but is invalid for the consuming property.

### 67. How can a CSS bug be debugged efficiently?

Reproduce the issue, inspect the element and ancestors, find the winning declaration, test one change in developer tools, and verify the fix across nearby sizes and states.

### 68. Which browser tool panels are useful for CSS work?

Elements or Inspector helps trace styles and layout. Console exposes errors and accepts small checks. Network confirms stylesheet loading. Performance records rendering and interaction costs.

### 69. How can horizontal overflow be investigated?

Find the element extending beyond the viewport. Check its fixed dimensions, content wrapping, intrinsic size, grid minimums, and positioning. Fix the source rather than hiding the overflow globally.

### 70. Which CSS properties are good starting points for animation?

Transform and opacity often avoid repeated layout, but browser behavior depends on the page and device. Measure the real interaction and honor reduced-motion preferences.

### 71. What does will-change do?

It hints that a property may change, allowing the browser to prepare. Use it sparingly and only when measurement supports it because preparation can use extra memory.

### 72. What is CSS containment?

Containment limits how some layout, style, or paint effects can affect surrounding content. It can improve isolation but changes layout behavior, so apply it only after checking the component.

### 73. When is content-visibility: auto useful?

It can defer rendering work for offscreen sections in long pages. Provide a reasonable intrinsic size and test scrolling, navigation, search, and assistive technology.

### 74. How can CSS specificity be kept manageable?

Use short component classes, a consistent layer order, and shallow selector nesting. Avoid selectors that encode long paths through the document.

### 75. What belongs in a CSS custom property?

Use one for a meaningful value that is shared or expected to vary at runtime, such as a theme color or spacing scale. Keep isolated values local when a shared token would add needless indirection.

### 76. How should browser support be checked?

Check current compatibility data for the exact property and value, then test target browsers. A feature query can help when a fallback preserves the essential content and interaction.

### 77. What should a CSS review verify?

Check selector scope, cascade behavior, responsive layouts, keyboard focus, text zoom, contrast, browser support, and whether any temporary debugging styles remain.

### 78. Why should layout be tested with real content?

Real text lengths, missing images, translated labels, and varied data can change intrinsic sizes and reveal overflow that short placeholder content did not expose.
