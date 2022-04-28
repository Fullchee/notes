### Auto-fill vs Auto-fit

**Auto-fill**
* ![922ec503ac8c417fa3ba5fc6153c4e82.png](./922ec503ac8c417fa3ba5fc6153c4e82.png)
* adds new empty columns that occupy space

**auto-fit**
* ![a58ffd7243a8a657fdc3b1e5d5a8f655.png](./a58ffd7243a8a657fdc3b1e5d5a8f655.png)
* make the columns fit the space
* empty columns occupy no space


## CSS Grid: 1fr vs auto
* ????

### [Inline content separators](https://medium.com/@mandy.michael/you-dont-need-a-media-query-for-that-1-inline-content-separators-a9c562a597a6)

* ![a0e93e7fc4e12ce32b05d5bb73386607.png](./a0e93e7fc4e12ce32b05d5bb73386607.png)
* ![916f43045c6b45731a9e9c76b6afd4ae.png](./916f43045c6b45731a9e9c76b6afd4ae.png)


```css
.container {
  overflow: hidden;
}
.entry {
  transform: translateX(-10px);
  padding-left:(10px);
}

.entry::before {
  top: 0;
  left: 0;
  width: 1px;
}
```

### Always show scroll bars on Mac
Why
* by default, scrollbars are always visible on non-macs



#### [Overflow](https://courses.joshwcomeau.com/css-for-js/02-rendering-logic-2/14-overflow)
* `auto` is amazing
    * use if it MIGHT scroll
* use `scroll` if you know if it 100% will scroll
* `hidden`
    * always add a comment explaining why you're using `hidden`
    * technically: it does `scroll` and removes the scrollbars
    * use cases
        * truncate text with elipses
        * artistic/decorative purposes
            * ![b1c377c5de363ba8c6064889e2d9f6fd.png](b1c377c5de363ba8c6064889e2d9f6fd.png)

        * solve specific problems
            * ![6279ff3f7c7ff1aa8ec781a1fc9a36c8.png](6279ff3f7c7ff1aa8ec781a1fc9a36c8.png)

##### [Can't hide the overflow only on one axis](https://courses.joshwcomeau.com/css-for-js/02-rendering-logic-2/14-overflow#scroll-containers)
Scroll containers!

Setting overflow to non-visible turns an element into a scroll container
```css
overflow-x: hidden;
overflow-y: visible;
```
![de9ff42109765ccb58504230868356c2.png](de9ff42109765ccb58504230868356c2.png)



## Images
```css
clip-path: polygon(0 0, 100% 0, 100% 100%, 0 100%);
clip-path: polygon(50% 0, 100% 50%, 50% 100%, 0 50%);
```
Clip path

https://developer.mozilla.org/en-US/docs/Web/CSS/clip-path


<https://codepen.io/Fullchee/pen/vYpqoOL>
