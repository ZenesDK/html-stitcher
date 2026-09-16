# 🧵 HTML Stitcher

English | **[Русский](./README.md)**

Merges HTML files into a single file or size-limited parts — right in your browser, nothing is uploaded.

**[Open the app →](https://ваш-домен/)**

![App screenshot](screenshot.png)

## Features

- **Two modes** — a single output file, or parts with a size limit (MB/KB/bytes);
  oversized files are never split — they go into their own part whole
- **Fully local** — files never leave your machine, no network involved
- **Leading zeros** — with 10+ parts names become `total_01.html`, so ordering never breaks
- **Single ZIP** — built right in the browser, no libraries (DEFLATE via CompressionStream)
- **SHA-256** — checksums for every part plus a `sha256sum -c` compatible manifest
- **Preview** — open the result in a new tab before downloading
- **File order** — drag & drop plus ↑ ↓ buttons for keyboard and touch
- **Web Worker** — heavy work runs off the main thread; the UI stays responsive on gigabytes
- **Progress & cancel** — percentage bar, any operation can be aborted
- **List virtualization** — thousands of files without lag
- **RU / EN interface, light & dark themes** — choices are remembered
- **Accessibility** — WCAG 2.1 AA markup and contrast

## Usage

1. Drop `.html` files onto the upload zone (or click to choose)
2. Pick a mode: “Single file” or “Parts by size”
3. Press “Stitch” → download parts separately or as a single ZIP

## Self-hosting

1. **Fork** this repository
2. **Settings → Pages → Deploy from a branch → main / (root) → Save**
3. In a minute the site is live at `https://YOUR_LOGIN.github.io/html-stitcher/`

The app is a single dependency-free `index.html`; no build step required.

## Technical details

| | |
|---|---|
| Dependencies | none — one self-contained `index.html` |
| Stitching | byte-exact concatenation, output matches the sources |
| ZIP | hand-written implementation (STORE + DEFLATE when CompressionStream exists) |
| Hashing | `crypto.subtle.digest` SHA-256 |
| Background work | Web Worker built from an inline Blob (with a main-thread fallback) |
| Requirement | HTTPS or `file://` (SHA-256 needs a secure context) |

## Compatibility

Full functionality (ZIP compression, SHA-256): Chrome/Edge 103+, Firefox 113+, Safari 16.4+.
Older browsers work fine except ZIP compression and checksums.

## Origin

The tool grew out of a small Python script that glued HTML files into 19 MB chunks.
The splitting logic is preserved 1:1 — it just moved into the browser.

## License

[MIT](./LICENSE)