# adWMG Checker: ads.txt / sellers.json

![adWMG Checker](store-assets/promo/marquee-1400x560-logo.png)

Chrome extension (Manifest V3) that validates `ads.txt` and `app-ads.txt` files, cross-references seller IDs with `sellers.json`, detects errors, and analyzes SPO metrics.

## Screenshots

| sellers.json | ads.txt |
| --- | --- |
| ![sellers.json tab](store-assets/screenshots/01-sellers-json.png) | ![ads.txt tab](store-assets/screenshots/02-ads-txt.png) |

| app-ads.txt | Settings and full file |
| --- | --- |
| ![app-ads.txt tab](store-assets/screenshots/03-app-ads-txt.png) | ![Settings panel](store-assets/screenshots/04-settings-and-full-file.png) |

![Owner and manager domains overlay](store-assets/screenshots/05-page-overlay.png)

## Install from source

1. Clone or download this repository.
2. Open `chrome://extensions` and enable **Developer mode**.
3. Click **Load unpacked** and select the repository folder (the one with `manifest.json`).

## Project structure

See [docs/extension-structure.md](docs/extension-structure.md) for the folder layout, asset map and packaging notes.

## License

[GNU AGPL v3.0](LICENSE)
