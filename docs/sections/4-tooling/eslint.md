# ESLint

[ESLint](https://eslint.org) is a tool for identifying and reporting on patterns found in ECMAScript/JavaScript code, with the goal of making code more consistent and avoiding bugs. This ensures all code confirms with the projects coding standards and it catches potential errors.

!> **IMPORTANT** If you are using [Vue CLI 3](https://cli.vuejs.org/) then you can skip this first part and go straight to [Lint before committing](#lint-before-committing).

## Setup

1. Lets install the `eslint` module and it's dependencies.

    **NOTE** When installing eslint globally it's dependencies must also be installed globally.
    
    ```bash
    $ npm install -g eslint eslint-config-standard eslint-plugin-import eslint-plugin-node eslint-plugin-promise eslint-plugin-standard
    ```
    
    Alternatively you can install locally, which makes sense if you want other developers to get up and running just using `npm install`.

    ```bash
    $ npm install --save-dev eslint eslint-config-standard eslint-plugin-import eslint-plugin-node eslint-plugin-promise eslint-plugin-standard
    ```

2. Setup a configuration file.

    ```bash
    $ eslint --init
    ```

    This will ask you a number of questions:
    
    ```
    ? How would you like to configure ESLint?
      Answer questions about your style
    ❯ Use a popular style guide
      Inspect your JavaScript file(s)
    
    ? Which style guide do you want to follow?
      Google
      Airbnb
    ❯ Standard
    
    ? What format do you want your config file to be in? (Use arrow keys)
    ❯ JavaScript
      YAML
      JSON
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
       "lint:error-only": "eslint -c .eslintrc.js --quiet --format codeframe bin src tests"
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

## Add babel-eslint

If you have setup Babel then you need to add the babel-eslint plugin for babel to play nice with ESLint.

ESLint's default parser and core rules only support the latest final ECMAScript standard and do not support experimental (such as new features) and non-standard (such as Flow or TypeScript types) syntax provided by Babel. babel-eslint is a parser that allows ESLint to run on source code that is transformed by Babel.

First install the `babel-eslint` plugin:

```bash
$ npm install --save-dev babel-eslint
```

Now add it to the `.bashrc.js` file:

```
module.exports = {
  parser: "babel-eslint"
};
```

**NOTE** The parser options described in the official documentation are for the default parser and are not necessarily supported by babel-eslint. Please see the section [Additional parser configuration](https://github.com/babel/babel-eslint#additional-parser-configuration) for the supported parserOptions.

## Lint before committing

Now lets make sure users cannot commit without there code being linted by ESLint and formatted by Prettier (see [next section](sections/4-tooling/prettier.md)). We always want this to run before code is committed to avoid committing files that contain errors or do not conform to our code formatting rules. We want to run this process with auto fix (`--fix`). A problem with running this on commit is that it will potentially change files that will not be part of the commit. To solve this we are going to add another cool tool [lint-staged](https://github.com/okonet/lint-staged). This tool will only run ESLint and Prettier on the staged files, which are the files we are committing. It will add any files that are changed during this process to the commit. Before it runs ESLint and Prettier it stashes any unstaged and untracked files and restores them once the process has completed. This way these files will not be processed. Pretty cool, right?

1. Install `lint-staged` and `husky`.

   ```bash
   $ npm install --save-dev lint-staged husky
   ```

2. Create the `.lintstagedrc.json` file in the project root and add the following entry to it, so that changes are linted before they are committed and any changes are added to the commit.

    ```json
    {
        "*.{js,vue}": ["npm run lint:fix --", "git add"]
    }
    ```

3. Create the `.huskyrc.json` file and add `lint-staged` to the git pre commit hook, so that staged files are linted before they are committed.

    ```json
    {
        "hooks": {
            "pre-commit": "lint-staged"
        }
    }
    ```

