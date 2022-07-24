# Flow Layout

```css
display: inline;
display: block;
display: inline-block;
```

## Inline Elements

### Assumes it's Typography
- TODO: LINK TO TYPOGRAPHY

### Magic space at the bottom
    - ![magic-bottom-space-inline.png](magic-bottom-space-inline.png)
- `display: block`
- `line-height: 0` on the wrapping div

### no height/width

### No inline styles for pseudo-classes/elements
- inline styles are only defined in HTML
- pseudo-classes/elements are defined in CSS
- ????????

### Line wrap
- ![inline-line-wrap.png](inline-line-wrap.png)


### Inline padding-left/right

Default
```css
box-decoration-break: slice;
```

![inline-padding-left-right.png](inline-padding-left-right.png "inline-padding-left-right.png")

```css
-webkit-box-decoration-break: clone;
box-decoration-break: clone;
```

![box-decoration-break-clone.png](box-decoration-break-clone.png)

## Inline-block
- like `inline` except you can apply padding, 
- doesn't word wrap