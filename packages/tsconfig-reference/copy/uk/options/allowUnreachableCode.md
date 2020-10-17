---
display: "Дозволити недосяжний код"
oneline: "Код, що ніколе не буде виконаний, викличе помилку"
---

У таких випадках, як:

- `undefined` (значення за замовчуванням) редактор показує рекомендації у формі попереджень
- `true` недосяжний код ігнорується
- `false` викликає помилки компіляції через недосяжний код

Ці попередження стосуються лише коду, який виявляється недосяжним через використання синтаксису JavaScript, наприклад:

```ts
function fn(n: number) {
  if (n > 5) {
    return true;
  } else {
    return false;
  }
  return true;
}
```

Із `"allowUnreachableCode": false`:

```ts twoslash
// @errors: 7027
// @allowUnreachableCode: false
function fn(n: number) {
  if (n > 5) {
    return true;
  } else {
    return false;
  }
  return true;
}
```

Це не впливає на помилки щодо коду, який _здається_ недоступним на основі аналізу типів.
