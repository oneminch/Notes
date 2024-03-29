## [[Terminal]] 📄

## [[Git]] 📄

## [[SSH]] 📄

## [[NPM]] 📄

## [[Transpilers]]

- **TypeScript** is a superset of [[JavaScript]] that adds [[Statically-Typed Language|static typing]] and other features, and it includes a [[Transpilers|transpiler]] that converts TypeScript code to JavaScript code.

- **Babel** is a free and open-source JavaScript compiler that converts modern JavaScript code that may not widely supported into a backwards-compatible version.
    - It can also be used to compile TypeScript into JavaScript
    - It is primarily used to convert ECMAScript 2015 (ES6) and later versions of JavaScript into backwards-compatible code.
    - It can automatically inject polyfills provided by `core-js` for support features that are missing entirely from JavaScript environments.
    - It can be used with build tools such as Webpack, Rollup, and Parcel, or as a standalone tool.

```json
// .babelrc
{
    "presets": ["@babel/preset-env"]
}
```

## [[Linters]] & [[Formatters]]

-  **ESLint** is a code linter that supports emerging JavaScript syntax.
    - It supports configuring rules on a per-project, per-file, and per-line basis, and comes with several hundred built-in rules. 
    - It also can be extended by loading additional rules from community plugins.

```json
// eslintrc.json
{
    "extends": [
        "eslint:recommended",
        "@babel/eslint-plugin",
        "plugin:react/recommended",
        "plugin:jest/recommended",
        "plugin:node/recommended"
    ],
    "rules": {
        "no-console": "warn",
        "no-unused-vars": "error",
        "react/react-in-jsx-scope": "off"
    }
}
```

- **Prettier** is a popular JavaScript formatter that enforces a consistent style throughout a codebase by parsing code and reprinting it according to its own rules.

```json
// .prettierrc
{
    "trailingComma": "es5",
    "tabWidth": 4,
    "semi": false,
    "singleQuote": true
}
```

## [[Bundling|Bundlers]] 📄

### Webpack

- Webpack is a module bundler that can be used to bundle JavaScript files for usage in a browser, as well as transform and bundle other types of files.
- It supports all browsers that are ES5-compliant, and may require the use of polyfills for older browsers that do not support certain features.
- It can be used to apply transformations to HTML, CSS, and JS files before including them in the bundler.
- It can be configured to use the `@babel/preset-env` preset to convert modern JavaScript code into a backwards-compatible version that can run on older JavaScript engines.
- The `@babel/preset-typescript` preset can be used to compile TypeScript code into JavaScript.

- The `webpack.config.js` file is where the configuration happens.
    - `entry` specifies the entry point for the dependency graph, and it can be set to a single file or multiple files.
    - `output` specifies where the bundles should be emitted and how they should be named.
    - `mode` can be set to `development`, `production`, or `none` to enable different built-in optimizations.
- Loaders allow Webpack to process other types of files and convert them into valid modules that can be consumed by your application.
- Plugins can be used to extend the functionality of Webpack and perform tasks such as code splitting, optimization, and runtime analysis.

```js
// webpack.config.js
const path = require('path');

module.exports = {
    entry: './src/index.js',
    output: {
        filename: 'bundle.js',
        path: path.resolve(__dirname, 'dist'),
    },
    module: {
        rules: [
            {
                test: /\.js$/,
                exclude: /node_modules/,
                use: {
                    loader: 'babel-loader',
                    options: {
                        presets: ['@babel/preset-env'],
                    },
                },
            },
            {
                test: /\.css$/,
                use: ['style-loader', 'css-loader'],
            },
        ],
    },
    plugins: [],
    mode: 'development',
};

```

### Other Bundlers

- **Rollup** is another popular JavaScript module bundler that is designed to be highly configurable and customizable. 
    - It is designed to be used for bundling JavaScript code into a format that can be used in a browser, and it supports a wide range of plugins and loaders for customization. 
    - It is particularly well-suited for bundling libraries and modules for use in other projects.

- **Parcel** is a web bundler that is designed to be simple and easy to use, with minimal configuration required. 
    - It is designed to be used for bundling web applications, and it supports a wide range of plugins and loaders for customization.
    - It is known for its zero configuration approach, meaning that it can automatically detect and bundle all assets and dependencies without requiring any configuration from the user.

- **Esbuild** is a JavaScript bundler and minifier that is designed to be extremely fast and lightweight. 
    - It is written in Go and is designed to be highly parallelized, making use of all available CPU cores to optimize the build process. 
    - It is particularly well-suited for large-scale projects and applications that require fast build times.

- **SWC** is a Rust-based platform for the web that provides fast and powerful tools for JavaScript and TypeScript.
    - It can be used for compilation, bundling, minification, transformation, and more.
    - It is used by popular frameworks and tools such as Next.js, Parcel, and Deno.

- **Vite** is a next-generation web bundler that leverages the power of native ES modules to deliver a fast and efficient development experience for modern web projects. 
    - It consists of a dev server that serves files over native ES modules, and a build command that bundles the code with Rollup.
    - It is designed to be simple and easy to use, with sensible defaults and minimal configuration.

- **Turbopack** is an incremental bundler and build system optimized for JavaScript and TypeScript, written in Rust. 
    - It is designed to be fast and efficient, and is built into Next.js as the default bundler for local development. 
    - It is designed to be used for bundling JavaScript and TypeScript code for use in a browser, and it supports a wide range of plugins and loaders for customization.

---
## Further

### Podcasts 🎙

<iframe src='https://podverse.fm/embed/player?episodeId=CIW8GYmDGM' title='Podverse Embed Player' class='pv-embed-player'>Syntax - How to Get Better at Debugging</iframe>

### Reads 📄

- [67 Weird Debugging Tricks Your Browser Doesn't Want You to Know (Alan Norbauer)](https://alan.norbauer.com/articles/browser-debugging-tricks)