# Components

## One component per file

Components should be defined in a file dedicated to them, which exports nothing
else and is named like the component.

The official React docs refer to components as "reusable UI elements for your
app". Having the components in their own files make them more self-contained and
navigable.

+++ :icon-check-circle: Good

```tsx
// Button.tsx
export function Button() {
  return <button>Click me</button>;
}
```

Here the file name matches the component exactly.

+++ :icon-circle-slash: Bad

```tsx
// button.tsx
export function Button() {
  return <button>Click me</button>;
}
```

Here the file name has incorrect casing.

+++

[!ref target="blank" text="Components: UI building blocks"](https://react.dev/learn/your-first-component#components-ui-building-blocks)

## Defining prop types

Define prop types for components using either `type` or `interface`, I don't
think there's much value to be gaining in standardizing which keyword to use as
interfaces seem to have better compile performance than intersection types, but
don't allow for more precise type definitions. Declaration merging should not be
common for most component props, so it's not an important factor.

The type should be named `Props` and be exported, allowing reuse for type
checking in other modules.

+++ :icon-check-circle: Good

```tsx
export type Props = {
  onClick(): void;
};

export function Button({ onClick }: Props) {
  return <button>Click me</button>;
}
```

```tsx
export interface Props {
  onClick(): void;
}

export function Button({ onClick }: Props) {
  return <button>Click me</button>;
}
```

In the above cases the type name is correct and it is properly exported.

+++ :icon-circle-slash: Bad

```tsx
export interface Prop {
  onClick(): void;
}

export function Button({ onClick }: Props) {
  return <button>Click me</button>;
}
```

```tsx
type Props = {
  onClick(): void;
};

export function Button({ onClick }: Props) {
  return <button>Click me</button>;
}
```

In the above cases the type name is either not exported or named incorrectly
(`Prop`).

+++
