## Writing our library VII

- Login to Travis
- add `.travis.yml`

```yml
language: node_js
node_js: '6'
cache: yarn
notifications:
  email: false
# allow this once https://github.com/travis-ci/travis-ci/issues/6933 is fixed
# install:
#  - yarn
script:
  - npm run build
```


DONE!

