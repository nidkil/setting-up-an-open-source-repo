## Bili

[Bili](https://github.com/egoist/bili) is a zero-config library bundler that uses [Rollup](https://github.com/rollup/rollup) under the hood. A module bundler compiles small pieces of code into something larger and more complex, such as a library or application. It can generate different bundle formats (UMD, minified UMD, ES and CommonJS).

Setting up and configuration is ridiculously easy. The documentation can be found [here](https://bili.egoist.sh).

1. Install Bili.

    ```bash
    $ npm install --save-dev bili
    ```

2. Create a `bili.config.json` configuration file in the root directory of the project with the following contents.

    ```json
    {
      "input": "<main-entry-point-js>",
      "outDir": "<directory-to-place-generated-files>",
      "format": [<formats-to-generate>],
      "moduleName": "<name-of-your-module>",
      "name": "<name-of-your-module>",
      "filename": "[name][suffix].js",
      "banner": true,
      "target": "<node|browser>"
    }
    ```

    This is an example `bili.config.json` file.

    ```json
    {
      "input": "./src/use-pkg-version-cli.js",
      "outDir": "./dist",
      "format": ["es", "umd", "umd-min", "cjs"],
      "moduleName": "use-pkg-version",
      "name": "use-pkg-version",
      "filename": "[name][suffix].js",
      "banner": true,
      "target": "node"
    }
    ```

3. Add an entry to the `scripts` section in the `package.json` file.

   ```json
   {
     "scripts": {
       "build": "rm -rf dist && bili --config bili.config.json"
     }
   }
   ```
