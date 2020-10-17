---
display: "Декларації"
oneline: "Створити файли d.ts для файлів проєкту"
---

Створює файли `.d.ts` для кожного файлу на TypeScript або на JavaScript у проєкті.
Ці файли .d.ts - це файли визначення типів, які описують зовнішній інтерфейс вашого модуля.
За допомогою файлів .d.ts такі інструменти, як TypeScript, можуть забезпечувати автодоповнення та точне виведення типів для нетипізованого коду.

Коли `declaration` має значення `true`, запуск компілятора на цьому коді

```ts twoslash
export let helloWorld = "hi";
```

згенерує такий `index.js`:

```ts twoslash
// @showEmit
export let helloWorld = "hi";
```

А також відповідний `helloWorld.d.ts`:

```ts twoslash
// @showEmittedFile: index.d.ts
// @showEmit
// @declaration
export let helloWorld = "hi";
```

При роботі з `.d.ts`-файлами для JavaScript ми радимо використовувати [`emitDeclarationOnly`](#emitDeclarationOnly) або [`outDir`](#outDir), щоб попередити випадкове переписування JavaScript-файлів.
