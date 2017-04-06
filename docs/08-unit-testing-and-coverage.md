## Writing our library IV

We will use [Jest](https://facebook.github.io/jest/) for everything related to test et all.

### Install

`yarn add -D jest @types/jest`

`yarn add -D ts-jest`

### Configure JEST

> package.json

```json
{
  "jest": {
    "globals": {
      "__TS_CONFIG__": {
        "module": "commonjs"
      }
    },
    "roots": [
      "<rootDir>/src"
    ],
    "transform": {
      ".(ts|tsx)": "<rootDir>/node_modules/ts-jest/preprocessor.js"
    },
    "testRegex": "(/__tests__/.*|\\.(test|spec))\\.(ts|tsx|js)$",
    "moduleFileExtensions": [
      "ts",
      "tsx",
      "js"
    ],
    "modulePathIgnorePatterns": [
      "/^((?!src).)/"
    ],
    "testResultsProcessor": "<rootDir>/node_modules/ts-jest/coverageprocessor.js",
    "coveragePathIgnorePatterns": [
      "<rootDir>/node_modules/",
      "<rootDir>/lib/",
      "<rootDir>/lib-esm/",
      "<rootDir>/umd/",
      "<rootDir>/src/.*(/__tests__/.*|\\.(test|spec))\\.(ts|tsx|js)$"
    ],
    "coverageThreshold": {
      "global": {
        "branches": 80,
        "functions": 80,
        "lines": 80,
        "statements": 85
      }
    }
  }
}
```


### Update our Scripts

```json
{
  "scripts": {
    "test": "jest",
    "test:watch": "npm t -- --watch",
    "test:coverage": "npm t -- --coverage"
  }
}
```

run test: `yarn test`

Whops no tests!


### Writting tests

- create test folder within src and name it `__tests__`
- create file within our tests `index.spec.ts`


#### Practice time!

- Write unit tests for `all` and `random`
- make sure you've got 100% coverage


**Hints:**

Use `yarn test:watch` during writting your tests
Use `yarn test:coverage` for checking how is your coverage doing ;)






**Here is how it should look like**

```ts
import * as starWars from '../index'

describe('starwars-names', () => {
  describe('all', () => {
    it('should be an array of strings', () => {
      const expected = true
      const actual = isArrayOfStrings(starWars.all())
      expect(actual).toBe(expected)

      function isArrayOfStrings(array: string[]) {
        return array.every((item) => typeof item === 'string')
      }
    })

    it('should contain `Luke Skywalker`', () => {
      const actual = starWars.all()
      const expected = 'Luke Skywalker'
      expect(actual).toContain(expected)
    })
  })

  describe('random', () => {
    it('should return a random item from the starWars.all', () => {
      const randomItem = starWars.random()
      expect(starWars.all()).toContain(randomItem)
    })

    it('should return an array of random items if passed a number', () => {
      const randomItems = starWars.random(3)
      expect(randomItems).toHaveLength(3)

      if (Array.isArray(randomItems)) {

        randomItems.forEach(function(item) {
          expect(starWars.all()).toContain(item)
        })

      }

    })
  })
})
```



