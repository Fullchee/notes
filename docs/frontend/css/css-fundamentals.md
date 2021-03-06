## [Inheritance](https://courses.joshwcomeau.com/css-for-js/01-rendering-logic-1/01-built-ins-and-inheritance)

like JS prototypal inheritance

```css
<main style="color: black;">
  <p style="color: red;">
    Hello <span>World</span>
  </p>
</main>
```

```javascript
class Main {
    color = "black";
}
class Paragraph extends Main {
    backgroundColor = "red";
}
class Span extends Paragraph {}
const s = new Span();
console.log(s.color);
```

```css
a {
    color: inherit; /* force inheritance */
}
```

### `initial` vs `unset`

-   initial: browser default
-   unset: ignore current, inherit from ancestor

### Cascade analogy

Death match between classes

The property with the most specificity emerges victorious

## Scroll bars

### Always show scroll bars on mac!

Why

-   by default, scroll bars are always visible on non-macs

### Why are pixels inaccessible for font-size?

[List of CSS mistakes](https://wiki.csswg.org/ideas/mistakes)

Downside of `inline-block`

-   it doesn't word wrap

## [Overflow](https://courses.joshwcomeau.com/css-for-js/02-rendering-logic-2/14-overflow)

-   `auto` is amazing
    -   use if it MIGHT scroll
-   use `scroll` if you know if it 100% will scroll
-   `hidden`

    -   always add a comment explaining why you're using `hidden`
    -   technically: it does `scroll` and removes the scrollbars
    -   use cases

        -   truncate text with elipses
        -   artistic/decorative purposes

            -   ![b1c377c5de363ba8c6064889e2d9f6fd.png](../b1c377c5de363ba8c6064889e2d9f6fd.png)

        -   solve specific problems
            -   ![6279ff3f7c7ff1aa8ec781a1fc9a36c8.png](../6279ff3f7c7ff1aa8ec781a1fc9a36c8.png)

### [Can't hide the overflow only on one axis](https://courses.joshwcomeau.com/css-for-js/02-rendering-logic-2/14-overflow#scroll-containers)

Scroll containers!

Setting overflow to non-visible turns an element into a scroll container

```css
overflow-x: hidden;
overflow-y: visible;
```

![de9ff42109765ccb58504230868356c2.png](../de9ff42109765ccb58504230868356c2.png)

## Images

Get an image from Unsplash

-   https://source.unsplash.com/random/300??300

### Clip path

```css
clip-path: polygon(0 0, 100% 0, 100% 100%, 0 100%);
clip-path: polygon(50% 0, 100% 50%, 50% 100%, 0 50%);
```

-   https://developer.mozilla.org/en-US/docs/Web/CSS/clip-path
-   https://codepen.io/Fullchee/pen/vYpqoOL
-   ![452a9d50f93ea6ccb6066564394f2818.png](../452a9d50f93ea6ccb6066564394f2818.png)

## Tooltip

-   Basic tooltip that rises from the text
    -   <https://codepen.io/Fullchee/pen/gOoNVmW>
    -   ![Image not found: d097e5540a0600370559549ecc2ea03d.png](../d097e5540a0600370559549ecc2ea03d.png "Image not found: d097e5540a0600370559549ecc2ea03d.png")

### Accessible tooltip

## Modal

-   `aside` has better support than `dialog`

1. dialog tag that's a sibling to the main content
2. blur, decrease contrast and brightness on the main when there's a de-emphasized class on the main content
   filter: blur(3px) contrast(0.8) brightness(0.8)
3. animation

## Box shadow

```css
box-shadow: 1px 2px 3px 4px grey;
```

1. a grey background is drawn with the same size and position as our element

2. moved 1px to the right and 2 px down

3. blurred by 3px

4. spread by 4px (makes your blur start further out)

5. Clip the shadow where the shadows and the element intersect

![6c759c7b2c4ec32d9974357c2a7f72b8.png](6c759c7b2c4ec32d9974357c2a7f72b8.png "6c759c7b2c4ec32d9974357c2a7f72b8.png")

## Pseudo-elements

`::before` and `::after`

-   can't add them to [replaced elements](https://developer.mozilla.org/en-US/docs/Web/CSS/Replaced_element)
    -   whose contents can't be changed

### What problem does tailwind solve?

maintainability

have an exhaustive list of utility classes

no duplicate styles

No need to install Bootstrap, then BEM in another part

Good for learning about good design practices
Default design system that can be modified

### When is a new stacking context created?

position: not the default static and has a z index

element has opacity less than 1

transforms, filters,
