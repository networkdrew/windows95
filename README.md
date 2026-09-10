# Windows 95 Web Simulation

A single-file, no-build nostalgia trip: a Windows 95 desktop rebuilt in plain HTML/CSS/JS, deployed as a static Cloudflare Worker.

## Apps
- **My Computer** — a fake file explorer with a tiny in-memory filesystem (create/rename/delete folders & text files)
- **Notepad** — a plain textarea, doubles as a viewer for text files opened from My Computer
- **Calculator** — basic arithmetic
- **Paint** — freehand canvas drawing with color/size controls
- **Command Prompt** — a handful of fake DOS commands (`dir`, `cls`, `echo`, `time`, `help`)
- **Control Panel** — clickable applets (Display, Sound, Network, System, Users, Date/Time) that show simple info dialogs
- **Recycle Bin** — deleting a file/folder in My Computer moves it here; restore it or empty the bin permanently
- **Internet Explorer** ("The Internet") — a working address bar with real recreated period websites. Try `www.yahoo.com`, `www.spacejam.com`, or `www.hotmail.com` (or use the Links quick-bar). Anything else returns a retro "cannot display the webpage" error. See `sites/README.md` for how these are built and what's stubbed vs. real.
- **Solitaire** — a simplified single-card-move Klondike (click a card to select it, click a pile to move it there)

## Local dev
Just open `index.html` in a browser — no build step. Or serve it locally:

```
npx http-server .
```

## Deploy
Deployed as a static Cloudflare Worker (see `wrangler.jsonc`) at **windows95.drewcassidy.dev**, linked from the [drewcassidy.dev](https://drewcassidy.dev) hub.

```
wrangler deploy
```
