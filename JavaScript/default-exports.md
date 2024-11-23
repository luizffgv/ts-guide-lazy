# Avoid default exports

Default exports should **always** be avoided.

Default exports make it harder to batch rename exported values, and allows for
accidentally importing a value with a different name than expected.

Default exports also create an additional source of decisions when importing a
module, and they don't provide any concrete benefit over named exports.

This guide will not repeat what other style guides already say, instead, you can
read them for yourself and come to your own conclusions.

[!ref target="blank" text="Google TypeScript Style Guide"](https://google.github.io/styleguide/tsguide.html#exports)
[!ref target="blank" text="TypeScript Deep Dive"](https://basarat.gitbook.io/typescript/main-1/defaultisbad)
