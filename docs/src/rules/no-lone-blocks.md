---
title: no-lone-blocks
layout: doc
edit_link: https://github.com/eslint/eslint/edit/main/docs/src/rules/no-lone-blocks.md
rule_type: suggestion
---


In JavaScript, prior to ES6, standalone code blocks delimited by curly braces do not create a new scope and have no use. For example, these curly braces do nothing to `foo`:

```js
{
    var foo = bar();
}
```

In ES6, code blocks may create a new scope if a block-level binding (`let` and `const`), a class declaration or a function declaration (in strict mode) are present. A block is not considered redundant in these cases.

## Rule Details

This rule aims to eliminate unnecessary and potentially confusing blocks at the top level of a script or within other blocks.

Examples of **incorrect** code for this rule:

::: incorrect

```js
/*eslint no-lone-blocks: "error"*/

{}

if (foo) {
    bar();
    {
        baz();
    }
}

function bar() {
    {
        baz();
    }
}

{
    function foo() {}
}

{
    aLabel: {
    }
}

class C {
    static {
        {
            foo();
        }
    }
}
```

:::

Examples of **correct** code for this rule with ES6 environment:

::: correct

```js
/*eslint no-lone-blocks: "error"*/
/*eslint-env es6*/

while (foo) {
    bar();
}

if (foo) {
    if (bar) {
        baz();
    }
}

function bar() {
    baz();
}

{
    let x = 1;
}

{
    const y = 1;
}

{
    class Foo {}
}

aLabel: {
}

class C {
    static {
        lbl: {
            if (something) {
                break lbl;
            }

            foo();
        }
    }
}
```

:::

Examples of **correct** code for this rule with ES6 environment and strict mode via `"parserOptions": { "sourceType": "module" }` in the ESLint configuration or `"use strict"` directive in the code:

::: correct

```js
/*eslint no-lone-blocks: "error"*/
/*eslint-env es6*/

"use strict";

{
    function foo() {}
}
```

:::
