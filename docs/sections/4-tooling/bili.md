## Bili

!> **IMPORTANT** If you are using [Vue CLI 3](https://cli.vuejs.org/) then you can skip this section as it provides its own packaging tool out of the box.

[Bili](https://github.com/egoist/bili) is a zero-config library bundler that uses [Rollup](https://github.com/rollup/rollup) under the hood. A module bundler compiles small pieces of code into something larger and more complex, such as a library or application. It can generate different bundle formats (UMD, minified UMD, ES and CommonJS).

Setting up and configuration is ridiculously easy. The documentation can be found [here](https://bili.egoist.sh).

## Setup

1. Install Bili.

    ```bash
    $ npm install --save-dev bili
    ```

2. Create a `bili.config.js` configuration file in the root directory of the project with the following contents.

    ```js
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

    ```js
    module.exports = {
      input: './src/use-pkg-version-cli.js',
      outDir: './dist',
      format: ['es', 'umd', 'umd-min', 'cjs'],
      moduleName: 'use-pkg-version',
      name: 'use-pkg-version',
      filename: '[name][suffix].js',
      banner: true,
      target: 'node',
      alias : {
        '@': require('path').resolve(__dirname, 'src')
      }
    }
    ```

3. Add an entry to the `scripts` section in the `package.json` file.

   ```json
   {
     "scripts": {
       "build": "rm -rf dist && bili --config bili.config.js"
     }
   }
   ```
