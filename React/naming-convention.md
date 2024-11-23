---
order: 1
---

# Naming convention

Here lies the default naming convention for React code.

## Components

Variables should be in **PascalCase**.

## Contexts

Contexts should be in **PascalCase**.

!!!secondary Incomplete

This is an incomplete section that still needs work. It doesn't specify whether
contexts should be suffixed with `Context` or not.

!!!

## `setState` callback parameter

The parameter of a callback provided to `setState` callback should be named `v`.

In case the identifier `v` is already used, you should use the initials of the
state variable name. This means a state variable named `dogsCount` should mean a
callback parameter named `dc`.

+++ :icon-check-circle: Good

```tsx
const [selectedIds, setSelectedIds] = useState(0);

const handleSelect = useCallback((id: string) => {
  setSelectedIds((v) => [...v, id]);
}, []);
```

+++ :icon-circle-slash: Bad

```tsx
const [selectedIds, setSelectedIds] = useState(0);

const handleSelect = useCallback((id: string) => {
  setSelectedIds((selectedIds) => [...selectedIds, id]);
}, []);
```

+++

=== Rationale

Using arbitrary parameter names like `selectedIds` can lead to the name getting
out of sync when the actual state variable is renamed. This can cause confusion.

Using `v` or the initials of the state variable name ensures that the parameter
is never outdated, and becomes natural and quick to read after some time.

Using a descriptive name is also redundant because the state setter function
already has a name that describes the parameter.

In the exceedingly rare case where the identifier `v` is already used in a state
setter, we use the initials just to not be totally arbitrary.

===

## Event handlers

Event handlers should be in **PascalCase** and be prefixed with `handle`.

This guide doesn't consider an _event handler_ only native browser events like
`click` or `submit`, but also any callbacks that are expected to react to some
event from a child component.

+++ :icon-check-circle: Good

```tsx
export function Cart() {
  const { setItems } = useCart();

  const handleClear = useCallback(() => {
    setItems([]);
  }, [setItems]);

  return (
    <CartContainer>
      <CartItems />
      <ClearCart onClear={handleClear} />
    </CartContainer>
  );
}
```

In this example, `handleClear` is an event handler that reacts to an action from
`ClearCart`. It correctly follows the name convention.

+++ :icon-circle-slash: Bad

```tsx
export function Cart() {
  const { setItems } = useCart();

  const clearCart = useCallback(() => {
    setItems([]);
  }, [setItems]);

  return (
    <CartContainer>
      <CartItems />
      <ClearCart onClear={clearCart} />
    </CartContainer>
  );
}
```

There's nothing inherently wrong with the code above, but it doesn't follow the
convention of prefixing event handlers with `handle`.

+++

## Props that receive event handlers

Props that receive event handlers should be in **PascalCase** and be prefixed
with `on`.

+++ :icon-check-circle: Good

```tsx
export type Props = {
  onClick(): void;
};

export function Button({ onClick }: Props) {
  return <button onClick={onClick}>Click me</button>;
}
```

+++ :icon-circle-slash: Bad

```tsx
export type Props = {
  clickHandler(): void;
};

export function Button({ clickHandler }: Props) {
  return <button onClick={clickHandler}>Click me</button>;
}
```
