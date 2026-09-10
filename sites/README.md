# Simulated 90s websites

Each subfolder here is a self-contained recreation of a real website from
the Windows 95 era, reachable from the desktop's "The Internet" app by
typing its real period address into the address bar (see `IE_SITES` and
`ieNavigate()`/`ieGo()` in `../index.html`).

## Pattern

- `sites/<name>/index.html` is the site's home page, plus whatever other
  real pages it has (`sites/<name>/other-page.html`), plus its own
  `img/` folder for any real downloaded assets it uses.
- Links to another page on the *same* site are normal relative `<a href>`.
- Links to a *different simulated site* (e.g. a Yahoo category page
  linking to Space Jam) call back into the outer app instead of using a
  real `<a href>`, since these pages run inside the IE window's `<iframe>`
  and are same-origin with it:
  ```html
  <a href="#" onclick="parent.ieGo('www.spacejam.com'); return false;">Space Jam</a>
  ```
  This keeps the outer address bar and window title in sync.
- A link to somewhere real but **not yet built** points to a local
  `soon.html` inside that site's own folder — a small period-appropriate
  "under construction" stub — rather than a dead link or a real link
  outside the simulation. Never leave a clickable link with no `href`.
- To add a new site: build its folder, add it to `IE_SITES` in
  `../index.html`, and (optionally) add it to the Links quick-bar.

## Research method

1. Find the right archived snapshot with the Wayback Machine — either a
   direct timestamped URL (`web.archive.org/web/<timestamp>/<url>`) or
   the CDX API (`web.archive.org/cdx/search/cdx?url=<domain>&from=<year>&to=<year>&output=json`)
   to list available captures instead of guessing a timestamp.
2. Pull the real text, structure, and links from that capture.
3. Download just the real images that still resolve (many old captures
   have dead image links — check before relying on one).
4. Hand-clean into a self-contained local page: strip Wayback's own
   rewrite/tracking scripts and any ad/analytics includes, relativize
   links, and route "leaving the site" links per the pattern above.

Don't copy an archived page's HTML wholesale — it comes wrapped in
archive.org's own JS and mostly-dead asset references, and copying every
ad pixel and tracking script bloats the repo with junk nobody wants.

## Status (see the project memory for the live backlog)

| Site | Real pages built | Notes |
|---|---|---|
| `yahoo/` | index, search, entertainment→movies, computers→internet→www→searchengines | Oct 1996 capture. Most home-page links still point to `soon.html`. |
| `spacejam/` | index, lineup, behind, sitemap | Recreated from the real spacejam.com/1996/ page (Warner Bros. still hosts it unchanged). 7 of 10 nav sections still stubbed. |
| `hotmail/` | index (login), signup, inbox | Fully interactive but 100% local — accounts live only in the visitor's own browser `localStorage`/`sessionStorage`, nothing is sent anywhere. No compose/folders yet. |

## Local testing note

`npx http-server` caches aggressively by default
(`Cache-Control: max-age=3600`), which makes re-testing edits in an
already-open browser tab look broken. Serve with `-c-1` while iterating:

```
npx http-server . -c-1
```
