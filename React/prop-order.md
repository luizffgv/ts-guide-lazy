# JSX Prop order

In JSX, props should be passed in a consistent order. This makes scanning for
specific props faster, and ensures consistent writing and resolution of
conflicts.

=== ESLint Rule

I suggest using the **eslint-plugin-react** rule
[react/jsx-sort-props](https://github.com/jsx-eslint/eslint-plugin-react/blob/master/docs/rules/jsx-sort-props.md).
Feel free to choose the order that makes the most sense to you and your team.

===

[!ref target="blank" text="react/jsx-sort-props"](https://github.com/jsx-eslint/eslint-plugin-react/blob/master/docs/rules/jsx-sort-props.md)

## Personal preference

I prefer to order props in ascending alphabetical order, with `className`, `ref`
and `style` first and with callbacks last, for example:

```tsx
<Button
  aria-label="Delete"
  className="rounded-xl"
  color="primary"
  disabled
  size="small"
  onClick={handleClick}
>
  <TrashIcon />
</Button>
```

=== Rationale

I order props in this way because it makes sense to me. They are closely relatd
to this way of subjectively splitting them, while still being objective:

1. **Meta**: Props that aren't specific to the component, instead being standard
   like `className`, `ref`, and `style`.
2. **What it displays**: Props that define the component's appearance or what it
   displays.
3. **How it behaves**: Props that define how the component behaves, like
   callbacks.

This logic separation is obviously subjective and impossible to enforce
consistently, so the ESLint rule is very encouraged to avoid conflicts while
still resembling this separation.

===
