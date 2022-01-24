### Auto-fill vs Auto-fit

**Auto-fill**
* ![922ec503ac8c417fa3ba5fc6153c4e82.png](922ec503ac8c417fa3ba5fc6153c4e82.png)
* adds new empty columns that occupy space

**auto-fit**
* ![a58ffd7243a8a657fdc3b1e5d5a8f655.png](a58ffd7243a8a657fdc3b1e5d5a8f655.png)
* make the columns fit the space
* empty columns occupy no space


## CSS Grid: 1fr vs auto
* ????

### [Inline content separators](https://medium.com/@mandy.michael/you-dont-need-a-media-query-for-that-1-inline-content-separators-a9c562a597a6)

* ![a0e93e7fc4e12ce32b05d5bb73386607.png](a0e93e7fc4e12ce32b05d5bb73386607.png)
* ![916f43045c6b45731a9e9c76b6afd4ae.png](916f43045c6b45731a9e9c76b6afd4ae.png)


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
