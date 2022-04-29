### [Inline content separators](https://medium.com/@mandy.michael/you-dont-need-a-media-query-for-that-1-inline-content-separators-a9c562a597a6)

* ![a0e93e7fc4e12ce32b05d5bb73386607.png](../a0e93e7fc4e12ce32b05d5bb73386607.png "a0e93e7fc4e12ce32b05d5bb73386607.png")
* ![916f43045c6b45731a9e9c76b6afd4ae.png](../916f43045c6b45731a9e9c76b6afd4ae.png "916f43045c6b45731a9e9c76b6afd4ae.png")


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


## Cut out a corner

Page dog ear

??????

```css
background: linear-gradient(-45deg, transparent 15px, blue 0)
```

