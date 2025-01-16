# Memoization

## When to use `useMemo`

### Replacing `useEffect` for transformations and `useState` for derived state

Sometimes, you may find a `useEffect` that is not really _interacting_ with
anything else, just updating one or more dependent states based on other
states/props.

If the dependent states are always updated along with the state/prop they depend
on, you can replace the `useState`s and the `useEffect`s with `useMemo`s to
calculate the derived states.

This prevents unnecessary re-renders and cascading effects. Be sure to check out
the official React guide on this topic, as it provides the same reasoning as
mine.

[!ref target="blank" text="Updating state based on props or state"](https://react.dev/learn/you-might-not-need-an-effect#updating-state-based-on-props-or-state)

+++ :icon-circle-slash: Bad

```tsx
export function Books() {
  const books = useBooks();

  const [nameFilter, setNameFilter] = useState("");

  const [filteredBooks, setFilteredBooks] = useState(books);

  useEffect(() => {
    setFilteredBooks(books.filter((book) => book.name.includes(nameFilter)));
  }, [books, nameFilter]);

  return (
    <>
      <SearchInput value={nameFilter} onChange={setNameFilter} />
      <BooksList books={filteredBooks} />
    </>
  );
}
```

The code above is bad because after the search input changes or the list of
books changes, the `<BooksList>` child component still renders once with the old
filtered books before the effect runs and the new `<BooksList>` is rendered and
committed. That one render with outdated data can be problematic in some cases.

+++ :icon-check-circle: Good

```tsx
export function Books() {
  const books = useBooks();

  const [nameFilter, setNameFilter] = useState("");

  const filteredBooks = useMemo(
    () => books.filter((book) => book.name.includes(nameFilter)),
    [books, nameFilter],
  );

  return (
    <>
      <SearchInput value={nameFilter} onChange={setNameFilter} />
      <BooksList books={filteredBooks} />
    </>
  );
}
```

Here the `filteredBooks` is calculated with `useMemo` and is always up-to-date
before `<BooksList>` is rendered. This way, `<BooksList>` never renders with an
outdated list of books.

+++

## When to use `useCallback`

`useCallback` returns a memoized version of a callback function that only
changes if one of the dependencies has changed. This makes it useful to avoid
re-renders of child components and recalculations that depend on the callback
every time the parent component renders.

### Callbacks that are passed to child components

When you pass a callback to a child component, you should wrap it in
`useCallback` because it may prevent unnecessary re-renders of the child
component and recalculations inside that component.

+++ :icon-check-circle: Good

```tsx
export function Counter() {
  const [count, setCount] = useState(0);

  const increment = useCallback(() => {
    setCount((c) => c + 1);
  }, []);

  const decrement = useCallback(() => {
    setCount((c) => c - 1);
  }, []);

  return <Controls increment={increment} decrement={decrement} />;
}
```

In this example, `increment` and `decrement` are wrapped in `useCallback`
because `Controls` may be wrapped in `React.memo`, or have effects or
memoization hooks that have the callback in their dependency array, which
present recalculations that can be avoided by memoizing the callbacks.

+++ :icon-circle-slash: Bad

```tsx
export function Counter() {
  const [count, setCount] = useState(0);

  const increment = () => {
    setCount((c) => c + 1);
  };

  const decrement = () => {
    setCount((c) => c - 1);
  };

  return <Controls increment={increment} decrement={decrement} />;
}
```

The code above is bad because `Controls` will re-render every time `Counter` is
rendered, and hook in `Controls` that depends on `increment` or `decrement` will
recalculate every time as they are different functions every time.

+++

### Callbacks that are passed to dependency arrays

When you pass a callback to a dependency array of a hook, you should wrap it in
`useCallback` to avoid unnecessary effect executions and recalculations.

+++ :icon-check-circle: Good

```tsx
export function ProductProvider({ children, productId }) {
  const favoriteProduct = useCallback(async () => {
    await api.favoriteProduct(productId);
  }, [productId]);

  export const value = useMemo(() => ({ favoriteProduct }), [favoriteProduct]);

  return (
    <ProductContext.Provider value={value}>{children}</ProductContext.Provider>
  );
}
```

The code above allows the `ProductProvider` to rerender as many times as it
needs without causing recalculations in components that depend on the
`ProductContext`, because `favoriteProduct` is memoized with `useCallback` and
`value` is memoized with `useMemo`.

If `favoriteProduct` was not memoized with `useCallback`, it would be a
different function every time `ProductProvider` rerenders, causing `value` to be
a different object every time.

+++ :icon-circle-slash: Bad

```tsx
export function ProductProvider({ children, productId }) {
  const favoriteProduct = async () => {
    await api.favoriteProduct(productId);
  };

  export const value = useMemo(() => ({ favoriteProduct }), [favoriteProduct]);

  return (
    <ProductContext.Provider value={value}>{children}</ProductContext.Provider>
  );
}
```

The provider above is bad because every component that depends on
`ProductContext` will rerender or do recalculations every time `ProductProvider`
rerenders, as even though `value` is memoized with `useMemo`, `favoriteProduct`
is a different function every time.

+++

### When to avoid `useCallback`

Avoid `useCallback` when the callback is not used in any dependency array, and
is only used in native components such as an `<a>` or `<button>`. Native tags
don't have possibly complex logic that can be avoided by memoizing the callback.
