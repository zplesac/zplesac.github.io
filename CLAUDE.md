# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this is

Personal site for Zeljko Plesac (https://zplesac.github.io), built with Hugo and the
[anatole](https://github.com/lxndrblz/anatole) theme. There is no custom code: no
`layouts/`, `assets/`, `data/` or `i18n/` overrides. Everything rendered comes from
the theme plus three Markdown pages in `content/`.

## Commands

```sh
git submodule update --init --recursive   # theme lives in themes/anatole (submodule)
hugo server                               # local preview with live reload
hugo --gc --minify                        # production build into public/ (what CI runs)
```

There are no tests or linters. A successful `hugo` build is the only check.

**Dart Sass is required.** anatole (v1.17.0+) hard-codes the `dartsass` transpiler, so
the build fails without a real Dart Sass binary on PATH. On this machine the `sass`
on PATH can be a broken Ruby gem from rvm; check that `sass --version` prints a Dart
Sass version before you blame the site for a build failure.

## Structure

- `hugo.toml`: site title and description, profile picture, social icons, and the main
  menu (Home / Talks / Resources). Adding a top-level page means adding a
  `content/<page>.md` and a matching `[[menu.main]]` entry here.
- `content/_index.md`: the home page bio.
- `content/talks.md`: a reverse-chronological bullet list of conference talks. New
  talks go at the top, linked to the event or recording when there is a URL.
- `content/resources.md`: links to blog posts, recordings and podcasts.
- `static/images/profile.jpeg`: profile picture referenced from `hugo.toml`.
- `public/` and `resources/` are build output and are gitignored.

## Deployment

`.github/workflows/hugo.yml` builds and deploys to GitHub Pages on every push to
`main`. It pins `HUGO_VERSION` (currently 0.165.0, extended) and installs Dart Sass
with snap. When you upgrade the theme submodule, check that the pinned Hugo version
still meets the theme's minimum. A theme/Hugo mismatch broke the Pages build once
before.
