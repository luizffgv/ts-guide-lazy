# JSDoc

JSDoc is a standard for documenting JavaScript code, often associating comments
with functions, classes, types and variables.

## Ensure consistency

To reduce decisions and ensure consistency, it's recommended to use a tool like
[eslint-plugin-jsdoc](https://www.npmjs.com/package/eslint-plugin-jsdoc).

=== Recommended base rules

Here's a complete **eslint-plugin-jsdoc** ruleset that treats plain incorrect
JSDoc as errors and warns about stylistic choices:

```json
{
  "rules": {
    "jsdoc/check-access": "error",
    "jsdoc/check-alignment": "warn",
    "jsdoc/check-examples": "off",
    "jsdoc/check-indentation": "warn",
    "jsdoc/check-line-alignment": "off",
    "jsdoc/check-param-names": "error",
    "jsdoc/check-template-names": "error",
    "jsdoc/check-property-names": "error",
    "jsdoc/check-syntax": "error",
    "jsdoc/check-tag-names": "error",
    "jsdoc/check-types": "error",
    "jsdoc/check-values": "error",
    "jsdoc/empty-tags": "error",
    "jsdoc/implements-on-classes": "error",
    "jsdoc/informative-docs": "warn",
    "jsdoc/match-description": "off",
    "jsdoc/multiline-blocks": "warn",
    "jsdoc/no-bad-blocks": "warn",
    "jsdoc/no-blank-block-descriptions": "warn",
    "jsdoc/no-defaults": "off",
    "jsdoc/no-missing-syntax": "off",
    "jsdoc/no-multi-asterisks": ["warn", { "allowWhitespace": true }],
    "jsdoc/no-restricted-syntax": "off",
    "jsdoc/no-types": "error",
    "jsdoc/no-undefined-types": "off",
    "jsdoc/require-asterisk-prefix": "warn",
    "jsdoc/require-description": "off",
    "jsdoc/require-description-complete-sentence": " off",
    "jsdoc/require-example": "off",
    "jsdoc/require-file-overview": "off",
    "jsdoc/require-hyphen-before-param-description": ["warn", "never"],
    "jsdoc/require-jsdoc": "off",
    "jsdoc/require-param": "off",
    "jsdoc/require-param-description": "error",
    "jsdoc/require-param-name": "error",
    "jsdoc/require-param-type": "off",
    "jsdoc/require-property": "off",
    "jsdoc/require-property-description": "error",
    "jsdoc/require-property-name": "error",
    "jsdoc/require-property-type": "off",
    "jsdoc/require-returns": "off",
    "jsdoc/require-returns-check": "error",
    "jsdoc/require-returns-description": "error",
    "jsdoc/require-returns-type": "off",
    "jsdoc/require-template": "off",
    "jsdoc/require-throws": "off",
    "jsdoc/require-yields": "off",
    "jsdoc/require-yields-check": "error",
    "jsdoc/sort-tags": "warn",
    "jsdoc/tag-lines": "warn",
    "jsdoc/valid-types": "error"
  }
}
```

===
