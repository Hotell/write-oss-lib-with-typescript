## Writing our library II

### Task runner

- npm
- yarn

We will use yarn!


```json
{
  "scripts": {
    "ts:style": "tsfmt --verify && tslint \"src/**/*.ts\"",
    "ts:style:fix": "npm run ts:format:fix && npm run ts:lint:fix"
  }
}
```

Now let's introduces some code that doesn't follows our rules.


let's fix them via our script

`yarn ts:style:fix`

DONE
