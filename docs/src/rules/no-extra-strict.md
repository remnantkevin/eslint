---
title: no-extra-strict
layout: doc
edit_link: https://github.com/eslint/eslint/edit/main/docs/src/rules/no-extra-strict.md

further_reading:
- https://es5.github.io/#C
---

Disallows strict mode directives when already in strict mode.

(removed) This rule was **removed** in ESLint v1.0 and **replaced** by the [strict](strict) rule. The `"global"` or `"function"` options in the new rule are similar to the removed rule.

The `"use strict";` directive applies to the scope in which it appears and all inner scopes contained within that scope. Therefore, using the `"use strict";` directive in one of these inner scopes is unnecessary.

```js
"use strict";

(function () {
    "use strict";
    var foo = true;
}());
```

## Rule Details

This rule is aimed at preventing unnecessary `"use strict";` directives. As such, it will warn when it encounters a `"use strict";` directive when already in strict mode.

Example of **incorrect** code for this rule:

::: incorrect

```js
"use strict";

(function () {
    "use strict";
    var foo = true;
}());
```

:::

Examples of **correct** code for this rule:

::: correct

```js
"use strict";

(function () {
    var foo = true;
}());
```

:::

::: correct

```js
(function () {
    "use strict";
    var foo = true;
}());
```

:::
