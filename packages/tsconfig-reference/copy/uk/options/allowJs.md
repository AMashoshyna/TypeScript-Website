---
display: "Дозволити JS"
oneline: "Дозволяє TS включати імпорт .JS-файлів"
---

Дозволяє імпортувати в проєкт не лише файли .ts та .tsx, але також JavaScript-файли. Наприклад, такий JS-файл:

```js twoslash
// @filename: card.js
export const defaultCardDeck = "Heart";
```

При імпорті у TypeScript-файл він викличе помилку:

```ts twoslash
// @errors: 2307
// @filename: card.js
module.exports.defaultCardDeck = "Heart";
// ---cut---
// @filename: index.ts
import { defaultCardDeck } from "./card";

console.log(defaultCardDeck);
```

З активованою опцією `allowJs` імпорт дозволено:

```ts twoslash
// @filename: card.js
module.exports.defaultCardDeck = "Heart";
// ---cut---
// @allowJs
// @filename: index.ts
import { defaultCardDeck } from "./card";

console.log(defaultCardDeck);
```

Цей прапор дозволяє `.ts`- та `.tsx`-файлам існувати поряд з файлами на JavaScript, тому його можна використовувати як спосіб поступово додавати TypeScript-файли до JS-проєктів.
