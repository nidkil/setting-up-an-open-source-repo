# Babel

[Babel](https://babeljs.io/) is a toolchain that is mainly used to convert ECMAScript 2015+ code into a backwards compatible version of JavaScript in current and older browsers or environments.

This is a test project to investigate how to setup Babel. It also includes instructions for Webstorm.

## Project structure

```
babel-test
|-- dist
|-- node_modules
|-- src
|   |--index.js
|   |--test.js
|-- .babelrc
|-- package.json
```

## Install

While you can install Babel CLI globally on your machine, it's much better to install it locally project by project. There are two primary reasons for this.

- Different projects on the same machine can depend on different versions of Babel allowing you to update one at a time.
- It means you do not have an implicit dependency on the environment you are working in. Making your project far more portable and easier to setup.

Install the following packages to get Babel to work with Node.
 
```bash
$ npm install --save-dev @babel/core @babel/cli @babel/node @babel/preset-env @babel/register @babel/polyfill
```

For easy development we will also add the [nodemon](https://github.com/remy/nodemon) package, which simplifies development by reloading node automatically when a source file changes.

```bash
$ npm install --save-dev nodemon
```

## Create .babelrc file

Create a .babelrc config in the project root and enable some plugins. To start, you can use the env preset, which enables transforms for ES2015+:  In order to enable the preset you have to add it to the `.babelrc` file, like this:

```json
{
  "presets": ["@babel/preset-env"]
}
```

See [here](https://babeljs.io/docs/en/configuration) for more information on it. And [here](https://gist.github.com/nodkz/41e189ff22325a27fe6a5ca81df2cb91) for a good and extensive example of a Babel configuration file. 

## Add script to package.json file

Add some scripts to the package.json to run and build the project with Babel.

```json
"scripts": {
    "clean": "rm -rf dist",
    "build": "npm run clean && babel src --out-dir dist --source-maps",
    "serve:dev": "nodemon --exec babel-node src/index",
    "serve:prd": "node dist/index"
}
```

From the command line you can build the project with:

```bash
$ npm run build
```

And run it in development mode with:

```bash
$ npm run serve:dev
```

## Add aliases

A cool feature in Webpack is adding aliases, which simplifies the require/import paths in projects. For example, instead of using complex relative paths like `../../../../utils/my-utils`, you can write `@/utils/my-utils`. It allows you to work faster as you don't have to calculate how many directory levels you have to navigate to access a file. The Babel `babel-plugin-module-resolver` plugin provides the same functionality.

Install the plugin:

```bash
$ npm install --save-dev babel-plugin-module-resolver
```

Add the plugin to the `babelrc.js` file:

```json
{
  "plugins": [
    ["module-resolver", {
      "root": ["./src"],
      "alias": {
        "@": ".",
        "libs": "./libs"
      }
    }]
  ]
}
```

Now you can simplify your imports with the aliases:

```
import myLib1 from '@/libs/my-lib'
import myLib2 from 'libs/my-lib'
```

## Webstorm

Okay lets get Webstorm working with Babel, so that we can debug our source code.

### Enable EMCAScript 6

Make sure ECMAScript 6 is set as the JavaScript version in WebStorm’s Preferences

```
File > Settings... (Ctrl+Alt+S) > Languages and Frameworks > JavaScript
```

Make sure the `JavaScript Language Version` is set to `ECMAScript 6`.

### Add the Babel file watcher

File watcher is a WebStorm built-in tool that allows you to automatically run commandline tools on file changes. For Babel Webstorm has pre-configured File watchers.

Go to the file watcher settings:

```
File > Settings... (Ctrl+Alt+S) > Tools > File watchers
```

Click the `+` button and select Babel from the list.
 
In the File watcher configuration dialog check if the path to Babel is correct: it should be located in the project node_modules folder, e.g. node_modules/.bin/babel.

All other Watcher settings are predefined and should be ready to go. With this default setup, compiled files will be located in the dist folder.

### Debugging

#### Using @babel/register

When you’re developing a Node.js application in ES6, one of the ways to run and test it is using `@babel/register`.

- In your Node.js run/debug configuration add `-r @babel/register` in the Node parameters field. Don’t forget to specify the path to the JavaScript file you’d like to run.
- Save configuration and hit run or debug.

#### Using @babel/node

Alternatively you can use @babel/node. To use it, you need to install it and setup a script in the `package.json` file. See the section `Add script to package.json file`.

### Getting Webstorm to recognize aliases
    
If you setup aliases using the Babel plugin `babel-plugin-module-resolver` Webstorm will not understand them by default. The trick to help Webstorm understand them is to define a webpack configuration file (`webpack.config.js`) that defines the same aliases.
    
```js
module.exports = {
 resolve: {
   alias: {
     '@': require('path').resolve(__dirname, 'src')
   }
 }
}
```
    
And voila like magic Webstorm now understands the aliases and you can navigate them with Ctrl+B.

## Troubleshooting

- [TypeError: <classname> is not a constructor](https://stackoverflow.com/a/40295288/862907)

## References

- [Good and extensive example of a Babel configuration file](https://gist.github.com/nodkz/41e189ff22325a27fe6a5ca81df2cb91)
- [Babel presets](https://codingcompiler.com/babel-presets/)
- [babel-preset-env: a preset that configures Babel for you](http://2ality.com/2017/02/babel-preset-env.html)
