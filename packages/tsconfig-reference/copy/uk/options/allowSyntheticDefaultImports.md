---
display: "Дозволити синтетичні імпорти за замовчуванням"
oneline: "Дозволяє 'import x from y' для модулів, що не мають експорту за замовчуванням"
---

Активована опція `allowSyntheticDefaultImports` дозволяє писати імпорти так:

```ts
import React from "react";
```

instead of:

```ts
import * as React from "react";
```

коли модуль **не визначає** експорт за замовчуванням (default export) явно.

Наприклад, якщо `allowSyntheticDefaultImports` не дорівнює `true`:

```ts twoslash
// @errors: 1259
// @checkJs
// @allowJs
// @esModuleInterop: false
// @filename: utilFunctions.js
// @noImplicitAny: false
const getStringLength = (str) => str.length;

module.exports = {
  getStringLength,
};

// @filename: index.ts
import utils from "./utilFunctions";

const count = utils.getStringLength("Check JS");
```

Цей код викличе помилку, бо об'єкта за замовчуванням, який можна імпортувати, немає. Хоча здається, що має працювати.
Транспілятори коду, наприклад Babel, для зручності автоматично створюють експорт за замовчуванням, коли його не визначено. Модуль виглядатиме так:

```js
// @filename: utilFunctions.js
const getStringLength = (str) => str.length;
const allFunctions = {
  getStringLength,
};

module.exports = allFunctions;
module.exports.default = allFunctions;
```

Цей прапор не впливає на створені JavaScript-файли. Він потрібний лише для перевірки типів.
Ця опція робить поведінку TypeScript подібною до Babel, де створюється додатковий код, щоб зробити використання експорту з модуля за замовчуванням (default export) ергономічнішим.
