# EvoPlan project page

Static project page for *EvoPlan: Evolutionary Neuro-Symbolic Robot Planning with
Spatio-Temporal Guarantees* (CoRL 2026). It is a single `index.html` plus `static/`, with
no build step and no external dependencies, served by GitHub Pages.

## Layout

```
index.html            the whole page (styles inline)
static/images/        figures rendered from the paper + robot photos
static/videos/        self-hosted clips (optional; prefer YouTube for long videos)
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

## Videos

PMLR does not accept videos, so the videos live here or on YouTube.

- **YouTube (recommended for anything over ~1 min):** upload as *Unlisted* or *Public*, then
  replace a `.video-slot` div in `index.html` with
  `<div class="video-embed"><iframe src="https://www.youtube.com/embed/VIDEO_ID" title="..." allowfullscreen></iframe></div>`.
- **Self-hosted short clips:** GitHub rejects files over 100 MB and Pages sites should stay under
  1 GB. Keep clips under ~25 MB, H.264 `.mp4`:
  ```bash
  ffmpeg -i raw.mov -vf "scale=-2:720" -c:v libx264 -crf 28 -preset slow -an static/videos/teaser.mp4
  ```
  then use `<video src="static/videos/teaser.mp4" controls muted playsinline></video>`.

## Before announcing the page

Search `index.html` for `TODO` and fill each one:

- [ ] Paper / arXiv / Code button links (remove `class="pending"` once a link is set)
- [ ] Headline video and the four video slots
- [ ] Abstract → camera-ready abstract
- [ ] BibTeX → add volume/pages once the PMLR entry exists
- [ ] Put the page URL in the paper (CoRL requires a link to videos/code in the main text)

## Custom domain (optional)

Add a `CNAME` file containing the domain (e.g. `evoplan.example.org`), point a DNS `CNAME`
record at `<user>.github.io`, and enable **Enforce HTTPS** in Settings → Pages.

## Regenerating figures

Figures under `static/images/` were rendered from the paper source (the Overleaf project) with
TeX Live's Ghostscript (`rungs`). The TikZ overview is compiled standalone with `times` at
the paper's 5.5 in text width so the labels fit their boxes as in the PDF.
