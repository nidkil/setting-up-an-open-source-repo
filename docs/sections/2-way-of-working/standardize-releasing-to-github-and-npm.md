# Standardize releasing to GitHub and NPM

Manually creating releases for GitHub and NPM is no fun. It is a tedious and error prone process. The process involves the following steps

1. Decide which feature branches you want to release
2. Merge these feature branches into the `master` branch
3. Push the master branch to GitHub
4. Build the release
5. Decide what the next version number should be based on the types of features being released
6. Update the version number in the `package.json` file
7. Create or update the CHANGELOG.md file with information about the features that are part of the release
8. Publishes the release to GitHub
9. Publish the release to NPM

Pray you did it right.

If we have standardized commit messages based on the Conventional Commit standard and use the Semantic Versioning standard why not atuomate the whole process? Yes we can!

- **[Release It!](https://github.com/webpro/release-it)** - Release It! automates the tedious tasks of software releases. It automates the release process based on the Conventional Commit standard and Semantic Versioning standard. O yeah!

