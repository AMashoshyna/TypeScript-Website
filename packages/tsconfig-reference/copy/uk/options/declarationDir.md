---
display: "Директорія декларацій"
oneline: "Визначає кореневу видректорію для файлів d.ts"
---

Пропонує можливість вибору кореневої директорії, куди буде збережено деклараційні файли.

```
example
├── index.ts
├── package.json
└── tsconfig.json
```

з таким `tsconfig.json`:

```json tsconfig
{
  "compilerOptions": {
    "declaration": true,
    "declarationDir": "./types"
  }
}
```

розмістить файли d.ts для `index.ts` у директорії `types`:

```
example
├── index.js
├── index.ts
├── package.json
├── tsconfig.json
└── types
    └── index.d.ts
```
