# Chrome Extension Structure (MV3)

## Current layout

```text
background/
  background.js
content/
  overlay.js
shared/
  utils.js
ui/
  popup/
    popup.html
    popup.css
    popup.js
  analyzer/
    analyzer.html
    analyzer.css
    analyzer.js
assets/
  icons/
    icon128.png
    iconlogo.png
scripts/
  restructure_sources.sh
store-assets/
  icon/
    store-icon-128x128.png
  screenshots/
    01-sellers-json.png
    02-ads-txt.png
    03-app-ads-txt.png
    04-settings-and-full-file.png
    05-page-overlay.png
  promo/
    small-tile-440x280-logo.png
    small-tile-440x280-ui.png
    marquee-1400x560-logo.png
    marquee-1400x560-ui.png
docs/
  extension-structure.md
manifest.json
README.md
LICENSE
```

## Why this structure

- `ui/popup` and `ui/analyzer` isolate independent UI entrypoints.
- `background` keeps MV3 service-worker logic separate from UI.
- `content` separates injected scripts that run in page context.
- `shared` stores reusable helpers imported by multiple runtime contexts.
- `assets` centralizes static files and keeps icon paths deterministic.
- `scripts/` keeps maintenance scripts outside runtime source.
- `store-assets` holds Chrome Web Store listing graphics; they are uploaded in the developer dashboard, not shipped in the extension.

## Asset map

| File | Size | Used by |
| --- | --- | --- |
| `assets/icons/icon128.png` | 128×128 | `manifest.json` → `icons.128` (toolbar, extensions page) |
| `assets/icons/iconlogo.png` | 170×170 | `ui/popup/popup.html` footer logo |
| `store-assets/icon/store-icon-128x128.png` | 128×128 | Web Store → Store icon |
| `store-assets/screenshots/*.png` | 1280×800 | Web Store → Screenshots (up to 5), README |
| `store-assets/promo/small-tile-440x280-*.png` | 440×280 | Web Store → Small promo tile (pick one) |
| `store-assets/promo/marquee-1400x560-*.png` | 1400×560 | Web Store → Marquee promo tile (pick one), README banner |

## Packaging

The Web Store ZIP must contain only runtime files:

```text
manifest.json
background/
content/
shared/
ui/
assets/
```

Leave `store-assets/`, `docs/`, `scripts/` and `README.md` out of the ZIP.

## Path checklist

1. `manifest.json`
   - `action.default_popup`: `ui/popup/popup.html`
   - `background.service_worker`: `background/background.js`
   - `content_scripts[].js`: `content/overlay.js`
   - `icons.128`: `assets/icons/icon128.png`

2. `ui/popup/popup.html`
   - Local links remain `popup.css` and `popup.js`.
   - Shared utility script remains `../../shared/utils.js`.
   - Footer logo remains `../../assets/icons/iconlogo.png`.

3. `ui/analyzer/analyzer.html`
   - Local links remain `analyzer.css` and `analyzer.js`.

4. `background/background.js`
   - Shared utility import remains `importScripts('../shared/utils.js')`.

## Automation script

Use:

```bash
./scripts/restructure_sources.sh
```

It flattens a legacy `src/`-based tree into root-level extension folders.
