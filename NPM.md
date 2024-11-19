- NPM is a package manager for the JavaScript programming language.
- It is the default package manager for [[Node|Node.js]] and is included as a recommended feature in the Node.js install.
- It can manage packages that are local dependencies of a project, as well as globally-installed JavaScript tools.
- For a local project, all the dependencies of a project are managed through the `package.json` file, which specifies a range of valid versions using the semantic versioning scheme, allowing developers to auto-update their packages while at the same time avoiding unwanted breaking changes.
- NPM provides a CLI that can be used to download and install software.

## NPM scripts

- **NPM scripts** are a feature of NPM that allows defining custom scripts in a project's `package.json` file.
    - These scripts can be used to automate various development tasks, such as running tests, building a project, and starting a development server.
- They are easy to use and flexible with some built-in tasks included, such as `npm start` and `npm test`.

## `npx`

- [`npx`](https://www.npmjs.com/package/npx) stands for Node Package Execute. 
- It allows us to run packages without having to install them globally.

## Publishing a Package

### Manual Process

1. Initialize a project with `npm init`.
2. Write package code.
3. Create a `README.md` file and add a license.
4. Test package locally.

```bash
npm install /path/to/package
```

5. Login to `npm` using `npm login`.
6. If package is written in [[TypeScript]], it needs to be compiled to [[JavaScript]].
7. Publish to `npm` and verify package is available online.

```bash
npm publish --access public
```

### Automated Process with GitHub Actions

- Requires `npm` token to be generated from profile.

```yml
# .github/workflows/publish.yml
name: Publish Package

on:
  push:
    branches:
      - main
    # OR
    # tags:
    #   - 'v*.*.*' 

jobs:
  publish:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - name: Set up Node.js
        uses: actions/setup-node@v2
        with:
          node-version: '14'
      - run: npm install
      - run: npm run build
      - run: npm publish
        env:
          NODE_AUTH_TOKEN: ${{ secrets.NPM_TOKEN }}
```

### Versioning

- Before publishing, `npm`'s built-in versioning command can be used to manually update a package version.
- `npm version`
    - updates the version in `package.json`,
    - creates a commit with the message `vX.Y.Z`, and
    - tags the commit with the version number.

```bash
npm version patch  # for a patch update
npm version minor  # for a minor update 
npm version major  # for a major update
```

- The process can be automated when using tools like `semantic-release`.
    - Using [[Git#Conventional Commits|conventional commits]] automatically determines the next version number.

---
## Further

### Videos 🎥

![How To Create And Publish Your First NPM Package](https://www.youtube.com/watch?v=J4b_T-qH3BY)