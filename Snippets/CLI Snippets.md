## Creating numbered items

- `touch file-{m..n}.txt` - Create numbered files (from `m` to `n`)
- `mkdir dir-{m..n}` - Create numbered directories (from `m` to `n`)

## Project Starters

### Astro

```bash
npm create astro@latest
```

### Nuxt

```bash
# Minimal
npx nuxi init <app>

# Content
npx nuxi init -t doc-driven <app>
# OR
npx nuxi init <app> -t content
```

### TailwindCSS

```bash
npm install -D tailwindcss

npx tailwindcss init
```

### Vite

```bash
# Without template
npm create vite@latest

# With template
npm create vite@latest <app> -- --template <template>
```

> [!info]
> Vite templates: `vanilla[-ts]`, `vue[-ts]`, `react[-ts]`, `preact[-ts]`, `lit[-ts]`, `svelter[-ts]`.

### Vue

```bash
npm init vue@latest
```

## Start a local server

### [[NPM]]

```bash
npx live-server
```

### [[Python]]

```bash
python -m http.server 8080
```

### Flask

```bash
# Normal mode
flask --app <app-name> run

# Debug mode: Reload on code change
flask --app <app-name> --debug run
```