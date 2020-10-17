---
display: "Downlevel Iteration"
oneline: "Для ітерації об'єктів генерувати більш сумісний, але багатослівний JavaScript"
---

Downleveling або пониження рівня - це термін, який TypeScript використовує для транспіляції у стару версію JavaScript.
Цей прапор надає підтримку для більш точної реалізації того, як сучасний JavaScript ітерує об'єкти у старих середовищах JavaScript.

ECMAScript 6 додав кілька нових примітивів ітерацій: цикл `for / of` (`for (el of arr)`), розбір масиву (`[a, ... b]`), розбір аргументів (`fn (... args)`) та`Symbol.iterator`.
`--downlevelIteration` дозволяє більш точно використовувати ці примітивні ітерації в середовищах ES5, де присутня реалізація `Symbol.iterator`.

#### Приклад: зміни до `for / of`

Без прапора `downlevelIteration` цикл `for / of` на будь-якому об'єкті перетворюється на традиційний цикл `for`:

```ts twoslash
// @target: ES5
// @showEmit
const str = "Hello!";
for (const s of str) {
  console.log(s);
}
```

This is often what people expect, but it's not 100% compliant with ECMAScript 6 behavior.
Certain strings, such as emoji (😜), have a `.length` of 2 (or even more!), but should iterate as 1 unit in a `for-of` loop.
See [this blog post by Jonathan New](https://blog.jonnew.com/posts/poo-dot-length-equals-two) for a longer explanation.

Часто люди саме цього і очікують, але це не на 100% відповідає поведінці ECMAScript 6.
Деякі рядки, такі як смайли (😜), мають `.length` 2 (або навіть більше!), але повинні з'явитися в циклі `for-of` як одна одиниця.
Див. [цей допис в блозі Джонатана Нью](https://blog.jonnew.com/posts/poo-dot-length-equals-two) для більш детального пояснення.

Коли увімкнено прапор `downlevelIteration`, TypeScript буде використовувати допоміжну функцію, яка перевіряє наявність реалізації `Symbol.iterator` (нативну чи поліфіл).
Якщо ця реалізація відсутня, ви повернетесь до ітерації на основі індексу.

```ts twoslash
// @target: ES5
// @downlevelIteration
// @showEmit
const str = "Hello!";
for (const s of str) {
  console.log(s);
}
```

> > **Примітка:** увімкнення `downlevelIteration` не покращує відповідність спецификації, якщо у середовищі виконання відсутній `Symbol.iterator`.

#### Приклад: зміни у роботі оператора spread з масивами

Так працює оператор `spread` з масивами:

```js
// Make a new array who elements are 1 followed by the elements of arr2
const arr = [1, ...arr2];
```

Виходячи з опису, здається, що привести цей код до стандартів ES5 нескладно:

```js
// The same, right?
const arr = [1].concat(arr2);
```

Однак у деяких рідкісних випадках поведінка відрізняється.
Наприклад, якщо в масиві є "дірка", відсутній індекс створить _свою_ властивість при роботі оператора spread, але не буде цього роботи при створенні масиву з `concat`:

```js
// Make an array where the '1' element is missing
let missing = [0, , 1];
let spreaded = [...missing];
let concated = [].concat(missing);

// true
"1" in spreaded;
// false
"1" in concated;
```

Подібно до `for / of`, `downlevelIteration` використовуватиме `Symbol.iterator` (якщо він присутній) для більш точного імітування поведінки ES 6.
