# Gradescope Re(sults viewer)

## What this is

`Gradescope Re(sults viewer)` is a web-app intended to be run locally with a downloaded export of the submissions for a [gradescope](www.gradescope.com) assignment. The goal is to give a convenient way to view the autograder results as well as the submission files, just as you can in gradescope. However, it also tries to help transition to testing the assignment files locally (only tries for jupyter notebooks atm).

## Main limitations

- Functions with gradescope's assignment export format as of April 2023 (this could in principle change)
- Only let's you view files from an assignment with names that are hardcoded into the app (search `src/` for "SUBMISSION_FILES")
- Only made to view python scripts and jupyter notebooks among the submission files

## Project development status

This was just something I slapped together for an assignment I was going to mark. I've only neatened it up for it to be open-sourced. This could be worked on to be useful for more general assignments, but won't be receiving any work from me unless there's some interest in it (feel free to make/comment on issues). 

## How to use

Download the
[latest build artifacts](https://gitlab.com/api/v4/projects/45594134/jobs/artifacts/main/download?job=build-job),
extract them, place the extracted gradescope export in the `build` directory, and rename this export directory to `submissions`.

Now the directory structure should look something like this:
```
build
├── 200.html
├── _app
│   ├── immutable
│   └── version.json
├── favicon.png
├── index.html
└── submissions
    ├── submission_565951130
    ├── submission_866516953
    .
    .
    .
```
From inside the `build` directory, start up a simple file server. For example, you can do this with Python3 by running the command `python -m http.server` and open up `localhost:8000` in the browser.
Optionally you can also start a jupyter server from inside the `build/submissions` directory (`jupyter notebook .`).

## Potential feature ideas

Make this more easily adapted for different types of assignments:
- Externalise the submission file list so that changes don't require a rebuild of the app
- Allow for viewing more file types (non-python code files, PDFs, images...)
- Add convenient ways to open/view/test common submission file types with other application (extensible something something?)

Help with the iteration-speed of building+testing a gradescope autograder (maybe a better scope of a sister project):
- Allow testing of an autograder on locally downloaded submissions from `setup.sh` and `run_autograder` files
- Dockerfile based `FROM` published gradescope container (docker.io/gradescope/autograder-base)
- Review tested autograder results

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

This builds the application into the `build` directory.

You can preview the production build with `npm run preview`.
