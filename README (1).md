# Williams 3D Equipment Viewer

**Live:** https://cjackman1995.github.io/viewer/

One viewer, any number of models. Share a model by link or QR — no rebuild per model or per customer.

## Files
- `viewer.html` — the viewer. Opens a model by URL: `viewer.html?m=<id>`
- `index.html` — gallery of every model in the catalog
- `models.json` — the catalog. Add a model = add one entry here
- `qr-sheet.html` — printable sheet of QR codes, one per model
- `models/` — put your `.glb` files here

## Add a model (the whole workflow)
1. Drop `your-model.glb` into `models/`
2. Add an entry to `models.json`:
   ```json
   { "id": "castle-ruins", "name": "Castle Ruins", "description": "…", "file": "models/your-model.glb" }
   ```
3. Share `https://YOURSITE/viewer.html?m=castle-ruins` — or print its QR from `qr-sheet.html`

## Hosting on GitHub Pages
1. Create a repo (e.g. `viewer`), add these files + the `models/` folder
2. Settings → Pages → Build from branch → `main` / root
3. Live at `https://<username>.github.io/viewer/`
4. Models under ~100 MB each are fine for a normal Git repo. For many large files, enable **Git LFS**.

## URL options
- `viewer.html?m=<id>` — look up by catalog id (normal case)
- `viewer.html?src=<direct-url-to-glb>` — one-off, skips the catalog

## Notes
- **Real-world AR scale.** For "will it fit in my space?" AR, each `.glb` must be built at true scale (1 unit = 1 meter) using the equipment's real measurements, and the viewer uses `ar-scale="fixed"` so customers see it at genuine size. Meshy/AI exports come out at arbitrary scale, so they must be scaled first.
- AR ("View in your space") works on Android automatically. For iOS AR, add a `.usdz` next to the `.glb` and set `"iosSrc": "models/name.usdz"` in the entry.
- `.glb` files should be served from the same host as the viewer (simplest, no CORS). Avoid serving the raw file straight from Google Drive — its direct links are unreliable for this.
