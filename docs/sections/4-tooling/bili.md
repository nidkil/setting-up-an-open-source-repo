## Bili

[Bili](https://github.com/egoist/bili) is a zero-config library bundler that uses [Rollup](https://github.com/rollup/rollup) under the hood. A module bundler compiles small pieces of code into something larger and more complex, such as a library or application. It can generate different bundle formats (UMD, minified UMD, ES and CommonJS).

Setting up and configuration is ridiculously easy. The documentation can be found [here](https://bili.egoist.sh).

1. Install Bili.

    ```bash
    $ npm install --save-dev bili    
    ```

2. Create a `.bili.config.json` configuration file in the root directory of the project with the following contents.

    ```json
    {
      "input": "<main-entry-point>",
      "outDir": "./dist",
      "format": ["es", "umd"],
      "moduleName": "<name-of-your-module>",
      "filename": "<name-of-your-module>",
      "banner": true,
      "target": "<node|browser>"
    }
    ```

    This is an example `.bili.config.json` file.
    
    ```json
    {
      "input": "./src/use-pkg-version-cli.js",
      "outDir": "./dist",
      "format": ["es", "umd"],
      "moduleName": "use-pkg-version",
      "filename": "use-pkg-version",
      "banner": true,
      "target": "node"
    }
    ```

3. Add an entry to `scripts` in the `package.json` file.

   ```json
   {
     "scripts": {
       "build": "bili --config .bili.config.json"
     }
   }
   ```
