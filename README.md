# SEO guides site (GitHub Pages)

Ready-to-publish copy of the three SEO articles, as a plain Jekyll site
(GitHub Pages default `minima` theme — no workflow files, no build step).

## Files

- `_config.yml` — site title/description, `minima` theme.
- `index.md` — home page listing the three guides + both Gumroad links.
- `how-to-format-chinese-thesis-word.md` — article 1 (2026-11-07).
- `gbt9704-official-document-word.md` — article 2 (2026-11-08).
- `npp-plugin-zero-to-plugins-admin.md` — article 3 (2026-11-09).

The internal "Target keywords / Publish to" footer was stripped from the
published copies; the originals in `../seo/` are untouched.

## To publish (George, ~2 minutes in the browser)

1. On github.com, create a new **public** repository named `guides`
   (empty — no README, no .gitignore, no license, so the push lands clean).
   The GitHub App cannot create repositories, which is why this step is yours.
2. Tell Muse "guides 建好了" — Muse pushes these files into it
   (pushing to an existing repo works fine).
3. In the repo: Settings → Pages → Source: "Deploy from a branch" →
   Branch `main`, folder `/ (root)` → Save.
4. The site goes live at `https://zhgao.github.io/guides/` within a minute
   or two. Check all three article links open.

## Still separate: dev.to cross-post

Cross-posting each article to dev.to still needs a logged-in dev.to
session in George's browser — that step is not covered by this package.
