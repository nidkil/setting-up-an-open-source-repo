# Recommended workflow 
  
A lot of the recommendations in this document have to do with the development and release workflow and it is very opinionated! It uses the following [workflow](https://github.com/conventional-changelog/conventional-changelog/tree/master/packages/conventional-changelog-cli#recommended-workflow) as foundation to optimize the workflow. It has been slightly adapted from the original and further clarified.
  
1. Make every change in a separate (feature) branch
2. When applicable include automated tests, code comments and documentation  
3. Commit those changes following the [Conventional Commits](https://www.conventionalcommits.org/en/v1.0.0-beta.2/) standard  
4. Make sure all tests are passing the Continuous Integration (CI) tool (all lights green)
5. Integrate features you want to release into the `master` branch
6. Build the release
7. Bump the version number following the [Semantic Versioning](https://semver.org/) standard and update the version number in the `package.json` file
8. Automatically generate the changelog based on the commit messages that follow the [Conventional Commits](https://www.conventionalcommits.org/en/v1.0.0-beta.2/) standard  
9. Commit the build, `package.json` and `CHANGELOG.md` files  
10. Tag the release with the updated version number
11. Push the version to GitHub  
12. Push the version to NPM
  
!> **Important**: Each change, be it code, documentation, etc., must be made in a separate branch. Branches that are part of a release are merged in to the `master` branch when a release is being prepared. When contributing to a project push your branch to GitHub and send a pull request for that branch to the main repository. The main repository will merge the branch into the `master` branch. Never submit a pull request for a change in the `master` branch itself!
