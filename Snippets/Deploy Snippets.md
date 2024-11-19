## Deploy a Static App to Surge

```yaml
# .github/workflows/deploy.yml
name: Deploy to Surge

on: [push]

jobs:
  build:
    name: Building Project
    runs-on: ubuntu-latest
    strategy:
      matrix:
        node-version: [12.x]

    steps:
      - name: Checkout
        uses: actions/checkout@v2

      - name: Use Node.js ${{ matrix.node-version }}
        uses: actions/setup-node@v1
        with:
          node-version: ${{ matrix.node-version }}

      - name: Install Packages
        run: npm install

      - name: Build Project
        run: npm run build

      - name: Install Surge
        run: npm install -g surge

      - name: Deploy to Surge
        run: surge ./dist ${{ secrets.SURGE_DOMAIN }} --token ${{ secrets.SURGE_TOKEN }}
```

> [!important]
> 
> Requires `SURGE_DOMAIN` & `SURGE_TOKEN` to be defined as secrets in the repo settings.

## Deploy a Vite App to GitHub Pages

```javascript
// vite.config.js

import { defineConfig } from "vite";

export default defineConfig({
  base: "/repo-name/"
});
```

> [!important]
> 
> `https://username.github.io/` -> `base: '/'`
>
> `https://username.github.io/repo-name` -> `base: '/repo-name/'`

```yaml
# .github/workflows/deploy.yml
name: Deploy

on:
  push:
    branches:
      - main

jobs:
  build:
    name: Build
    runs-on: ubuntu-latest

    steps:
      - name: Checkout repo
        uses: actions/checkout@v2

      - name: Setup Node
        uses: actions/setup-node@v1
        with:
          node-version: 16

      - name: Install dependencies
        uses: bahmutov/npm-install@v1

      - name: Build project
        run: npm run build

      - name: Upload production-ready build files
        uses: actions/upload-artifact@v2
        with:
          name: production-files
          path: ./dist

  deploy:
    name: Deploy
    needs: build
    runs-on: ubuntu-latest
    if: github.ref == 'refs/heads/main'

    steps:
      - name: Download artifact
        uses: actions/download-artifact@v2
        with:
          name: production-files
          path: ./dist

      - name: Deploy to GitHub Pages
        uses: peaceiris/actions-gh-pages@v3
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_dir: ./dist
```

---
## Further

### Reads 📄 

- [Deploying a Static Site - Vite](https://vitejs.dev/guide/static-deploy.html#github-pages)
