# Import order

Imports should be sorted in a consistent order, with third-party modules first,
followed by modules from your organization, then custom path aliases set up in
your project, and finally local imports.

=== Prettier plugin

The recommended way for automatically sorting imports is through a Prettier
plugin named **prettier-plugin-sort-imports**.

A recommended configuration is something like:

```json
{
  "prettier": {
    "plugins": ["prettier-plugin-sort-imports"],
    "importOrder": [
      "<THIRD_PARTY_MODULES>",
      "^@your-organization/(.*)$",
      "^@path-alias-1/(.*)$",
      "^@path-alias-2/(.*)$",
      "^@path-alias-N/(.*)$",
      "^[./]"
    ],
    "importOrderSeparation": true,
    "importOrderSortSpecifiers": true
  }
}
```

[!ref target="blank"](https://github.com/trivago/prettier-plugin-sort-imports)

===
