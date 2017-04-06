## Writing our library VI

### Conventional changelog

**Message format**:

```
<type>(<scope>): <subject>
<BLANK LINE>
<body>
<BLANK LINE>
<footer>
```


**Type**

```
feat: A new feature
fix: A bug fix
docs: Documentation only changes
style: Changes that do not affect the meaning of the code (white-space, formatting, missing semi-colons, etc)
refactor: A code change that neither fixes a bug nor adds a feature
perf: A code change that improves performance
test: Adding missing or correcting existing tests
chore: Changes to the build process or auxiliary tools and libraries such as documentation generation
```

we need to install [commitizen](https://github.com/commitizen/cz-cli)

`yarn add -D commitizen cz-conventional-changelog validate-commit-msg`

Configure commitizen in package.json:

```json
{
  "scripts":{
    "commit": "git-cz"
  },
  "config": {
    "commitizen": {
      "path": "./node_modules/cz-conventional-changelog"
    },
    "validate-commit-msg": {
      "types": "conventional-commit-types",
      "maxSubjectLength": 120
    }
  }
}
```

### Git Hooks

`yarn add -D husky`

add scripts:

```json
{
  "scripts":{
    "commitmsg": "validate-commit-msg",
    "prepush": "npm run verify"
  }
}
```
