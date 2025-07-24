# Шпаргалка: TypeScript + Node.js (CommonJS) + Nodemon

## 1. Встановлення залежностей

```bash
npm install --save-dev typescript ts-node nodemon @types/node
```

## 2. package.json

```json
{
  "name": "my-app",
  "version": "1.0.0",
  "main": "dist/app.js",
  "type": "commonjs", // ВАЖЛИВО: CommonJS для стабільності
  "scripts": {
    "dev": "ts-node src/app.ts",
    "watch": "nodemon --watch src --ext ts,js,json --exec \"ts-node src/app.ts\""
  },
  "devDependencies": {
    "typescript": "^5.0.0",
    "ts-node": "^10.0.0",
    "nodemon": "^3.0.0",
    "@types/node": "^20.0.0"
  }
}
```

## 3. tsconfig.json

```json
{
  "compilerOptions": {
    "target": "ES2020",
    "module": "commonjs",
    "lib": ["ES2020"],
    "outDir": "./dist",
    "rootDir": "./src",
    "strict": true,
    "esModuleInterop": true,
    "skipLibCheck": true,
    "forceConsistentCasingInFileNames": true,
    "resolveJsonModule": true,
    "declaration": true,
    "declarationMap": true,
    "sourceMap": true
  },
  "include": ["src/**/*"],
  "exclude": ["node_modules", "dist"]
}
```

## 4. Структура проекту

```
my-app/
  src/
    app.ts
  package.json
  tsconfig.json
```

## 5. Запуск

- **Розробка:**
  ```bash
  npm run dev
  ```
- **Автоматичний перезапуск при зміні файлів:**
  ```bash
  npm run watch
  ```

---

## Чому цей підхід класний?

- **Стабільність:** CommonJS — стандарт для Node.js, працює з усіма пакетами.
- **Простота:** Не потрібно додаткових флагів чи loader'ів, все працює "з коробки".
- **Швидкість:** Nodemon і ts-node швидко перезапускають додаток при зміні .ts файлів.
- **Відсутність попереджень:** Немає ExperimentalWarning, як у ESM.
- **Гнучкість:** Легко перейти на production-збірку через `tsc` (TypeScript Compiler).
- **Сумісність:** Працює з будь-якими npm-пакетами, тестовими фреймворками, дебагерами тощо.

---

## Якщо потрібен ESM (тільки якщо точно треба!)
- Замість `"type": "commonjs"` став `"type": "module"` у package.json
- В tsconfig.json: `"module": "ESNext"`
- Скрипти запуску складніші, потрібен loader: `NODE_OPTIONS="--loader ts-node/esm" node src/app.ts`
- Можливі попередження та проблеми з деякими пакетами

---

**Рекомендація:** Для більшості проектів — CommonJS + ts-node + nodemon = стабільна, зручна, швидка розробка на TypeScript у Node.js! 🚀 
