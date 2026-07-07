# OsamaDabb.github.io

Personal portfolio/blog site for Osama Dabbousi, hosted on GitHub Pages at
`osamadabb.github.io` (repo: `OsamaDabb/OsamaDabb.github.io`). Plain static
HTML/CSS/JS — no build step, no Jekyll, no framework. Pages are served as-is.

Base theme is "Miniport" by HTML5 UP (`assets/css/main.css`, `assets/js/*`),
with site-specific overrides layered in `assets/css/custom.css` (loaded after
`main.css`, so it wins the cascade). Prefer editing `custom.css` over touching
`main.css`.

## Pages

- `index.html` — landing page
- `work.html` — portfolio grid, blog listing, and news mentions (sections:
  `#portfolio`, `#blog`, `#news`)
- `contact.html`
- `blog-*.html` — individual long-form blog posts (see below)

## Adding a new blog post

1. Copy an existing `blog-*.html` as a template, or use the placeholder
   comment block already present in unfinished posts:
   ```html
   <!-- PASTE YOUR POST CONTENT BELOW THIS LINE ... -->
   <p><em>Coming soon.</em></p>
   <!-- END OF POST CONTENT -->
   ```
2. Fill in `<title>`, `meta description`, and all `og:`/`twitter:` tags in
   `<head>` — these are currently NOT auto-generated and must match the post's
   actual content (they've drifted out of sync before).
3. Set the `<h2>` and byline `<p>` in the "Post Header" article.
4. Wrap body content in `<div class="post-body">` — this class (defined in
   `custom.css`) supplies paragraph/heading/list spacing and image sizing
   helpers so you don't have to hand-style every element:
   - `<p>` — standard paragraph
   - `<h3>` — section heading
   - `<span class="image fit">...</span>` — full-width image or
     `<video autoplay loop muted playsinline>` (used for large diagrams/demo
     clips)
   - `<span class="image inline">...</span>` — small centered image, capped
     at 320px wide (used for asides like the XKCD comic in the thesis-defense
     post)
   - `<span class="image small">...</span>` — small centered image capped at
     250px tall (used for the closing photo in the thesis-defense post)
5. Add the post to the `.blog-list` in `work.html` (`<h3><a href="...">`,
   teaser `<p>`, and `.blog-meta` tag(s)). Remove the `<span class="soon-tag">`
   once the post is actually live — its presence is what marks a post as
   "Coming Soon" on the listing page.
6. There is no math renderer (no KaTeX/MathJax) anywhere on the site. Write
   any equations as plain italicized text (e.g. `<em>dx/dt</em>`), not LaTeX.

Existing `tech-box` variants (in `main.css`): `python`, `pytorch`, `tiledb`,
`cpp`, `tensorflow`, `cuda-cpp`, `matplotlib`, `cupy`, `pyvista`. For a tag
that doesn't fit a technology (e.g. a non-technical post), use the inline
style pattern from `blog-teaching.html`:
`<span class="tech-box" style="background:#e2e8f0;color:#1e293b;">Label</span>`.

## Media conventions

- All images/videos live flat in `images/` (no subfolders).
- Photos/screenshots dropped in at full camera/screenshot resolution should be
  resized and compressed before committing — e.g.
  `convert input.png -auto-orient -resize 1800x -strip -quality 85 output.jpg`.
  Check `-auto-orient` in particular: phone photos often carry EXIF rotation
  that `identify`/plain `convert` will otherwise ignore, leaving the image
  sideways.
- Prefer JPEG over PNG for photos (much smaller for near-identical visual
  quality); keep PNG only for graphics with flat colors/text where JPEG
  artifacts would show.
- Video files (manim animations, simulation captures) are committed directly
  as MP4 — no size problems so far (largest is ~18MB; GitHub's hard limit is
  100MB/file, soft repo-size guidance is ~1GB). Existing convention for
  in-post animations: `<video autoplay loop muted playsinline>` (no visible
  controls — they're meant to loop ambiently while the reader reads, matching
  the homepage/work.html portfolio video treatment).

## Theming

Colors are CSS custom properties in `custom.css` (`--bg`, `--text`,
`--accent`, `--nav-bg`, `--nav-text`, `--box-bg`, `--surface`), with a
`@media (prefers-color-scheme: dark)` override block. Respect these variables
rather than hardcoding colors when adding new components, so dark mode stays
consistent.
