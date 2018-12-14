# ESLint

[ESLint](https://eslint.org) is a tool for identifying and reporting on patterns found in ECMAScript/JavaScript code, with the goal of making code more consistent and avoiding bugs. This ensures all code confirms with the projects coding standards and it catches potential errors.

!> **IMPORTANT** If you are using [Vue CLI 3](https://cli.vuejs.org/) then you can skip this first part and go straight to [Lint before committing](#lint-before-committing).

## Setup

1. Lets install the `eslint` module.

   ```bash
   $ npm install -g eslint
   ```

2. Setup a configuration file.

   ```bash
   $ eslint --init
   ```

   After that, you can run ESLint on any file.

   ```bash
   $ eslint file1.js file2.js
   ```

   Or directory like this. The quotes and `**` indicate that glob must be used, in other words it will recursively iterate all directories and lint all files.

   ```bash
   $ eslint "src/**"
   ```

3. Add the following entry to `scripts` in the `package.json` file.

   ```json
   {
     "scripts": {
       "lint": "eslint -c .eslintrc.js --format codeframe bin src tests",
       "lint:fix": "eslint --fix -c .eslintrc.js --format codeframe bin src tests",
       "lint:error-only": "eslint -c .eslintrc.js --quiet --format codeframe src tests bin",
     }
   }
   ```

    A great feature of ESLint is its auto-fixing capability. With the `–fix` option on the command line, ESLint makes changes to the linted source code for fixable errors.

    The `--format codeframe` option specifies how ESLint will format messages. ESLint comes with [several built-in formatters](https://eslint.org/docs/user-guide/formatters/) to control the appearance of the linting results, and supports third-party formatters as well. The `codeframe` style displays the code and indicates exactly which part of the code the error or warning is referencing. Makes it a lot more understandable than the default `compact` formatter that is used.

   Now all you have to do is run `npm run lint` or `yarn lint` to check your project files.

   The `eslint:fix` command will try and automatically fix as many issues as possible. The fixes are made to the actual files themselves and only the remaining unfixed issues are output.

   You can find more information about the commandline interface of ESLint [here](https://eslint.org/docs/user-guide/command-line-interface).

4. Create `.eslintignore` file with the following contents.

   ```
   dist
   node_modules
   ```

5. Add the following to the `.eslintrc.js` file.

   ```js
   module.exports = {
     root: true,
     extends: ['standard'],
     parserOptions: {
       ecmaVersion: 2017
     },
     env: {
       es6: true
     },
     overrides: [
       {
         files: ['bin/*.js', 'src/*.js', 'test/*.js'],
         excludedFiles: 'dist/*.js',
         rules: {
           quotes: [2, 'single'],
           'no-console': process.env.NODE_ENV === 'production' ? 'warn' : 'off',
           'no-debugger': process.env.NODE_ENV === 'production' ? 'error' : 'off'
         }
       }
     ]
   }
   ```

   ESLint defaults to ES5 syntax checking. Using the `emacVersion` option in the `parseOptions` section and `es6` option in the `env` section you can override this and use the latest well supported version of JavaScript.

   The `overrides` section allows you to apply configuration to specifc file types. Here we are defining overrides for the file types specified in the `files` option, It specifies which folders and file types to include and with the `excludedFiles` option which directories and files to excluded. The `rules` section of `overrides` specifies which rules to overrule.

   You can find more information about configuring ESLint [here](https://eslint.org/docs/user-guide/configuring).

   You can find more information about ESLint rules [here](https://eslint.org/docs/rules/).

## Lint before committing

Now lets make sure users cannot commit without there code being linted by ESLint.

1. In the project root directory install `husky`.

   ```bash
   $ npm install --save-dev husky
   ```

2. Add ESLint to the git pre commit hook in `.huskyrc.json`, so that changes are linted before they are committed.

   ```json
   {
     "husky": {
       "hooks": {
         "pre-commit": "npm run lint:fix"
       }
     }
   }
   ```
