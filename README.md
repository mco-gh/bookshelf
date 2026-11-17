# Bookshelf

Turn a photo of a bookshelf into an interactive catalogue, in the browser at [mco.dev/bookshelf](https://mco.dev/bookshelf/). Upload a picture and every spine becomes a hotspot: hover over it to see the title, or click for details. Scanning uses Anthropic's Claude with your own API key, and you can try it first on an example shelf without one.

The app is plain HTML, CSS and JavaScript modules: edit the files at the repo root directly, there is no build step for them. Open `index.html` from any web server to run it.

## Vendored code

`build/` only rebuilds the third-party code the page loads from `vendor/`:

- `anthropic.js`: the Anthropic SDK and Zod, bundled for the browser
- `interestfor.min.js`: polyfill for hover tooltips in Firefox and Safari

Run it after upgrading a dependency:

```bash
cd build
npm install
npm run build
```

## Publishing

This repo is mounted in [mco-gh/mco.dev](https://github.com/mco-gh/mco.dev) as a git submodule at `static/bookshelf`, so everything in it is served under `mco.dev/bookshelf/`. After pushing a change here, update the submodule pointer there to publish it:

```bash
cd mco.dev
git submodule update --remote static/bookshelf
git commit -am "Update bookshelf"
git push
```

## Install on a phone

The app is an installable web app: `manifest.webmanifest` describes it, and `sw.js`
is a network-first service worker, so it is always current when online and still
opens offline. Nothing needs bumping on release. The icons in `icons/` are rendered
from the SVG sources by `bash build/icons/render.sh` (needs Google Chrome).
