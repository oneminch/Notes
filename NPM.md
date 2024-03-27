- NPM is a package manager for the JavaScript programming language.
- It is the default package manager for [[Node|Node.js]] and is included as a recommended feature in the Node.js install.
- It can manage packages that are local dependencies of a project, as well as globally-installed JavaScript tools.
- For a local project, all the dependencies of a project are managed through the `package.json` file, which specifies a range of valid versions using the semantic versioning scheme, allowing developers to auto-update their packages while at the same time avoiding unwanted breaking changes.
- NPM provides a CLI that can be used to download and install software.

## NPM scripts

- **NPM scripts** are a feature of NPM that allows defining custom scripts in a project's `package.json` file.
    - These scripts can be used to automate various development tasks, such as running tests, building a project, and starting a development server.
- They are easy to use and flexible with some built-in tasks included, such as `npm start` and `npm test`.

## npx

- [npx](https://www.npmjs.com/package/npx) stands for Node Package Execute. 
- It allows us to run packages without having to install them globally.
