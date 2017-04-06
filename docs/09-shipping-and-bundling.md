## Writing our library V


We need various formats to support every environment

- ES5
  - AMD
  - CommonJS
  - UMD
- ES2015

### UMD + ES5

We need module bundler --> WEBPACK

`yarn add -D webpack awesome-typescript-loader`

> webpack.config.js

```js
const { resolve } = require('path');
const webpack = require('webpack');

const packageJSON = require('./package.json');
const packageName = packageJSON.name;

const PATHS = {
  entryPoint: resolve(__dirname, 'src/index.ts'),
  bundles: resolve(__dirname, 'umd'),
}

const UMD = {
  libName: pascalCase(packageName),
}

const config = (env) => {

  return {
    // These are the entry point of our library. We tell webpack to use
    // the name we assign later, when creating the bundle. We also use
    // the name to filter the second entry point for applying code
    // minification via UglifyJS
    entry: {
      [packageName]: [PATHS.entryPoint],
      [`${packageName}.min`]: [PATHS.entryPoint]
    },
    // The output defines how and where we want the bundles. The special
    // value `[name]` in `filename` tell Webpack to use the name we defined above.
    // We target a UMD and name it MyLib. When including the bundle in the browser
    // it will be accessible at `window.MyLib`
    output: {
      path: PATHS.bundles,
      filename: '[name].js',
      libraryTarget: 'umd',
      library: UMD.libName,
      umdNamedDefine: true
    },
    // Add resolve for `tsx` and `ts` files, otherwise Webpack would
    // only look for common JavaScript file extension (.js)
    resolve: {
      extensions: ['.ts', '.tsx', '.js']
    },
    // Activate source maps for the bundles in order to preserve the original
    // source when the user debugs the application
    devtool: 'source-map',
    plugins: [
      // Apply minification only on the second bundle by
      // using a RegEx on the name, which must end with `.min.js`
      // NB: Remember to activate sourceMaps in UglifyJsPlugin
      // since they are disabled by default!
      new webpack.optimize.UglifyJsPlugin({
        sourceMap: true,
        include: /\.min\.js$/,
      }),

      new webpack.LoaderOptionsPlugin({
        minimize: true
      }),
    ],
    module: {
      // Webpack doesn't understand TypeScript files and a loader is needed.
      // `node_modules` folder is excluded in order to prevent problems with
      // the library dependencies, as well as `__tests__` folders that
      // contain the tests for the library
      rules: [{
        test: /\.tsx?$/,
        exclude: /node_modules/,
        use: [{
          loader: 'awesome-typescript-loader',
          options: {
            // we don't want any declaration file in the bundles
            // folder since it wouldn't be of any use ans the source
            // map already include everything for debugging

            // This cannot be set because -> Option 'declarationDir' cannot be specified without specifying option 'declaration'.
            // declaration: false,
          }
        }],
      }]
    }
  }
}

module.exports = config;


// helpers

function camelCaseToDash(myStr) {
  return myStr.replace(/([a-z])([A-Z])/g, '$1-$2').toLowerCase();
}

function dashToCamelCase(myStr) {
  return myStr.replace(/-([a-z])/g, (g) => g[1].toUpperCase());
}

function toUpperCase(myStr) {
  return `${myStr.charAt(0).toUpperCase()}${myStr.substr(1)}`;
}

function pascalCase(myStr) {
  return toUpperCase(dashToCamelCase(myStr));
}
```


### CommonJS + ES2015

We can use TYPESCRIPT

```yarn tsc``` --> commonJS + Es5
```yarn tsc  --module es2015 --target es2015 --outDir lib-esm` ---> pure es2015

---

### Adding new tasks

- build all formats with one task
- cleanup `yarn add -D shx`
- verify if tests and styles are ok
- make it run before build

```json
{
  "scripts" : {
    "build": "tsc && tsc --module es2015 --target es2015 --outDir lib-esm && webpack",

    "cleanup": "shx rm -rf umd lib lib-esm typings coverage docs",
    "verify": "npm run ts:style && npm t",

    "prebuild": "npm run cleanup && npm run verify"
  }
}
```


### Telling the package what type to consume


We need to confi our `package.json`

- add `typings`
- add `main` et all

```json
{
  "main": "lib/index.js",
  "module": "lib-esm/index.js",
  "umd": "umd/typescript-lib-starter.min.js",
  "typings": "typings/index.d.ts",
}
```

