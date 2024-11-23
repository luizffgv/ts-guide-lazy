# Expressions

## Use strict equality

Always use the `===` (strict equality) and `!==` (strict inequality) operators
to compare two values. Using the same approach for all comparisons will make
your code more consistent and gives you one less thing to think about.

=== ESLint Rule

ESLint's **eqeqeq** rule should be enabled to enforce this. It also has a
"smart" option that allows `==` in certain conditions, and I often used it in
the past. However, using the default setting gives you more consistency and will
help everyone avoid non-productive discussions in code reviews.

[!ref target="blank"](https://eslint.org/docs/latest/rules/eqeqeq)

===

## Prefer postfix decrement/increment

When incrementing or decrementing a variable, use the prefix notation (`++i`)
unless the context requires the postfix notation (`i++`). The prefix notation is
more clear because the result of the expression has the same value as `i` after
evaluation, while in postfix notation the resulting value is outdated compared
to the new value of `i`.

+++ :icon-check-circle: Good

```js
for (let i = 0; i < 10; ++i) {
  console.log(i);
}
```

Here we don't need to defer the update to `i`, so the prefix notation is
simpler.

Now, here's an example where the postfix notation is necessary:

||| Code

```js
console.log("Counting from 1 to 5");
let i = 1;
while (i < 6) {
  console.log(i++);
}
```

||| Output

```txt
Counting from 1 to 5
1
2
3
4
5
```

|||

+++ :icon-circle-slash: Bad

```js
for (let i = 0; i < 10; i++) {
  console.log(i);
}
```

This is a bad example because we have no reason to use the postfix notation,
since deferring the update to `i` is not necessary.

Now, here's an example where the prefix notation causes a problem:

||| Code

```js
console.log("Counting from 1 to 5");
let i = 1;
while (i < 6) {
  console.log(++i);
}
```

||| Output

```txt
Counting from 1 to 5
2
3
4
5
6
```

|||

+++

## Avoid the comma operator

The comma operator allows you to evaluate a sequence of expressions as a single
expression, which results in the value of the last expression. This is a
confusing form of operation sequencing and should be avoided.

## Avoid function expressions

Arrow functions should be favored over function expressions. Arrow functions are
terser and more predictable in regards to the `this` keyword.

+++ :icon-check-circle: Good

```js
const numbers = [1, 3, 5, 7];
const sum = numbers.reduce((acc, n) => acc + n, 0);
```

+++ :icon-circle-slash: Bad

```js
const numbers = [1, 3, 5, 7];
const sum = numbers.reduce(function (acc, n) {
  return acc + n;
}, 0);
```

Function expression was used when not necessary. This is incorrect.

+++

When you need a dynamically bound `this`, function expressions may be necessary
and are therefore allowed.

## Avoid implicit coercion

Some ways to convert values to another type are obscure and should be avoided,
here are some bad examples:

```js
const hasItems = !!items.length;
const num = +str;
```

=== ESLint Rule

The **no-implicit-coercion** ESLint rule can be enabled to enforce this.

[!ref target="blank"](https://eslint.org/docs/latest/rules/no-implicit-coercion)

===

## Avoid other types when booleans are expected

In contexts where a boolean value is expected, such as an `if` condition, avoid
passing non-boolean values directly. Instead, explicitly compare the value to
something in order to make the intent clear.

Contexts in which this rule applies include conditions for `if`, `while`, `for`,
and `do-while` statements. It also applies for the operands of the logical
negation `!` operator, binary logical operators `&&` and `||`, and the first
operand for the conditional (ternary) operator.

+++ :icon-check-circle: Good

```js
declare const documents: Document[];

if (documents.length === 0) {
  console.log("No documents found");
}
```

+++ :icon-circle-slash: Bad

```js
declare const documents: Document[];

// Bad: Non-boolean passed to "!" operator
if (!documents) {
  console.log("No documents found");
}
```

=== ESLint Rule

The **strict-boolean-expressions** ESLint rule can be enabled to enforce this.

[!ref target="blank"](https://typescript-eslint.io/rules/strict-boolean-expressions/)

## Prefer nullish coalescing

Use the nullish coalescing operator (`??`) instead of the logical OR operator
(`||`) when you want a fallback value for when an expression is `null` or
`undefined`.

When you really want to check for falsy values, you may freely use the logical
OR operator.

+++ :icon-check-circle: Good

```js
declare const bar: string | null | undefined;
const foo = bar ?? "default"; // Here we are handling only null and undefined

declare const owo: string | boolean;
const awoo = owo || "default"; // OK, we are checking for falsy values
```

+++ :icon-circle-slash: Bad

```js
declare const bar: string | null | undefined;
const foo = bar || "default"; // May be bad, this will also trigger for an empty
                              // string

```

+++

=== ESLint Rule

The **prefer-nullish-coalescing** ESLint rule can be enabled to enforce this.

[!ref target="blank"](@typescript-eslint/prefer-nullish-coalescing)

===
