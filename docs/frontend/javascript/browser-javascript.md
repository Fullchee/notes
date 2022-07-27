# Browser JavaScript

## Sub-resource integrity

```html
<script src="//cdnjs....."
 integrity="sha256-..."
crossorigin="anonymous">
```

if the CDN gets hacked, then the script won't run

## [Get the URL params](https://stackoverflow.com/a/901144/8479344)

```javascript
// ?q=turtles or window.location.search
search_string = new URL("https://www.google.ca/search?q=turtles&oq=tortuga");
search_string = new URL(window.location.search);

params = new URLSearchParams(search_string);

params.get("q"); // "turtles"
```
