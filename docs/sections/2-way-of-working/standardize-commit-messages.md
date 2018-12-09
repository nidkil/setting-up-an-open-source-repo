# Standardize commit messages
  
When working on a repository with multiple people it is important to standardize the way commit messages are written and enforce this standard. Why think up your own commit message standard if others have already come up with a great standard? Check out the [Conventional Commits](https://www.conventionalcommits.org/en/v1.0.0-beta.2/) standard. This standard streamlines the way commit messages are structured, so that that the releasing process can be automated. The commit messages of changes merged into the master branch can be used to automatically generate a standardized `CHANGELOG.md` and automatically bump the version number. The nice thing of this standard is that it follows the [Semantic Versioning](https://semver.org/) standard that standardizes the way version numbers are incremented (bumped). Very cool.  
  
Advantages of standardizing commit messages:  
- Automatically generating the `CHANGELOG.md` file  
- Automatically determe a semantic version bump based on the types of commits in the release
- Communicating the nature of changes to the team, the public and other stakeholders
- (Automatically) triggering build and publishing processes  
- Making it easier for people to contribute to your projects, by allowing them to explore a (more) structured commit history  
  
There are a number of tools available to help implement, follow and enforce these standards, which we will be setting up in this guide.

- **[husky](https://www.npmjs.com/package/husky)** - Uses the `git commit` and `git push` hooks to validate that the commit messages are inline with the commit standard.  
- **[commitlint](https://github.com/marionebl/commitlint)** - Checks if commit messages meet the [Conventional Commit](https://www.conventionalcommits.org/en/v1.0.0-beta.2/) standard. It by default follows the [Angular conventional commit standard](https://docs.google.com/document/d/1QrDFcIiPjSLDn3EL15IJygNPiHORgU1_OOAqWjiDU5Y/edit), but also offers other standards out of the box or if you feel adventures you can create your own. Read more about it [here](https://github.com/angular/angular.js/blob/master/CONTRIBUTING.md#-git-commit-guidelines).   
- **[commitizen](https://www.npmjs.com/package/commitizen)** - Provides  a cli to interactively help structure commit messages according to the Conventional Commit standard. When you commit with Commitizen, you'll be prompted to fill out any required commit fields at commit time.  
