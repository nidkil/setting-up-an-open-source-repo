# Prettier

[Prettier](https://prettier.io/) is a zero-configuration code formatting utility by design. Its only purpose is to reformat source code; it does this job well. The main goal of Prettier is to remove all the distractions of writing code by allowing the developer writing code as he likes. Prettier instantly formats the code correctly on save. This means all code uses the same coding style, which makes the code much easier to read and understand.

ESLint also features code formatting capabilities. However, in corporation with Prettier this can lead to problems due to contrary formatting configurations. It is possible to disable all ESLint rules related to code formatting and use Prettier only for beautifying your code.

Prettier is built for integration with ESLint, so they play well together . We want ESLint to (if possible) auto-fix detected programming errors and derivations from coding conventions and Prettier to auto-fix violations of code formatting conventions. This is can be achieved manually by running npm scripts and automatically by using git commit hooks. We will setup both.

An additional requirement is that we want everything to work for [Vue single file components](https://vuejs.org/v2/guide/single-file-components.html) too. 

1. Lets install the `prettier` module.

   ```bash
   $ npm install --save-dev prettier
   ```

2. Install plugins so that we can use `prettier` with `eslint`.

   ```bash
   $ npm install --save-dev eslint-plugin-prettier eslint-config-prettier
   ```
   
   With `eslint-config-prettier` we turn off all ESLint code formatting rules that are unnecessary or might conflict with Prettier.
   
   With `eslint-plugin-prettier` we add Prettier as an ESLint rule.

3. Add `prettier` to `.eslintrc.json` file.

   ```json
    {
      "extends": ["prettier", "prettier/standard"],
      "plugins": ["prettier"],
      "rules": {
        "prettier/prettier": "error"
      }
    }
   ```

    Or in a more concise way.
    
   ```json
    {
      "extends": ["plugin:prettier/recommended"]
    }
   ```

4. Lets overrule some Prettier rules by adding a `.prettierrc` configuration file to the root directory of our project. Add the following content.

    ```json
    {
      "trailingComma": "none",
      "tabWidth": 2,
      "semi": false,
      "singleQuote": true,
      "endOfLine": "lf"
    }
    ```
 
    These changes will make Prettier behave like the standard settings of Vue (no trailing comma's, tabs replaced by two spaces, no trailing semicolons and single quotes for strings). The last setting changes end of line characters to `\n`, which is common on Linux and macOS. Otherwise Prettier opts for `auto`, which means preserving the line endings used or if mixed it will convert line endings to the first line ending type it finds per file.
    
    You can find more information about the available options [here](https://prettier.io/docs/en/options.html).
 
5. Check for `eslint` configuration conflicts with `prettier`. The `eslint-config-prettier` plugin is shipped with a CLI helper tool that checks for configuration conflicts. Add a script to the `package.json` file.

   ```json
   {
     "scripts": {
       "lint:check": "eslint --print-config .eslintrc.json | eslint-config-prettier-check"
     }
   }
   ```

6. Adding a pre commit hook to git that runs `eslint` and `prettier`. Add the following entry to the sripts in `package.json`.

   ```json
   {
     "scripts": {
       "pre-commit": "npm run lint-check && npm run lint"
     }
   }
   ```
   
   The pre commit hook prevents committing if the lint check or linting are not successful. This is a great option to improve development productivity and code quality.

### ESLint and Prettier with Vue.js

If you are using Vue CLI 3 then you are lucky, because it can generate a project with ESLint setup. Just select the option when creating the project. These instructions are for this situation. The generated `.eslintrc.js`  file looks like this.

```js
module.exports = {
  root: true,
  env: {
    node: true
  },
  'extends': [
    'plugin:vue/essential',
    '@vue/standard'
  ],
  rules: {
    'no-console': process.env.NODE_ENV === 'production' ? 'error' : 'off',
    'no-debugger': process.env.NODE_ENV === 'production' ? 'error' : 'off'
  },
  parserOptions: {
    parser: 'babel-eslint'
  }
}
```

Lets add `prettier` to the mix.

```js
module.exports = {
  root: true,
  env: {
    node: true
  },
  'extends': [
    `prettier`,
    `prettier/standard`,
    'plugin:vue/essential',
    '@vue/standard'
  ],
  plugins: ['vue', 'prettier'],
  rules: {
    'prettier/prettier': 'error',
    'no-console': process.env.NODE_ENV === 'production' ? 'error' : 'off',
    'no-debugger': process.env.NODE_ENV === 'production' ? 'error' : 'off'
  },
  parserOptions: {
    parser: 'babel-eslint'
  }
}
```

Finally we need to change setup the `scripts` in `package.json`.

```json
{
  "scripts": {
    "lint": "vue-cli-service lint -c .eslintrc.js --format codeframe plugin src tests",
    "lint:fix": "vue-cli-service lint -c .eslintrc.js --format codeframe --fix plugin src tests",
    "lint:error-only": "vue-cli-service lint -c .eslintrc.js --format codeframe --quiet plugin src tests",
    "REMARK#1": "Following command isn't working",
    "lint:check": "vue-cli-service lint --print-config .eslintrc.js | eslint-config-prettier-check",
    "pre-commit": "npm run lint-check && npm run lint"
  }
}
```

Note that we are not calling `eslint` directly, but calling it through Vue CLI 3 using `vue-cli-service lint`.
