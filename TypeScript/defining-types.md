# Defining types

## Variants

Enums should be used when declaring variants based on a fixed set of values.

+++ :icon-check-circle: Good

```ts
export enum Variant {
  DEFAULT = "primary",
  PRIMARY = "primary",
  SECONDARY = "secondary",
  TERTIARY = "tertiary",
}

type Props = {
  variant: Variant;
};

export declare function Button(props: Props): JSX.Element;
```

Here the enum constants are implementation details.

+++ :icon-circle-slash: Bad

```ts
export type Variant = "primary" | "secondary" | "tertiary";

type Props = {
  variant: Variant;
};

export declare function Button(props: Props): JSX.Element;
```

+++

!!! Don't replace enums by arrays or objects with const assertions

Enums can be replaced by arrays or objects with const assertions, which are
straightforward and don't introduce as many abstractions and implementation
details as enums do, but they are less type-safe because the type checking is
based on the values themselves rather than which enum was used. Enums have type
checking even if the underlying constant is the same.

Let's see an example enum and two ways of replacing it.

Original enum:

```ts
export enum Variants {
  Primary = "primary",
  Secondary = "secondary",
  Tertiary = "tertiary",
}
```

+++ Replaced by array

```ts
export const VARIANTS = ["primary", "secondary", "tertiary"] as const;

export type Variant = (typeof VARIANTS)[number];
```

Resulting type:

```ts
type Variant = "primary" | "secondary" | "tertiary";
```

+++ Replaced by object

```ts
export const VARIANTS = {
  primary: "primary",
  secondary: "secondary",
  tertiary: "tertiary",
} as const;

export type Variant = (typeof VARIANTS)[keyof typeof VARIANTS];
```

Resulting type:

```ts
type Variant = "primary" | "secondary" | "tertiary";
```

+++

!!!

## Type parameters

Generic type parameters should be prefixed by `T` and should be in PascalCase.

Good names include `TName`, `TFunctionMap`, `TRootState`.

Bad names include `Name` (not prefixed by `T`), and `TfunctionMap`
(`functionMap` not in PascalCase).

=== ESLint Rule

This can be enforced using the **@typescript-eslint/naming-convention** ESLint
rule.

```json
{
  "rules": {
    "@typescript-eslint/naming-convention": [
      "warn",
      {
        "selector": "typeParameter",
        "format": ["PascalCase"],
        "prefix": ["T"]
      }
    ]
  }
}
```

[!ref target="blank" text="naming-convention"](https://typescript-eslint.io/rules/naming-convention/)

===

## Properties with function types

### Avoid arrow function syntax

Properties with function type declarations should not use the arrow function
syntax.

+++ :icon-check-circle: Good

```ts
type Foo = {
  bar(): void;
  baz(qux: BazProps): void;
};
```

+++ :icon-circle-slash: Bad

```ts
type Foo = {
  bar: () => void;
  baz: (qux: BazProps) => void;
};
```

+++

## Function parameters

Functions that take a single object parameter (which are encouraged by this
guide) should define a type for that object. That type should have the name of
the function in **PascalCase** with pre `Props` suffix.

+++ :icon-check-circle: Good

```ts
type InsertManyProps = {
  value: string;
  index: number;
  count: number;
};

function insertMany({ value, index, count }: InsertManyProps) {
  /* ... */
}
```

+++ :icon-circle-slash: Bad

```ts
// This type has the wrong name
type InsertProps = {
  value: string;
  index: number;
  count: number;
};

function insertMany({ value, index, count }: InsertProps) {
  /* ... */
}
```

+++

### Avoid inline types for destructured parameters

+++ :icon-check-circle: Good

```ts
type InsertManyProps = {
  value: string;
  index: number;
  count: number;
};

function insertMany({ value, index, count }: InsertManyProps) {
  /* ... */
}
```

Functions taking more than one parameter are discouraged, but if used, inline
types are allowed when they are simple enough:

```ts
function insert(value: string, index: number) {
  /* ... */
}
```

Simple types are primitive types, like `string`, `number`, `boolean`, generic
types, such as `Array<T>` and `Record<string, number>`, and interfaces, classes
and type aliases.

Union types, intersection types and custom object types should be used through
type aliases.

+++ :icon-circle-slash: Bad

```ts
function insertMany({
  value,
  index,
  count,
}: {
  value: string;
  index: number;
  count: number;
}) {
  /* ... */
}
```

+++
