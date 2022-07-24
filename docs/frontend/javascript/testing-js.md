## Jest

-   `--u`
-   `-i`

npm tests

-   need to pass `--`
    -   npm test -- -u -t="ColorPicker"


### Expect an error

Wrap it in an anon function

```javascript
test(‘’, () => {
  expect(() => {
    calculateSquare());
  }).toThrow(‘You must provide a number’);
})
```