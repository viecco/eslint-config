# eslint-config-viecco
Shared ESLint configs for Node, Web, and universal Expo projects.

> This project is a wrap of [eslint-config-universal](https://github.com/expo/expo/tree/master/packages/eslint-config-universe), used by @viecco for internal projects.

## Installation

```sh
yarn add --dev eslint-config-viecco
```

You will also need to install `eslint`, `prettier`, `@typescript-eslint/eslint-plugin`, and `@typescript-eslint/parser`:

```sh
yarn add --dev eslint prettier @typescript-eslint/eslint-plugin @typescript-eslint/parser
```

## Usage

Import this config into your own ESLint configuration using the `extends` option. ESLint checks both package.json and .eslintrc.* files for its configuration:

### package.json
```js
{
  "eslintConfig": {
    // Choose from viecco/native, viecco/node, viecco/web
    "extends": "viecco"
  }
}
```

### .eslintrc.js
```js
module.exports = {
  extends: 'viecco',
};
```

## Customizing Prettier

If you would like to customize the Prettier settings, create a file named `.prettierrc.json` in your project directory. An example of Prettier configuration file:

```json
{
  "jsxBracketSameLine": false,
  "jsxSingleQuote": true,
  "printWidth": 80,
  "quoteProps": "as-needed",
  "semi": false,
  "singleQuote": true,
  "tabWidth": 2,
  "trailingComma": "all"
}
```

Read more about [configuring `prettier`](https://prettier.io/docs/en/configuration.html) and [all of the available options](https://prettier.io/docs/en/options.html).

## Support for Different Platforms

There are several configs for different platforms. They are:
* `viecco`: the basic config for JavaScript projects for which there isn't a more specific config
* `viecco/native`: the config for React Native projects, including Expo projects, with support for React and JSX
* `viecco/web`: the config for code that runs in web browsers, with support for React and JSX
* `viecco/node`: the config for code that runs in Node

For an Expo project, your configuration might look like this:

```js
"eslintConfig": {
  "extends": "viecco/native"
}
```

You also can extend multiple configs, which is useful for projects that span several platforms:

```js
"eslintConfig": {
  "extends": ["viecco/node", "viecco/web"]
}
```

## Optional Additional TypeScript Typed Linting

Universe also provides optional additional config for typescript-eslint rules that make use of the parsed type information. Note that this may increase the time it takes to run lint for large projects. More information can be found at https://github.com/typescript-eslint/typescript-eslint/blob/master/docs/getting-started/linting/TYPED_LINTING.md

To enable the additional config, the following changes to your config are required:

### .eslintrc.js

```diff
module.exports = {
  extends: [
    'viecco',
+   'viecco/shared/typescript-analysis',
  ],
+ overrides: [
+   {
+     files: [
+       '*.ts',
+       '*.tsx',
+       '*.d.ts'
+     ],
+     parserOptions: {
+       project: './tsconfig.json'
+     },
+   },
+ ],
};
```

More info on parserOptions.project can be found at https://github.com/typescript-eslint/typescript-eslint/tree/master/packages/parser#parseroptionsproject

## Philosophy

This config is designed to mark severe problems (ex: syntax errors) as errors and stylistic issues as warnings. This lets your team apply policies like, "make sure a commit has no errors but ignore warnings if the commit didn't introduce them."

It's also designed to be a more lenient config for teams who are stronger at decision-making and have a culture of osmotically learning coding guidelines and benefit more from flexibility than rigid rules.