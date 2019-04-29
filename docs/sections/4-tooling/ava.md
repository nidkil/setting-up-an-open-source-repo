# AVA

Testing can be a drag. [AVA](https://github.com/avajs/ava) helps you get it done. AVA is a test runner for Node.js with a concise API, detailed error output, embrace of new language features and process isolation that let you write tests more effectively. So you can ship more awesome code. 🚀


## Install

```bash
$ npm install --save-dev ava
```

## Configure

1. Add AVA to the `scripts` in the `package.json` file.

    **NOTE** AVA can only be run using the AVA cli. 
    
    ```json
    {
      "scripts": {
        "test": "ava"
      }
    }
    ``` 

2. Make AVA play nicely with our Babel setup 

    AVA uses [Babel 7](https://babeljs.io/) out of the box, so you can use the latest JavaScript syntax in your tests. By default the AVA Babel pipeline is applied to test and helper files ending in `.js`. If the project uses Babel then it will automatically compile these files using the project's Babel configuration.

    If you are using Babel for your source files then you must also configure [source compilation](https://github.com/avajs/ava/blob/master/docs/recipes/babel.md#compile-sources). AVA does not compile source files. The [Babel register module](https://babeljs.io/docs/en/babel-register) is needed for this, which compiles source files on the fly.
    
    Install the `@babel/register` module:
    
    ```bash
    $ npm install --save-dev @babel/register
    ```
    
    Create the file `test/_register.js` and add the following:
    
    ```js
    require('@babel/register')({
      // These patterns are relative to the project directory (where the `package.json` file lives):
      ignore: ['node_modules/*', 'test/*']
    });

    ```

    Add the following to the `package.json` file:
    
    ``` json
    {
        "ava": {
            "require": [
                "./test/_register.js"
            ]
        }
    }
    ```

## Running tests

As mentioned previously AVA can only be run using the AVA cli.

```bash
$ npm test
```

## Webstorm

https://github.com/avajs/ava/blob/master/docs/recipes/debugging-with-webstorm.md

## References

- [Assertions](https://github.com/avajs/ava/blob/master/docs/03-assertions.md)
- [Configuring Babel](https://github.com/avajs/ava/blob/master/docs/recipes/babel.md)
- [Compile sources](https://github.com/avajs/ava/blob/master/docs/recipes/babel.md#compile-sources)
- [Webstorm](https://github.com/avajs/ava/blob/master/docs/recipes/debugging-with-webstorm.md)
