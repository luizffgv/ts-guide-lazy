# Discoverability

Discoverability across a codebase refers to how easy it is to locate specific
functionalities.

## What is greppability

One metric related to discoverability is greppability. Greppability is a measure
of how easy it is to find something in a codebase using textual search. The
linked article below explains this concept in detail.

[!ref text="Greppability is an underrated code metric"](https://morizbuesing.com/blog/greppability-code-metric/)

### Greppability in file names

One place where greppability is important is in the naming of files. In Visual
Studio Code and I assume other editors, it's possible to navigate to a specific
file via the `CTRL+P` command.

If you have an application that has many dashboards, it's likely that they'll
define components with similar names and functions. For example, assume each
dashboard defines components named `Filter` and `Results`. You should specify
which dashboard each component is related to, like `CodeMetricsFilter` and
`CodeMetricsResults`. This way, you can easily differentiate their editor tabs
from other tabs, and also find them quickly via keyboard shortcuts.

## Discoverability for React

React applications are mostly dominated by React concepts such as components,
hooks, and context. Each should be easily identifiable in the codebase.

### Components

Our component file naming conventions allows components to be quickly identified
across the codebase. View the page below for more information.

[!ref target="blank"]("/react/components")

### Hooks

Files that export hooks should be named like the hook, including the `use-`
prefix. This way, you can easily identify hooks.

### Contexts

!!!secondary Incomplete

This is an incomplete section that still needs work.

!!!
