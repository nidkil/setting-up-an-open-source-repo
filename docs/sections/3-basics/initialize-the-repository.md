# Initialize the repository 

## package.json

All repositories contain a `package.json` file in the root directory of the project. This file holds metadata that is relevant to the project. This file provides information about the project and is used by many tools and also NPM. It describes project as well as handles the project's dependencies. It can also contain other metadata such as a project description, the version distribution, license information, even configuration data.

Create a new project and generate a `package.json` manifest file execute the following commands.

```bash
$ mkdir my-cool-project
$ cd my-cool-project
$ npm init  
```

The last command will ask some questions to generate a basic `package.json` file in your project directory. This file will be updated during the lifecycle of the project when adding additional dependencies and scripts.

After the initial version has been initialized, ensure the `package.json` file contains at least the following settings.
  
```json  
  {
    "name": "<repository name>",
    "version": "<version number>",
    "description": "<short concise description of the project>",
    "keywords": [
      <keywords to categorise the project>
    ],
    "repository": {
      "type": "git",
      "url": "https://github.com/<username>/<repository name>.git"
    },
    "homepage": "<url to the project homepage, can be the GitHub repo itself or GitHub pages>",
    "bugs": "url to the project homepage, can be the repo itself",
    "bin": "./bin/<start script>",
    "author": "<name> <email address> (<homepage>)",
    "license": "<license type>",
    "entry": "src/<entry script>.js",
    "main": "src/<entry script>.js",
    "module": "./dist/<entry script>.js",
    "browser": "./dist/<entry script>.js",
    "unpkg": "./dist/<entry script>.js",
    "files": [
      <files and directories to include in npm module>
    ],
    "scripts": {
      <scripts>
    },
    "dependencies": {
      <runtime dependencies>
    },
    "devDependencies": {
      <development dependencies>
    },
    "engines": {
      "node": ">=6"
    }
  }
```  

Check out [this](https://github.com/nidkil/setting-up-an-open-source-repo) repository for a completely filled out example.

Most of the entries speak for them selves. Just to point out somethings entries that are not in the above example or require additional explanation:
- **private** - If you add `private` and set the value to `true`, then NPM will refuse to publish it. Useful when you only want to publish to GitHub and not NPM. Then there is no chance of accidentally publishing it to NPM when you automate the publishing process.
- **version** - Is the version number of a particular release that should follow the form `major.minor.patch` format. It should initially be set to `0.0.0`. It will be incremented automatically every time we publish a new version to GitHub and/or NPM. More on this later. As explained in [Recommended workflow](sections/2-way-of-working/recommended-workflow.md) incrementing or bumping the version number follows the [Semantic Versioning](https://semver.org/) standard.
- **engines** - This section specifies the node version that the package requires. These settings are advisory. If you want to force the minimum version then you also need to add `engineStrict` and set it to `true`.
  
## Git

Does Git really require an introduction? I don't think so, but we will lend from [Wikipedia](https://en.wikipedia.org/wiki/Git).

> Git is a version-control system for tracking changes in computer files and coordinating work on those files among multiple people. It is primarily used for source-code management in software development, but it can be used to keep track of changes in any set of files. As a distributed revision-control system, it is aimed at speed, data integrity, and support for distributed, non-linear workflows.

Initializing Git is as easy as executing the following command in the root directory of the project.

```bash
$ git init
```

You should setup a remote repository. You can use [GitHub](https://github.com) or [GitLab](https://gitlab.com) or any other hosted git solution. Ones you have created the remote repository you need to link your local and remote repository with the following command.

```bash
$ git remote add origin https://github.com/<username>/<repository-name>.git
```

Now you are all ready to start committing and publishing to GitHub. Don't start yet, we will be adding additional tools to streamline and standardize this process.

> **Note** I will soon provide separate guide with all kinds of useful Git commands you incidentally need and find yourself googling for. More on that later.

Okay, lets add a `.gitignore` file in the root directory of the project and add the following contents.

```bash
node_modules/
.idea/
.env.local
package-lock.json
```

Feel free to add other files that git must ignore.
