### Why `withRouter` HOC?

```js
<Route path="/movies" component={MoviesIndex} />
```

The component gets access to `this.props.history`

* so you can `history.push`

Some components (example: Header) are in every pages

* can't wrap with a `Route`

```js
export default withRouter(Header)
```

gives that component access to

* `history`
* `match`
* `location`