# Шпаргалка: TypeScript + Node.js + Path Aliases (@/)

## 1. Встановлення залежностей

```bash
npm install --save-dev typescript ts-node nodemon tsconfig-paths @types/node
```

## 2. tsconfig.json

```json
{
  "compilerOptions": {
    "target": "ES2020",
    "module": "commonjs",
    "lib": ["ES2020"],
    "outDir": "./dist",
    "rootDir": "./src",
    "baseUrl": "src",
    "paths": {
      "@/*": ["*"]
    },
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

## 3. package.json (scripts)

```json
{
  "scripts": {
    "dev": "ts-node -r tsconfig-paths/register src/app.ts",
    "watch": "nodemon --watch src --ext ts,js,json --exec \"ts-node -r tsconfig-paths/register src/app.ts\""
  }
}
```

## 4. Як імпортувати

```ts
import { LLM } from "@/core/llm";
import { MongoReasoningAgent } from "@/reasoning/agents/mongo-reasoning-agent";
```

## 5. Офіційна документація
- [TypeScript Handbook: Module Resolution](https://www.typescriptlang.org/tsconfig#paths)
- [tsconfig-paths (npm)](https://www.npmjs.com/package/tsconfig-paths)

---

**Тепер ти можеш писати короткі імпорти з будь-якої точки проекту!** 
