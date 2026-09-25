# EvoPlan project page

Static project page for *EvoPlan: Evolutionary Neuro-Symbolic Robot Planning with
Spatio-Temporal Guarantees* (CoRL 2026). It is a single `index.html` plus `static/`, with
no build step and no external dependencies, served by GitHub Pages.

## Layout

```
index.html            the whole page (styles inline)
static/images/        figures rendered from the paper + robot photos
.nojekyll             tells GitHub Pages to serve files as-is
```

## Publish on GitHub Pages (one-time)

1. On github.com, create a new **public** repository, e.g. `evoplan` (no README, no license,
   so the first push is clean). The page will be served at
   `https://<user>.github.io/evoplan/`.
   To serve it from the bare `https://<user>.github.io/` instead, name the repository `<user>.github.io`.
2. Push this folder:
   ```bash
   cd evoplan-website
   git remote add origin git@github.com:Nbhavyasai/evoplan.git
   git push -u origin main
   ```
3. In the repository, go to **Settings → Pages**. Under *Build and deployment*, set
   *Source* to **Deploy from a branch**, *Branch* to **main** and folder to **/ (root)**, then Save.
4. Wait about a minute, then open `https://<user>.github.io/evoplan/`. The Pages settings
   screen shows the live URL once the first deployment finishes (the **Actions** tab shows its progress).

Every later `git push` to `main` redeploys automatically.

## Updating the page

- **Paper / Code buttons:** they currently read *Coming soon*. When a link exists, turn the
  `<span class="btn soon">` into `<a class="btn" href="...">` and drop the `<em>Coming soon</em>` badge.
- **Adding a video:** embed YouTube with
  `<div style="aspect-ratio:16/9"><iframe src="https://www.youtube.com/embed/VIDEO_ID" style="width:100%;height:100%;border:0" allowfullscreen></iframe></div>`,
  or self-host a short H.264 clip (keep it under ~25 MB; GitHub rejects files over 100 MB):
  `ffmpeg -i raw.mov -vf "scale=-2:720" -c:v libx264 -crf 28 -preset slow -an static/videos/demo.mp4`.
- **BibTeX:** add volume and pages once the PMLR entry exists.

## Custom domain (optional)

Add a `CNAME` file containing the domain (e.g. `evoplan.example.org`), point a DNS `CNAME`
record at `<user>.github.io`, and enable **Enforce HTTPS** in Settings → Pages.

## Regenerating figures

Figures under `static/images/` were rendered from the paper source (the Overleaf project) with
TeX Live's Ghostscript (`rungs`). The TikZ overview is compiled standalone with `times` at
the paper's 5.5 in text width so the labels fit their boxes as in the PDF.
