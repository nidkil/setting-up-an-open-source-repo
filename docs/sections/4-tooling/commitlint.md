# commitlint

The `commitlint` tool is a linter that lint's commit messages to enforce the conventional commit standard. We want to check that commit messages comply before they are committed. We do this using the git pre-commit hook using `husky`. Let's install `husky` and `commitlint` and configure them.

1. In the project root directory install `husky`.

   ```bash
   $ npm install --save-dev husky
   ```

2. Install `commitlint` and the conventional commit rules `config-conventional`.

    ```bash
   $ npm install --save-dev @commitlint/config-conventional @commitlint/cli
   ```

3. Add a `commitlint.config.js` file with the following contents that tells commitlint which ruleset to use.

   ```js
   module.exports = {
     extends: ['@commitlint/config-conventional']
   }
   ```

3. Now add the `.huskyrc.json` file to configure `husky` in the project's root directory, so that it knows we want to run `commitlint` before committing to validate that commit messages conform with the conventional commit message standard.

   ```json
   {
     "hooks": {
       "commit-msg": "commitlint -E HUSKY_GIT_PARAMS"
     }
   }
   ```

    With Husky in place, we can add git hooks by adding corresponding npm scripts to `package.json`. With `pre-commit` we can add a pre commit hook that aborts a git commit if the npm script returns an exit code other than 0, which stands for "successful".

4. Add `commitlint` to the `scripts` in `package.json`

   ```json
   {
     "scripts": {
       "commitlint": "commitlint",
       "commitlint:last": "commitlint --edit",
       "git:first": "git rev-list HEAD | tail -n 1",
       "git:last": "git rev-list HEAD | head -n 1"
     }
   }
   ```

   Now we can easily run `commitlint` using `npm run commitlint` and pass it commandline arguments using the double dash (--).

   For the other commands please refer to `Tips & tricks` that follows.

### Tips & tricks

1. Check the last commit message

   ```bash
   $ npm run commitlint --- --edit
   ```

2. Check from a certain commit message

   Find the commit id (sha1 hash) of the commit message you want to check from using:

   ```bash
   $ git log
   ```

   Now check the commit message using:

   ```bash
   $ npm run commitlint --- --from <commit id> --to <commit id>
   ```

3. Check from the first commit message

   Get the first commit id (sha1 hash) using:

   ```bash
   $ git rev-list HEAD | tail -n 1
   ```

   Check the commit messages using:

   ```bash
   $ npm run commitlint --- --from <commit id>
   ```
