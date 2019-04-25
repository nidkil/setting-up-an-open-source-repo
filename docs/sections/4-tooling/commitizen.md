# Commitizen

Commitizen is een interactive tool that helps follow the commit message standard.

## Setup

1. Install `commitizen` tool globally.

    ```bash
   $ npm install -g commitizen
   ```

    Alternatively you can install locally, which makes sense if you want other developers to get up and running just using `npm install`.

    ```bash
    $ npm install --save-dev commitizen
    ```

2. Install the `cz-conventional-changelog` module.

    ```bash
   $ commitizen init cz-conventional-changelog --save-dev --save-exact
   ```

3. Verify that Commitizen has been configured automatically by checking if the flowing has been added to the 'package.json' file.

   ```json
   {
     "config": {
       "commitizen": {
         "path": "./node_modules/cz-conventional-changelog"
       }
     }
   }
   ```

   This means that Commitizen has been installed with the Conventional Commit standard adapter installed.

4. Time to start committing

    The following `cz` command has been replaced by an interactive cli.

   ```bash
   $ git cz
   ```

   It interactively guides you through creating a commit message that follows the Conventional Commit standard. Cool or what?

5. Add the command to the `scripts` section of the 'package.json' file, so that it can easily be referenced and used in the future.

   ```json
   {
     "scripts": {
       "cz:commit": "git cz",
       "cz:retry": "git cz --retry"
     }
   }
   ```

   This first command `npm run cz:commit` or `yarn cz:commit` starts the interactive commit session. The second command `npm run cz:retry` can be used if committing failed and you have fixed the issue. It will use the previous information you selected/entered.

