## Typescript

So what is Typescript?

http://www.typescriptlang.org/play/

**config TS**

- tsconfig.json
- Weak mode / strong mode
- @types modules via npm


### Add Typescript

`yarn add -D typescript`

`yarn tsc -- --init`

```json
{
  "compilerOptions": {
    "module": "commonjs",
    "target": "es5",
    "noImplicitAny": false,
    "sourceMap": false
  }
}
```

We need to set following:
- strict mode
- declaration files generation
- output directory for compiled files
- include files
- exclude files

```json
{
  "compilerOptions": {
    "module": "commonjs",
    "target": "es5",

    "noUnusedLocals": true,
    "noImplicitAny": true,
    "strictNullChecks": true,
    "noImplicitThis": true,

    "sourceMap": true,

    "outDir": "lib",

    "declaration": true,
    "declarationDir": "typings",

    "pretty": true
  },
  "include": [
    "src"
  ],
  "exclude": [
    "node_modules"
  ]
}
```


### Add TSlint

`yarn add -D tslint@4.5.1 tslint-config-standard`

`yarn tslint -- --init`

```json
{
  "extends": "tslint:recommended"
}
```

It helps us fix errors ( some of them )

`yarn tslint -- --fix`

Now we wanna use standard rules with few custom ones

```json
{
  "extends": [
    "tslint-config-standard"
  ],
  "rules": {
    "import-spacing": true,
    "ordered-imports": [
      true
    ],
    "space-before-function-paren": [
      true,
      "never"
    ],
    "max-line-length": [
      true,
      120
    ]
  }
}
```


### Add Typescript-formatter

TSlint has not all capabilities in terms of formatting our souce code.

`yarn add -D typescript-formatter`
