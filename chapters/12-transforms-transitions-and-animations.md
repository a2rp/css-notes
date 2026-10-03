# 12. Transforms, transitions, and animations

[Back to notes index](../README.md)

| Previous | Notes index | Next |
| --- | --- | --- |
| [Previous: Pseudo-classes, pseudo-elements, and forms](./11-pseudo-classes-elements-and-forms.md) | [Notes index](../README.md) | [Next: Custom properties and CSS functions](./13-custom-properties-and-css-functions.md) |

## Transform without changing document flow

Transforms rotate, scale, skew, or translate an element visually. They do not move surrounding content to make room for the transformed box.

```css
.icon {
    transform: translateY(-0.1rem) rotate(-8deg);
    transform-origin: center;
}

.card:hover {
    transform: translateY(-0.2rem);
}
```

Transform functions are applied in order. `transform-origin` changes the point around which a rotation or scale occurs. The individual properties `translate`, `rotate`, and `scale` can also be used when they make the intent clearer.

A non-none transform creates a stacking context and can establish a containing block for positioned descendants. If a fixed child behaves as though it were attached to a transformed ancestor, inspect the transform on its ancestors.

## Transition between state values

A transition interpolates a property when its value changes, often because a pseudo-class matches:

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

A transition lists the properties to animate, duration, timing function, and optional delay. Prefer specific properties over `transition: all`; broad transitions can animate unintended changes and make debugging harder. Some properties cannot be smoothly interpolated.

Transitions need a before and after state. They do not create a repeated sequence or explain a change that occurs before the element is rendered.

## Define repeated motion with keyframes

Use `@keyframes` when an animation needs more than a simple state-to-state transition:

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

The animation shorthand can set a name, duration, timing function, delay, iteration count, direction, fill mode, and play state. Keep an animation finite unless repeating motion is necessary to communicate ongoing activity. A continuously moving decorative element can distract from the page.

If an animation changes the same property as another rule, the animated value participates in the cascade while the animation is active. Avoid having separate animations compete over the same property on the same element.

## Respect reduced motion

Some visitors ask their system to reduce non-essential movement. Keep essential information available without motion and remove or replace large movement, scaling, and repeated effects:

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

Reduced motion is a user preference, not a signal to hide content. A progress state can use text, a static icon, or another non-moving cue when animation is disabled.

## Keep motion efficient and useful

- Animate short, meaningful changes that help users understand state.
- Prefer `transform` and `opacity` for simple motion where possible.
- Avoid animating large areas continuously.
- Do not use motion to convey information without a text or visual alternative.
- Keep controls usable while an animation runs.
- Test with the system's reduced-motion setting enabled.

Changing layout properties such as width, height, margin, or top can cause repeated layout work. For a simple entrance or hover effect, a transform often avoids moving neighboring content. Measure before optimizing complex motion.

## Try it

1. Transition a button's background and vertical position on hover.
2. Add the matching `:focus-visible` state so keyboard users get clear feedback.
3. Change `transform-origin` on a rotating icon.
4. Replace a transition with a short keyframe animation.
5. Enable reduced motion on the device and verify that the page remains understandable.

## Common mistakes

- Using a transition on a property that changes before the element appears.
- Writing `transition: all` and animating unrelated properties.
- Repeating a large scale or pan animation indefinitely.
- Removing essential content when reduced motion is enabled.
- Assuming transformed elements keep their original stacking behavior.
- Animating layout dimensions when a transform can express the same visual effect.
- Using motion without a focus, active, or static state that communicates the same result.

## Official references

- [CSS animations](https://developer.mozilla.org/en-US/docs/Web/CSS/Guides/Animations)
- [The `transform` property](https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Properties/transform)
- [The `transition` property](https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Properties/transition)
- [The `animation` property](https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Properties/animation)
- [The `prefers-reduced-motion` media feature](https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/At-rules/%40media/prefers-reduced-motion)

| Previous | Notes index | Next |
| --- | --- | --- |
| [Previous: Pseudo-classes, pseudo-elements, and forms](./11-pseudo-classes-elements-and-forms.md) | [Notes index](../README.md) | [Next: Custom properties and CSS functions](./13-custom-properties-and-css-functions.md) |
