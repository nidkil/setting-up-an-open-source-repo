# JSON Lint

JSON Lint is a validator and reformatter for JSON. It is a pure JavaScript version of the service provided at [jsonlint.com](https://jsonlint.com/).

## Setup

Lets install the `jsonlint` module.

```bash
$ npm install --save-dev jsonlint
```

## Configure

1. Add a script to package.json

    Add the following to the `scripts` section of the `package.json` file:
    
    ```json
    {
      "scripts": {
        "jsonlint": "jsonlin --in-place"
      }
    }
    ```
    
    Use the script as follows:
    
    ```bash
    $ npm run jsonlint -- <filename>.json
    ```
    
    This will lint the json file and update it.

2. Add JSON Lint to `lint-staged`

    To ensure JSON Lint is run with all the other linters add it to the `.lintstagedrc.json` file:
    
    ```json
    {
      "*.json": [ "jsonlint --in-place", "git add" ]
    }
    ```
    
    This will lint staged JSON files in the pre-commit hook and commit the changes back before actually committing the files.
