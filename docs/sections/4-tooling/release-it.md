# Release It!

Release It! automates the tedious tasks of software releases. It automates the release process and is based on the Conventional Commit standard and Semantic Versioning standard. What does it do?

1. Build the release
2. Bump the version number and updates the `package.json` file
3. Generates the CHANGELOG.md
4. Commit the changes to git and tag it
5. Pushes the release to GitHub and/or NPM

If you have ever done this process manually, then you know what a big deal and time saver this is!

> **Prerequisites**: The repository must exist on GitHub. If the repository was first created locally it must have been published to the GitHub repo.

1. Install `release-it` using npm.

    ```bash
    $ npm install --save-dev release-it
    ```

2. Add `release-it` to the `scripts` section of the `package.json` file.

    ```json
    {
      "scripts": {
        "release": "release-it --verbose"
      }
    }
    ```

    By default, Release It! runs in interactive mode and allows you to confirm each task before execution. By using the `-n` option (i.e. non-interactive), the process is fully automated without prompts. To pass the `-n` option when using `npm run` use the double dash (--), i.e. `npm run release -- -n`.

    **Pro tip**: if you break off the release process `release-it` before the changes have been committed to git `release-it` will have updated a few files. To revert this just run the following git command.

    ```bash
    $ git checkout .
    ```

3. Add a basic `.release-it.json` configuration file.

    ```json
    {
      "src": {
        "commitMessage": "chore: release v${version}",
        "tagName": "v${version}",
        "tagAnnotation": "chore: release v${version}"
      },
        "github": {
          "release": true
        }
    }
    ```

    > **IMPORTANT** It is important that the `commitMessage` conforms with the Conventional Commit standard or commitlint will throw an error when release-it tries to commit the changes it makes.

    This defines the commit message, commit tag and enables publishing to GitHub.

    For all configuration options checkout the [defaults](https://github.com/webpro/release-it/blob/master/conf/release-it.json).

4. Create a GitHub token

    To automate releasing to GitHub `release-it` requires a GitHub `personal access token` to authenticate itself when pushing releases. Personal access tokens function like ordinary OAuth access tokens. They can be used instead of a password for Git over HTTPS, or can be used to authenticate to the API over Basic Authentication.

    - Open a browser and go to [GitHub](https://github.com)
    - Login to GitHub
    - Go to settings (click on the dropdown with your avatar in the top right corner and select `Settings`)
    - Select the option `Developer settings` (at the bottom of the list)
    - Select the option `Personal access tokens` (at the bottom of the list)
    - Enter the name for the token, i.e. `release-it`
    - Select the following OAuth scopes (permissions): repo:status, repo_deployment, pubic_repo [1]
    - Click `Generate token`
    - Copy the generated `personal access token`, since it will only be displayed once!
    - Create an environment file `.env.local` and add the copied `personal access token` with the key `GITHUB_TOKEN` [2]

        ```
        GITHUB_TOKEN=<the-copied-github-token>
        ```

        [1] Always select the minimum number of permissions to limit the damage if the token is ever exposed. Only check the sub permissions, never the top level groups!

        [2] The `.env.local` file MUST never be published to GitHub or NPM. Mmake sure `.env.local` is in the `.gitignore` file, as NPM will also use this as ignore file if the `.npmignore` file does not exist.

    **Pro tip**: you could go directly to the token page and generate a token by opening up a browser and going to [https://github.com/settings/tokens](https://github.com/settings/tokens)! But now you know how to get there through the settings :-)

5. Setup the GitHub token

    We will use the cool [`node-env-run`](https://www.npmjs.com/package/node-env-run) module to dynamically set the GITHUB_TOKEN environment variable when we execute `release-it`, using the `.env.local` file we created in the previous step.

    - Install `node-env-run` using npm.

        ```bash
        $ npm install -g node-env-run
        ```

    - Change the `release-it` script in the `package.json` file.

        ```json
        {
          "scripts": {
            "release": "nodenv --env ./.env.local --exec release-it --verbose"
          }
        }
        ```

    Now we are ready to release to GitHub using `npm run release` or `yarn release`.

    Lets take it a step further and also publish to NPM.

6. If you are publishing to NPM, create a NPM account if you do not already have one.

    Run the following command and enter your: username, password and email address.

    ```bash
    $ npm login
    ```

    You will receive an email to confirm your email address. Go confirm it!

7. Lets enhance the `.release-it.json` configuration file.

    ```json
    {
      "dry-run": false,
      "requireCleanWorkingDir": true,
      "non-interactive": false,
      "verbose": false,
      "pkgFiles": ["package.json"],
      "disable-metrics": true,
      "increment": "conventional:angular",
      "beforeChangelogCommand": "conventional-changelog -p angular -i CHANGELOG.md -s",
      "changelogCommand": "conventional-changelog -p angular | tail -n +3",
      "safeBump": false,
      "buildCommand": "npm run build",
      "src": {
        "commitMessage": "chore: release v${version}",
        "tagName": "v${version}",
        "tagAnnotation": "Release v${version}",
        "beforeStartCommand": "npm run test && npm run lint:error-only"
      },
      "github": {
        "release": true,
        "releaseName": "🚀 Release ${version}",
        "tokenRef": "GITHUB_TOKEN"
      },
      "npm": {
        "publish": true,
        "tag": "latest"
      }
    }
    ```

    Now release-it does all the magic:
    - Building a new release
    - Publishing to GitHub
    - Publishing to NPM

    O yeah!

8. Release it!

    Okay now everything is setup lets do our first release. Execute the following command and follow the prompts :-)

    ```bash
    $ npm run release
    ```
