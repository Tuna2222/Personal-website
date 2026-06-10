# Agent Notes

## Repo Shape
- This is a Hugo Apéro personal site with blogdown/RStudio wiring, not a Node app or R package.
- Main source of truth: `config.yaml` plus `content/`; root `README.md` is only a short site link.
- The theme is vendored under `themes/hugo-apero/`. Do not treat `themes/hugo-apero/assets/academicons/package.json` as repo-level npm tooling.

## Commands
- Netlify production build is `hugo`, publishing `public/` (`netlify.toml`).
- Netlify branch/deploy previews use `hugo -F -b $DEPLOY_PRIME_URL`.
- Hugo is pinned to `0.98.0` in both `netlify.toml` and `.Rprofile`; use that version for parity when possible.
- The `gh-pages` Netlify context intentionally runs `true` and publishes `.`.

## Content And Layout
- Top-level menu/content sections are wired in `config.yaml`; existing source sections include `content/Research/`, `content/collection/`, `content/story/`, and `content/recipe/`.
- Section `_index.md` files carry important Apéro front matter (`cascade`, `layout: list-sidebar`, sidebar labels). Preserve that pattern when adding pages.
- Paths may contain spaces, uppercase names, and Unicode, e.g. `content/Research/Course projects/` and `content/recipe/炖菜/`; quote paths in shell commands.
- Raw HTML is allowed by `markup.goldmark.renderer.unsafe: yes`, and existing Markdown uses inline HTML.
- The only repo-level layout override found is `layouts/shortcodes/blogdown/postref.html`; most rendering behavior comes from the vendored theme.

## Generated Or Ignored Files
- Do not edit generated build output in `public/` or `resources/_gen/` unless the task explicitly targets generated artifacts.
- Hugo ignores `.Rmd`, `.Rmarkdown`, `_cache`, `.knit.md`, and `.utf8.md` per `config.yaml`; blogdown/RStudio handles R Markdown generation before Hugo sees content.
- `R/build.R` and `R/build2.R` are placeholder pre/post-build hooks, not active custom build logic.

## Verification Notes
- No repo-root lint, typecheck, test config, CI workflow, `package.json`, `DESCRIPTION`, or `renv.lock` was found.
- For content/config changes, the closest repo-declared verification is a Hugo build with the pinned Hugo version.
