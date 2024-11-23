# Functions

## Always use objects as parameters

Functions that have parameters should always have a single (object) parameter
instead of multiple parameters, this makes refactoring easier and makes it
easier to know what each argument is at a glance.

+++ :icon-check-circle: Good

```js
function insertMany({ value, index, count }) {
  /* ... */
}

insertMany({
  value: "foo",
  index: 2,
  count: 3,
});
```

This invocation makes it clear that we are inserting the value `"foo"` at index
`2` and we are inserting it `3` times.

+++ :icon-circle-slash: Bad

```js
function insertMany(value, index, count) {
  /* ... */
}

insertMany("foo", 2, 3);
```

This invocation is less clear about what each argument is, requiring the reader
to see the function definition or enable inlay hints.

+++
