## Writing our library IX

Now our lib is published to npm. Let's use it!


- Setup new project

`mdkir test-sw-names`

`cd test-sw-names`

`yarn add -D typescript`

`yarn tsc -- --init`

configure `tsconfig.json`

```json
{
    "compilerOptions": {
        "module": "commonjs",
        "target": "es5",
        "noImplicitAny": true,
        "noImplicitThis": true,
        "strictNullChecks": true,
        "sourceMap": true,
        "moduleResolution": "node"
    }
}
```

- in your terminal run `yarn tsc -- -w`

- create `index.ts` and use your library!

> src/index.ts

```ts
import {all,random} from 'starwars-ts-names'

setInterval(()=>{
  console.log(all());
},1000);

```

**TRY IT OUT**

`node src/index.js`


CONGRATULATIONS YOU ARE JEDI OSS KNIGHT NOW!


