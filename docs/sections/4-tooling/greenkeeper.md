# Greenkeeper

In short, [Greenkeeper](https://greenkeeper.io) makes sure that you know when your project’s dependency updates break your code.

Greenkeeper sits between npm and GitHub, observing all of the modules your repository depends on. Each time one of them is updated, Greenkeeper opens a new branch with that update. The repository’s CI tests kick in, and Greenkeeper watches them to see whether they pass or not.

Based on the test results and your current version definitions Greenkeeper will open up clear, actionable issues for you. If an update doesn’t break your code, nothing will happen, because everything is fine and no human intervention is required. If things do break, you’ll be informed immediately: you’ll know exactly which update to which dependency caused the problem, and you’ll be nicely set up to fix the problem.

**Prerequisites**

Greenkeeper has a number of requirements for each repository it is meant to watch:

- The repo must have at least one package.json file somewhere in the project
- The repo must have a form of Continuous Integration (CI) that sets commit statuses on branches (like Travis CI, for example, but other services work too)
- The CI must be active on the repo and be allowed to act on new branches
- Issues must be enabled for the repo (careful: issues are disabled by default on forked repositories)
- If you do not have a paid subscription, the repo must be public

If you meet the prerequisites move on to the installation.

1. Install the Greenkeeper GitHub app.

    Install the Greenkeeper GitHub app on the repository’s parent organization or user account (you’ll only need to do this once per account).

    To install, visit [Greenkeeper’s app page on GitHub](https://github.com/apps/greenkeeper) and click Install. If you’ve already installed it somewhere, click on Configure instead. You can then choose which organization or account to install the app in.

2. Grant repository access

    Now set up the Greenkeeper app and tell it which of the account’s repositories to try and watch.

3. Enable Greenkeeper on each repo

   Enable Greenkeeper on that individual repository by merging the Initial Pull Request.

   To set itself up on a repository, Greenkeeper will open an Initial Pull Request. This will attempt to update all dependencies at once, so you’re up to date. In addition, it will add the Greenkeeper badge to your project’s `README.md`. Note that Greenkeeper will only be able to do this if your repository meets all the prerequisites.

   Important: Greenkeeper will only start watching the repository’s dependencies after this pull request has been merged. It will also remind you after a few days in case you forget.

   Also Important: The initial PR will not be opened if all dependencies are already up to date, and the `README.md` already has a badge. In this case, Greenkeeper is silently enabled.

   You can check the status of each repository in the [Greenkeeper Account Dashboard](https://account.greenkeeper.io/).
