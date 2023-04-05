# Npm packages

Resources:

- [Developers](https://docs.npmjs.com/cli/v7/using-npm/developers#before-publishing-make-sure-your-package-installs-and-works)
- [Publishing unscoped public packages](https://docs.npmjs.com/creating-and-publishing-unscoped-public-packages)
- [package.json](https://docs.npmjs.com/cli/v6/configuring-npm/package-json)

CLI:

- [npm](https://docs.npmjs.com/cli/v7/commands)
- [yarn](https://yarnpkg.com/cli/)

Blogs:

- [How to build, test, and publish a TypeScript npm package in 2022](https://www.strictmode.io/articles/build-test-and-publish-npm-package-2022)

## Publishing

See minimal [package.json](https://docs.npmjs.com/cli/v7/using-npm/developers#the-packagejson-file) documentation.

Additional package.json fields:

- [main](https://docs.npmjs.com/cli/v7/configuring-npm/package-json#main)
- [repository](https://docs.npmjs.com/cli/v7/configuring-npm/package-json#repository)
- [keywords](https://docs.npmjs.com/cli/v7/configuring-npm/package-json#keywords)

Changelog is documented in repository releases.

### Including files

- [files](https://docs.npmjs.com/cli/v6/configuring-npm/package-json#files)

The optional files field is an array of file patterns that describes the entries to be included when your package is
installed as a dependency.

- [directories](https://docs.npmjs.com/cli/v6/configuring-npm/package-json#directories)

You can indicate the structure of your package using a directories object. If you specify a `bin` directory, all the
files in that folder will be added as executable from CLI.

### Test locally

Preview what will be published: 

```shell
npm publish --dry-run
```

Link local package directory as package in npm_modules:

- [Avoid npm link](https://hirok.io/posts/avoid-npm-link)

Instead of using `npm link`, use `npm install` or `npx link` to symlink a local package as a dependency:

```shell
npx link <path to package>
```
