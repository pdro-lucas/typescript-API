# Configurando um projeto com typescript

Para começar a utilizar o TypeScript no seu projeto, primeire instale-o com o comando abaixo:

```sh
$ pnpm add typescript @types/node -D
```

Crie um arquivo `tsconfig.json` e adicione a seguinte configuração:

```json
{
  "compilerOptions": {
    "target": "es2019",
    "moduleResolution": "node",
    "module": "commonjs",
    "lib": ["es2019"],
    "sourceMap": true,
    "outDir": "dist",
    "strict": true,
    "noImplicitAny": true,
    "strictNullChecks": true,
    "strictFunctionTypes": true,
    "noImplicitThis": true,

    "resolveJsonModule": true,
    "alwaysStrict": true,
    "removeComments": true,
    "noImplicitReturns": true,
    "esModuleInterop": true,
    "allowSyntheticDefaultImports": true,
    "baseUrl": ".",
    "paths": {
      "@src/*": ["./src/*"],
      "@test/*": ["./test/*"]
    },
    "rootDirs": ["./src", "./test"],
    "experimentalDecorators": true,
    "emitDecoratorMetadata": true
  },
  "include": ["./src/**/*.ts", "./test/**/*.ts"],
  "exclude": ["./node_modules", "dist"]
}
```

Para que os alias funcione, instale a seguinte biblioteca:

```sh
$ pnpm add module-alias
$ pnpm add @types/module-alias -D
```

Agora crie uma configuração para os alias:

```ts
// src/util/module-alias
import moduleAlias from "module-alias";
import * as path from "path";

const files = path.resolve(__dirname, "../..");

moduleAlias.addAliases({
  "@src": path.join(files, "src"),
  "@test": path.join(files, "test"),
});
```

## Configurando o eslint

Instale as dependencias:

```sh
$ pnpm add -D @typescript-eslint/eslint-plugin eslint @typescript-eslint/parser
```

Crie um arquivo `.eslintrc` e adicone o seguinte:

```json
{
  "root": true,
  "parser": "@typescript-eslint/parser",
  "plugins": ["@typescript-eslint"],
  "extends": [
    "eslint:recommended",
    "plugin:@typescript-eslint/eslint-recommended",
    "plugin:@typescript-eslint/recommended"
  ]
}
```

Adicione os seguinte scripts ao seu `package.json`:

```json
...
"scripts": {
  "lint": "eslint ./src ./test --ext .ts",
  "lint:fix": "eslint ./src ./test --ext .ts --fix",
}
...
```

## Adicionando o ts-node

Instale com o comando abaixo:

```sh
$ pnpm add -D ts-node-dev
```

Agora adicione o seguinte no seu `package.json`

```json
"scripts": {
  "start:dev": "ts-node-dev 'src/index.ts'",
}
```
