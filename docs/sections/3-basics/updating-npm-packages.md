# Updating NPM packages

In any project you will want to update package dependencies often. There is a simple NPM tool to help you do this.

**NOTE** You will want to verify any updated packages do not break any existing functionality using automated tests.

## Standard way to update packages

The npm `update` command allows you to update any out-of-date packages, according to the `package.json` versions. This is the default way to update packages with npm.

You can use the npm `outdated` command to find out which packages need to be updated.

## Another way to update packages

Another way is to use the [npm-check-updates](https://www.npmjs.com/package/npm-check-updates) (ncu) module. This package allows you to easily upgrade your `package.json` dependencies to the latest versions of modules regardless of any version constraints in those files. Then with the npm `install` or `update` commands you can upgrade the installed packages.

## Semantic Versioning: Major, Minor, & Patch Version Ranges

npm packages use semantic versioning (semver) as specified on the semver.org website. This means that a package version consist of three components:

- **MAJOR** updated when there are incompatible API changes
- **MINOR** updated when functionality is added that is backwards compatible
- **PATCH** updated when a bug fixes is done that is backwards compatible

node-semver is the package that parses the semver and also understands some additional semver syntax, such as: [Basic Ranges](https://github.com/npm/node-semver#ranges), [Tilde Ranges](https://github.com/npm/node-semver#tilde-ranges-123-12-1), [Prerelease Tags](https://github.com/npm/node-semver#prerelease-tags), [Caret Ranges](https://github.com/npm/node-semver#caret-ranges-123-025-004), [Hyphen Ranges](https://github.com/npm/node-semver#hyphen-ranges-xyz---abc), and [X-Ranges](https://github.com/npm/node-semver#x-ranges-12x-1x-12-).

As a user of npm packages, you can specify which kinds of updates you want to accept in the `package.json` file. For example, if you were starting with a package version 1.0.4, these are three basic ways you could specify which updates to allow:

- Allow **Patch** releases: 1.0 or 1.0.x or ~1.0.4
- Allow **Minor** releases: 1 or 1.x or ^1.0.4
- Allow **Major** releases: * or x

More fine-grained version ranges are also available if you use the additional `semver` syntax mentioned above.

## Install npm-check-updates

Install the npm-check-updates (ncu) tool globally with the following command:

```	
$ npm install -g npm-check-updates 
```

## Checking for updates

Use the following command to see which **local** packages have updates available:

```	
$ ncu 
```

It will list the packages that have updates available with the current version and the installed version.

Use the following command to see which **global** packages have updates available:

```	
$ ncu -g 
```

## Strict vs. non-strict versioned updates

You can either allow for strict versioned updates (strictly within the `package.json semver` constraints) or non-strict versioned updates (to update regardless of the `semver` constraints).

**NOTE 1** `ncu` does not actually update modules, but updates the `semver` numbers of the modules in the `package.json` file. The actual updating is done with `npm install` command.

**NOTE 2** The following commands are only relevant for **local** packages. Global packages need to be updated using `npm install -g <package-name>`.

### Non-strict versioned updates

For non-strict versioned updates, there are several command line options available with `ncu`.

#### Upgrade a specific package

To upgrade a specific package to its newest major version, we use the following command:

```
$ ncu --upgrade <package-name>
```

This updates the `semver` number in the `package.json` file for the specified package.

**NOTE** the ncu tool maintains the existing semantic versioning policies, e.g. "allow only minor upgrades", when updating the `package.json` file. So even if the major version of the specified package was increased, the policy of only allowing minor upgrades upon a npm update is still in effect.

Now we need to install the updated package version using npm install:

```	
$ npm install
```

To check the version fo the specified package use the following command:

```
$ npm list <package-name>
```

#### Upgrade all package

To update all of package dependencies in `package.json` use the following commands:
	
```
$ ncu --upgrade
$ npm install
```

#### Upgrade all package and update semver

The ncu tool can install newer package versions following the `semver` constraints in the `package.json` file, but by default does not update the `semver` to the newer version in the `package.json` file.

If you want to enforce writing those newly installed package versions to the `package.json` file, you can use the `–upgradeAll` option. Though not necessary, this functionality is there if you want it.

```	
$ ncu --upgradeAll
$ npm install
```

#### Upgrading packages using regex

You can also upgrade packages using regular expression (regex) syntax. For example, this would match and upgrade all packages starting with `eslint`:
	
```
ncu --upgrade /^eslint/
```

#### Only process dependencies

To only process `dependencies` and skip the `devDependencies` use the `-p` flag:
	
```
$ ncu -p
```

This can be useful to maintain a stable development environment.
