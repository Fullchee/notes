# SVG


```css
M 213.1,6.7
```

* Move to (don't draw anything)

upper case: absolute
lower case: relative

```css
c -32.4-14.4-73.7,0-88.1,30.6
```
* curve 
https://css-tricks.com/svg-path-syntax-illustrated-guide/


```css
z
```

closes the path


| **M**x,y       | Move to the absolute coordinates x,y                                                                      |
|----------------|-----------------------------------------------------------------------------------------------------------|
| **m**x,y       | Move to the right x and down y (or left and up if negative values)                                        |
| **L**x,y       | Draw a straight line to the absolute coordinates x,y                                                      |
| **l**x,y       | Draw a straight line to a point that is relatively right x and down y (or left and up if negative values) |
| **H**x         | Draw a line horizontally to the exact coordinate x                                                        |
| **h**x         | Draw a line horizontally relatively to the right x (or to the left if a negative value)                   |
| **V**y         | Draw a line vertically to the exact coordinate y                                                          |
| **v**y         | Draw a line vertically relatively down y (or up if a negative value)                                      |
| **Z**(or**z**) | Draw a straight line back to the start of the path                                                        |

