# zevari-assets

Public host for Zevari content assets (PDF carousels, infographic PNGs).

## Why this exists

Zevari's `media_assets_attach_from_url` needs a public URL that serves the file
with the correct `Content-Type`. Google Drive and GitHub-raw both serve PDFs as
`application/octet-stream`, which Zevari rejects. **jsDelivr** (the GitHub CDN)
serves by file extension, so a `.pdf` comes back as `application/pdf` and Zevari
accepts it.

## URL format

```
https://cdn.jsdelivr.net/gh/future-boop/zevari-assets@<commit-sha>/<path>
```

Pinning to a commit SHA makes the URL immutable and purges the CDN instantly
(no cache wait).

## How to publish (automatic)

From the ZEVARI project, run the publish script with any local file:

```powershell
./tools/zevari-publish.ps1 -File "content/2026-W30/fri-carousel.pdf"
```

It copies the file here, commits, pushes, prints the jsDelivr URL, and verifies
the MIME type. Then attach that URL in Zevari with `kind: "document"` for PDFs or
`kind: "image"` for PNG/JPG/GIF.

Folders are organized by month (`YYYY-MM`) by default; override with `-Subdir`.
