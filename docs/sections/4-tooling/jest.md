# Jest

!> **IMPORTANT** If you are using [Vue CLI 3](https://cli.vuejs.org/) select the option `Unit Testing` and choose `Jest` as testing solution. You can skip the first steps and go straight to [step 6](#step-6).

Unit testing is an important aspect of software quality control. There is a lot that can be said about it and how to do it. I will limit myself to the highlights:

- Unit tests find problems early in the development cycle
- An automated unit test suite watches over your code in two dimensions: time[1] and space[2]
- Developers will be less afraid to change existing code
- The development process becomes more flexible
- Improves your project’s truck factor
- Reduces the need for manual testing
- Software development will become more predictable and repeatable

[1] It watches over your code in the time dimension because once you’ve written a unit test, it guarantees that the code you wrote works now and in the future.
[2] It watches over your code in space dimension because unit tests written for other features guarantee that your new code did not break them; likewise it guarantees that code written for other features does not adversely affect the code you wrote for this feature.

There are many test frameworks out there, I personally prefer [Jest](https://jestjs.io/) as it is an all in one solution.

## Setup

1. Lets install the `jest` module.

   ```bash
   $ npm install --save-dev jest
   ```

2. Add a basic `jest.config.js` configuration file.

   ```bash
   $ jest --init
   ```

   You will be asked a number of questions. Most of them speak for them self. One that can save you a lot of initialization time is the type of test environment `node` or `jsdom`. If you are developing a library that does not require a browser functionality choose `node`.
   
   Example:
   
   ```
   √ Would you like to use Jest when running "test" script in "package.json"? ... yes
   √ Choose the test environment that will be used for testing » node
   √ Do you want Jest to add coverage reports? ... yes
   √ Automatically clear mock calls and instances between every test? ... no   
   ```

3. If you did not select the option to run Jest from the `scripts` section of the `package.json` file during initialization, then add the following.

   ```json
   {
     "scripts": {
       "test": "jest"
     }
   }
   ```

   Now all you have to do is run `npm test` or `yarn test` to check your project files.

4. Add an alias for the `src` directory by adding the following to the `jest.config.js` file.

   ```js
   module.exports = {
     moduleNameMapper: {
       "@/(.*)$": "<rootDir>/src/$1"
     }
   }
   ```

5. Configure Babel to use Jest

   To use Jest with Babel install the required dependencies:

   ```bash
   $ npm install --save-dev babel-jest
   ```
   
   By default Jest looks for spec files (`*.spec.js`) in all directories of a project except for `node_modules`. This means that it will pickup tests in the `dist` directory. To disable this add the following to the `jest.config.json` file:
   
   ```js
   testPathIgnorePatterns: [
     "\\\\node_modules\\\\",
     "\\\\dist\\\\"
   ],
   ```
   
   Add the following the the `package.json` file if you are developing for Node:
   
   ```json
   {
     "jest": {
       "transform": {
         "^.+\\.jsx?$": "babel-jest"
       }
     }
   }
   ```
   
   Configure Babel to target the current Node version by adding the following to the `babel.config.js` file:
    
   ```js
   module.exports = {
     "presets": [
       [
         "@babel/preset-env", {
           "targets": {
             "node": "current"
           }
         }
       ]
     ]
   };
   ```
    
6. Configure eslint to work with Jest.

   Install the eslint Jest plugin.

   ```bash
   $ npm install -save-dev eslint-plugin-jest
   ```

   Create a `test` directory in the main project directory.

   ```bash
   mkdir test
   ```

   In the `test` directory create a `.eslintrc.js` file specifically for the tests and add the following contents.

   ```js
   module.exports = {
     extends: ['plugin:jest/recommended'],
     plugins: ['jest'],
     overrides: [
       {
         files: ['test/*.js'],
         rules: {
           'jest/no-disabled-tests': 'warn',
           'jest/no-focused-tests': 'error',
           'jest/no-identical-title': 'error',
           'jest/prefer-to-have-length': 'warn',
           'jest/valid-expect': 'error'
         }
       }
     ]
   }
   ```

   This makes use of eslint's cascading configuration. The configuration cascade works by using the closest .eslintrc file to the file being linted as the highest priority, then any configuration files in the parent directory, and so on.

7. <a name="step-6">Update pre commit hooks in `.huskyrc.json`, so that test are also run before committing.</a>

   ```json
   {
     "husky": {
       "hooks": {
         "pre-commit": "npm test && npm run lint:check && npm run lint:fix"
       }
     }
   }
   ```

## Jest with Vue CLI 3

1. Update the following entries in the `scripts` section of the `package.json` file.

   ```json
   {
     "scripts": {
       "serve": "vue-cli-service serve --open",
       "test:unit": "vue-cli-service test:unit",
       "coverage": "vue-cli-service test:unit --coverage"
     }
   }
   ```

## Webstorm

### Getting Webstorm to recognize aliases

Webstorm will not understand aliases setup in Jest by default. The trick to help Webstorm understand them, is to define a webpack configuration file (`webpack.config.js`) that has the same aliases.

```js
module.exports = {
 resolve: {
   alias: {
     '@': require('path').resolve(__dirname, 'src')
   }
 }
}
```

And voila like magic Webstorm now understands the aliases and you can navigate them with Ctrl+B and code completion works. O yeah!

### Getting rid of 'Unresolved function or method expect()'

Webstorm will display a warning for Jest functions and methods. To get ride of these warnings you have to add the Jest Typescript definition to Webstorm.

- File > Settings (Ctrl+Alt+S) > Languages & Frameworks > Javascript > Libraries
- Click the 'Download...'
- Type 'Jest'
- Select and click 'Download & Install'

Now Webstorm will recognize Jest functions and methods.
