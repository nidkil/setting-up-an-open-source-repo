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
    "author": "<name> <email address> (<homepage>)",
    "license": "<license type>",
    "repository": {
      "type": "git",
      "url": "https://github.com/<username>/<repository name>.git"
    },
    "homepage": "<url to the project homepage, can be the GitHub repo itself or GitHub pages>",
    "bugs": "url to the project homepage, can be the GitHub repo itself",
    "bin": "./bin/<start script>",
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
    "engines": {
      "node": ">=6"
    },
    "dependencies": {
      <included runtime dependencies>
    },
    "devDependencies": {
      <development dependencies>
    },
    "peerDependencies": {
      <excluded runtime dependencies>
    }
  }
```

Check out [this](https://github.com/nidkil/use-pkg-version) repository for a completely filled out example.

Most of the entries speak for them selves. Just to point out somethings entries that are not in the above example or require additional explanation:
- **private** - If you add `private` and set the value to `true`, then NPM will refuse to publish it. Useful when you only want to publish to GitHub and not NPM. Then there is no chance of accidentally publishing it to NPM when you automate the publishing process.
- **version** - Is the version number of a particular release that should follow the form `major.minor.patch` format. It should initially be set to `0.0.0`. It will be incremented automatically every time we publish a new version to GitHub and/or NPM. More on this later. As explained in [Recommended workflow](sections/2-way-of-working/recommended-workflow.md) incrementing or bumping the version number follows the [Semantic Versioning](https://semver.org/) standard.
- **bin** - A script that executes the library. Useful when you provide a CLI to interact with the library. This script can for example be referenced from the `scripts` section of the `package.json` file.
- **entry** - This entry points to a script that will execute the library. Useful when you provide a CLI to interact with the library.
- **main** - Serves the same purpose as `entry`.
- **module** - Is the entry point when using the library from Node.
- **browser** - Is the entry point when using the library from a browser.
- **unpkg** - This is the UMD build. It is used to distribute the library through the [unpkg](http://unpkg.org/) CDN [1]. For NPM package authors, NPM relieves them from the burden of publishing their code to a CDN in addition to the NPM registry. All the package author needs to do is include the UMD build in their `package.json` file.
- **scripts** - Commands that can be called using `npm run <command>` or `yarn <command>`.
- **engines** - This section specifies the node version that the package requires. These settings are advisory. If you want to force the minimum version then you also need to add `engineStrict` and set it to `true`.
- **dependencies** - Are packages that are installed when running `npm init`.
- **devDependencies** - Are also packages that are installed when running `npm init`, unless the `--production` flag is passed.
- **peerDependencies** - A warning message is shown if missing when running `npm init`. You have to solve these dependencies yourself. When developing for example a plugin the framework you are developing it for can be a peerDependencies as it will be installed as the plugin will be used with the framework.

In addition the `package.json` file can contain sections for other tools. For example the `husky` configuration can either be in a separate configuration file or in the `package.json` file in a section named `husky`.

[1] A content delivery network or content distribution network (CDN) is a geographically distributed network of proxy servers and their data centers. The goal is to distribute service spatially relative to end-users to provide high availability and high performance. CDNs serve a large portion of the Internet content today, including web objects (text, graphics and scripts), downloadable objects (media files, software, documents), applications (e-commerce, portals), live streaming media, on-demand streaming media, and social networks.

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
.DS_Store
node_modules
/dist
/clover

# local env files
.env.local
.env.*.local

# Log files
npm-debug.log*
yarn-debug.log*
yarn-error.log*

# Editor directories and files
.idea
.vscode
*.suo
*.ntvs*
*.njsproj
*.sln
*.sw*
```

Feel free to add other files that git must ignore.
