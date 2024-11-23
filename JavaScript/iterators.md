# Iterators

## Avoid `.forEach`

Avoid using `.forEach` when you can use the **for...of** statement.

**for...of** can be faster, more consistent across different iterables, allows
you to use `break`, `continue`, and `return`, and works better with type
narrowing.

You can use **eslint-plugin-unicorn**'s **no-array-for-each** ESLint rule to
detect and fix `.forEach` calls.

[!ref target="blank" text="no-array-for-each"](https://github.com/sindresorhus/eslint-plugin-unicorn/blob/main/docs/rules/no-array-for-each.md)
