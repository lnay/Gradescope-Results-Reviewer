# Gradescope Results Review Helper

## What this is

## How to use

[latest build artifacts](https://gitlab.com/api/v4/projects/45594134/jobs/artifacts/main/download?job=build-job).


## Development

This is an `npm` project which builds a single page application which can be served with just a file server (no node required).
The framework used here is [Svelte Kit](kit.svelte.dev)

### Dev Build

Once you've created a project and installed dependencies with `npm install` (or `pnpm install` or `yarn`), start a development server:

```bash
npm run dev

# or start the server and open the app in a new browser tab
npm run dev -- --open
```

### Production Build

To create a production version of the app:

```bash
npm run build
```

You can preview the production build with `npm run preview`.
