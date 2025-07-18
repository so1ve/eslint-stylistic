---
title: no-multi-spaces
rule_type: layout
related_rules:
  - key-spacing
  - space-infix-ops
  - space-in-brackets
  - space-in-parens
  - space-after-keywords
  - space-unary-ops
  - space-return-throw-case
---

# no-multi-spaces

Multiple spaces in a row that are not used for indentation are typically mistakes. For example:

```js

if(foo  === "bar") {}

```

It's hard to tell, but there are two spaces between `foo` and `===`. Multiple spaces such as this are generally frowned upon in favor of single spaces:

```js

if(foo === "bar") {}

```

## Rule Details

This rule aims to disallow multiple whitespace around logical expressions, conditional expressions, declarations, array elements, object properties, sequences and function parameters.

Examples of **incorrect** code for this rule:

::: incorrect

```js
/* eslint @stylistic/no-multi-spaces: "error" */

var a =  1;

if(foo   === "bar") {}

a <<  b

var arr = [1,  2];

a ?  b: c
```

:::

Examples of **correct** code for this rule:

::: correct

```js
/* eslint @stylistic/no-multi-spaces: "error" */

var a = 1;

if(foo === "bar") {}

a << b

var arr = [1, 2];

a ? b: c
```

:::

## Options

This rule's configuration consists of an object with the following properties:

- `"ignoreEOLComments": true` (defaults to `false`) ignores multiple spaces before comments that occur at the end of lines
- `"exceptions": { "Property": true, "ImportAttribute": true }` (`"Property"` and `"ImportAttribute"` are the nodes specified by default) specifies nodes to ignore
- `"includeTabs": false` (defaults to `true`) consider multiple tabs or spaces mixed with tabs as multiple spaces

### ignoreEOLComments

Examples of **incorrect** code for this rule with the `{ "ignoreEOLComments": false }` (default) option:

::: incorrect

```js
/* eslint @stylistic/no-multi-spaces: ["error", { ignoreEOLComments: false }] */

var x = 5;      // comment
var x = 5;      /* multiline
 * comment
 */
```

:::

Examples of **correct** code for this rule with the `{ "ignoreEOLComments": false }` (default) option:

::: correct

```js
/* eslint @stylistic/no-multi-spaces: ["error", { ignoreEOLComments: false }] */

var x = 5; // comment
var x = 5; /* multiline
 * comment
 */
```

:::

Examples of **correct** code for this rule with the `{ "ignoreEOLComments": true }` option:

::: correct

```js
/* eslint @stylistic/no-multi-spaces: ["error", { ignoreEOLComments: true }] */

var x = 5; // comment
var x = 5;      // comment
var x = 5; /* multiline
 * comment
 */
var x = 5;      /* multiline
 * comment
 */
```

:::

### exceptions

To avoid contradictions with other rules that require multiple spaces, this rule has an `exceptions` option to ignore certain nodes.

This option is an object that expects property names to be AST node types as defined by [ESTree](https://github.com/estree/estree). The easiest way to determine the node types for `exceptions` is to use [AST Explorer](https://ast-explorer.dev/) with the espree parser.

The `Property` and `ImportAttribute` node types are ignored by default, because for the [key-spacing](key-spacing) rule some alignment options require multiple spaces in properties of object literals and import attributes.

Examples of **correct** code for the default `"exceptions": { "Property": true, "ImportAttribute": true }` option:

::: correct

```js
/* eslint @stylistic/no-multi-spaces: "error" */
/* eslint @stylistic/key-spacing: ["error", { align: "value" }] */

var obj = {
    first:  "first",
    second: "second"
};
```

:::

Examples of **incorrect** code for the `"exceptions": { "Property": false }` option:

::: incorrect

```js
/* eslint @stylistic/no-multi-spaces: ["error", { exceptions: { "Property": false } }] */
/* eslint @stylistic/key-spacing: ["error", { align: "value" }] */

var obj = {
    first:  "first",
    second: "second"
};
```

:::

Examples of **correct** code for the `"exceptions": { "BinaryExpression": true }` option:

::: correct

```js
/* eslint @stylistic/no-multi-spaces: ["error", { exceptions: { "BinaryExpression": true } }] */

var a = 1  *  2;
```

:::

Examples of **correct** code for the `"exceptions": { "VariableDeclarator": true }` option:

::: correct

```js
/* eslint @stylistic/no-multi-spaces: ["error", { exceptions: { "VariableDeclarator": true } }] */

var someVar      = 'foo';
var someOtherVar = 'barBaz';
```

:::

Examples of **correct** code for the `"exceptions": { "ImportDeclaration": true }` option:

::: correct

```js
/* eslint @stylistic/no-multi-spaces: ["error", { exceptions: { "ImportDeclaration": true } }] */

import mod          from 'mod';
import someOtherMod from 'some-other-mod';
```

:::

### includeTabs

Consider multiple tabs (`\t`) or spaces mixed with tabs as multiple spaces for this rule. This option defaults to `true`.

Example of **incorrect** code for this rule with the `{ "includeTabs": true }` option:

::: incorrect

```js
/* eslint @stylistic/no-multi-spaces: ["error", { "includeTabs": true }] */

var a =	 1 +		2;
```

:::

## When Not To Use It

If you don't want to check and disallow multiple spaces, then you should turn this rule off.
