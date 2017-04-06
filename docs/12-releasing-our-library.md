## Writing our library VIII

`yarn add -D standard-version`

add npm scripts:

```json
{
  "scripts" {
    "prerelase": "npm run build",
    "release": "npm run release:local",
    "postrelease": "npm run release:github && npm run release:npm",
    "release:local": "standard-version",
    "release:github": "git push --no-verify --follow-tags origin master",
    "release:npm": "npm publish"
  }
}
```


- Push your changes!
- Login to Travis
- Add project to pipeline
- Add badges to your Readme.md

```md
Add badges
[![Build Status](https://travis-ci.org/Hotell/typescript-lib-starter.svg?branch=master)](https://travis-ci.org/Hotell/starwars-ts-names)

[![Standard Version](https://img.shields.io/badge/release-standard%20version-brightgreen.svg)](https://github.com/conventional-changelog/standard-version)
```

- commit your changes via `yarn commit` -> commitizen will show up


### Release !

**Initial release:**

`yarn release -- --first-release`

**Lets add some functionality**

`yarn commit`

`yarn release -- --first-release` bang!

now you should have version `1.1.0` of your library

GOOD JOB!



