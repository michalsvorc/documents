# ECMAScript modules

Overview:

- [Pure ESM package](https://gist.github.com/sindresorhus/a39789f98801d908bbc7ff3ecc99d99c)
- [Node.js 18.x documentation](https://nodejs.org/dist/latest-v18.x/docs/api/esm.html)

Tools:

- [ES Module Ready?](https://esmodules.dev/)

## Description

Node.js has two module systems: CommonJS modules and ECMAScript modules.

Authors can tell Node.js to use the ECMAScript modules loader via the .mjs file extension, the package.json "type"
field, or the `--input-type` flag. Outside of those cases, Node.js will use the CommonJS module loader.
