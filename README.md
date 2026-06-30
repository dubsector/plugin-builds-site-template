# plugin-builds-site-template

A GitHub Pages landing page template for automated Minecraft plugin build pipelines — pulls the latest GitHub Release via the API and renders a download card with build metadata, Sigstore/SLSA verification commands, and a build history table.

This is the style used by [mcmmo-builds](https://github.com/dubsector/mcmmo-builds) and [coreprotect-builds](https://github.com/dubsector/coreprotect-builds). Copy `docs/index.html` as-is and customize the marked spots below — don't re-derive the CSS or markup from scratch, or you'll end up with subtle drift (wrong color tokens, missing fonts, mismatched spacing) like coreprotect-builds did before this template existed.

## Quick start

1. Copy `docs/index.html` into your new repo.
2. Edit the `<script>` config block at the top: `PLUGIN_NAME`, `REPO`, `UPSTREAM_REPO`.
3. Update the two `TODO`-marked regexes (`parseName`, `getMcRange`) to match your release title format and however your release body states the supported MC version range.
4. Update the static HTML: `<title>`, nav `Star` link `href`, `.nav-title`, hero `<h1>`/`<p>`, and the `<footer>` copyright/license/repo links.
5. In your repo settings, enable **Pages → Deploy from a branch → `/docs`** on your default branch.
6. Make sure your release workflow publishes GitHub Releases with: a `.jar` asset, a `.sigstore.json` bundle, and an `.intoto.jsonl` provenance file (the verify-block commands assume these exist). See mcmmo-builds' or coreprotect-builds' `.github/workflows/build.yml` for a full pipeline example (cosign signing + SLSA attestation + smoke tests).

## Variants

- **Single release track** (this template): one "Latest" card + a history table. Use this if your plugin only publishes one kind of build.
- **Multiple release tracks** (e.g. stable + dev): see [coreprotect-builds/docs/index.html](https://github.com/dubsector/coreprotect-builds/blob/master/docs/index.html) for the side-by-side `.top-grid` two-column extension of this same base style — same tokens and components, just an additional layout layer for projects that publish more than one track.

## Structure

- `:root` CSS custom properties — color tokens, radius, fonts. Don't change these; they're what keeps every builds site visually consistent.
- `.download-card` / `.meta-item` / `.verify-block` — the latest-release card.
- `.builds-wrap` / `.builds-table` — the history table for older releases.
- `.loading` / `.error-msg` — fetch states.
- Nav has a `max-width: 480px` media query so it doesn't overflow on narrow phones — keep it if you add/remove nav items, re-check it still fits.
