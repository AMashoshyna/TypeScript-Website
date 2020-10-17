---
display: "Перевірка JS"
oneline: "Перевірити типи у .js-файлах проєкту"
---

Працює в тандемі з `allowJs`. Коли увімкнено функцію `checkJs`, виводяться повідомлення про помилки у файлах на JavaScript. Це еквівалент `// @ ts-check` на початку всіх JavaScript-файлів вашого проєкту.

Наприклад, відповідно до визначення типу `parseFloat`, яке існує з TypeScript, цей JavaScript-код є помилковим:

```js
// parseFloat only takes a string
module.exports.pi = parseFloat(3.124);
```

Після імпорту у модуль на TypeScript:

```ts twoslash
// @allowJs
// @filename: constants.js
module.exports.pi = parseFloat(3.124);

// @filename: index.ts
import { pi } from "./constants";
console.log(pi);
```

Так помилок не буде. Але якщо увімкнути `checkJs`, то ви побачите помилку у JavaScript-файлі.

```ts twoslash
// @errors: 2345
// @allowjs: true
// @checkjs: true
// @filename: constants.js
module.exports.pi = parseFloat(3.124);

// @filename: index.ts
import { pi } from "./constants";
console.log(pi);
```
