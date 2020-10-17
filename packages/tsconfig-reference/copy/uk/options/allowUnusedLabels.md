---
display: "Дозволити невикористані ярлики"
oneline: "Випадкове створення ярлика приводить до помилки"
---

Значення false вимикає попередження про невикористані ярлики (labels).

Ярлики у JavaScript зустрічаються дуже рідко, найчастіше внаслідок невдалої спроби написати літерал об'єка:

```ts twoslash
// @errors: 7028
// @allowUnusedLabels: false
function verifyAge(age: number) {
  // Тут пропущено 'return'
  if (age > 18) {
    verified: true;
  }
}
```
