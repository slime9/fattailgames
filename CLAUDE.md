# Fat Tail Games — fattailgames.com

Static marketing site for Fat Tail Games, LLC. Hand-written HTML and CSS, no
build step, no dependencies, no JavaScript.

## Deploying

`git push origin main` **is** the deploy. GitHub Pages serves the repo root of
`slime9/fattailgames`; `CNAME` pins the custom domain. A push goes live in
roughly a minute — there is nothing to build, install, or run locally.

To preview: `python3 -m http.server 8765` from the repo root, then
http://localhost:8765. Use a server rather than opening files directly — every
internal link and asset path is site-absolute (`/styles.css`, `/privacy`) and
will 404 under `file://`.

## Layout

```
index.html         home page
privacy/           SLIP privacy policy  ->  /privacy
404.html           GitHub Pages serves this for unknown paths
styles.css         all styles for every page
favicon.svg        SVG favicon (no .ico or PNG fallback)
robots.txt         allows everything, points at the sitemap
sitemap.xml        list URLs here manually when adding a page
CNAME              fattailgames.com
```

**New pages go in `<name>/index.html`, not `<name>.html`** — that is what gives
the extensionless URL (`/privacy`, not `/privacy.html`).

## Styling

Everything lives in `styles.css`, including page-specific sections, grouped and
labelled by page. One cached request beats several at this size. There is no
preprocessor and no framework — just plain CSS with custom properties.

Colors, fonts, and the text measure are tokens on `:root`. **Use the tokens**;
do not hard-code hex values in new rules — that includes inline SVG, whose
`stroke` and `fill` are set from CSS classes (see `.curve-primary`). The only
literal colors in the repo are in `favicon.svg`, which is a standalone file with
no stylesheet attached.

Reusable pieces worth knowing before writing new CSS:

- `.wrap` — the 780px centered column every section uses
- `.eyebrow` — small uppercase mono label above a heading
- `.meta-line` — mono line prefixed with an accent dot
- `.prose` — long-form body copy, used by the privacy page and any future
  policy page; styles its own `h2`, `p`, `ul`, and accent-dash bullets
- `.masthead` / `.back-link` — the subpage header; the home page has the hero
  instead and no masthead

Dark only, on purpose. `color-scheme: dark` is set and there is no light
palette — don't add `prefers-color-scheme` rules without deciding to support
both properly.

## Per-page head boilerplate

Each page carries its own `<title>`, `description`, `canonical`, and Open Graph
tags. Copy the block from `index.html` and change the values; the canonical and
`og:url` must be the page's real absolute URL.

There is no `og:image` yet — the cards render as `summary`, not
`summary_large_image`. Adding one needs a real 1200×630 PNG.

## Related, but not in this repo

`api.fattailgames.com` is a separate service. It also serves a copy of the SLIP
privacy policy, which is where `/privacy` here was adapted from — the two can
drift, so update both when the policy changes.
