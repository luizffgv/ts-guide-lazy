---
order: 1
---

# Naming convention

Here lies the default naming convention for TypeScript code. The guide may
define additional rules for specific contexts. To see more, find the **Naming
convention** sections of other categories.

## Enums

Enums should be in **PascalCase** and named in singular form. Enum members
should be in **ALL_CAPS**.

Enum values have no specific convention.

+++ :icon-check-circle: Good

```ts
enum Color {
  RED = "R",
  GREEN = "G",
  BLUE = "B",
}
```

+++ :icon-circle-slash: Bad

```ts
enum Colors {
  Red = "R",
  Green = "G",
  Blue = "B",
}
```

This is bad because the enum name is not in singular form, and the enum members
are not in **ALL_CAPS**.

+++

=== ESLint Rule

The **@typescript-eslint/naming-convention** ESLint rule can be used to enforce
this.

[!ref target="blank"](https://typescript-eslint.io/rules/naming-convention/)

```json
{
  "@typescript-eslint/naming-convention": [
    "error",
    {
      "selector": ["enum"],
      "format": ["PascalCase"]
    },
    {
      "selector": ["enumMember"],
      "format": ["UPPER_CASE"]
    }
  ]
}
```

===
