# Stride

A personal running and walking log. Paste a session summary, and it becomes one day on the graphs.

Installable as a PWA — once installed it opens in its own window with no browser address bar or tabs, and works offline.

## What's in here

```
index.html             the whole app (markup, styles, logic — one file)
manifest.webmanifest   PWA manifest: name, icons, standalone display
sw.js                  service worker: offline app-shell cache
icons/                 app icons (192, 512, maskable, apple-touch, favicon)
.nojekyll              tells GitHub Pages to serve every file as-is
```

Everything uses relative paths, so it works both at the root of a domain and under
`https://<user>.github.io/<repo>/` without edits.

## Publishing on GitHub Pages

1. Create a new repository on GitHub.
2. Upload the contents of this folder — `index.html` must sit at the repository root,
   not inside a subfolder.
3. Go to **Settings → Pages**.
4. Under **Source**, choose **Deploy from a branch**, pick `main` and the `/ (root)` folder, then save.
5. Wait a minute, then open `https://<your-username>.github.io/<repo-name>/`.

HTTPS is required for a service worker, and GitHub Pages serves HTTPS by default, so
nothing further is needed.

## Installing it as an app

- **Android / Chrome:** open the site, then menu → *Install app* (or *Add to Home screen*).
- **iPhone / iPad, Safari:** open the site, tap Share → *Add to Home Screen*. iOS only
  installs PWAs from Safari.
- **Desktop Chrome or Edge:** open the site and click the install icon at the right of
  the address bar.

Launched from the home screen or app list, it runs standalone — full screen, no browser
chrome.

## Adding a session

Tap **Add**, paste something like:

```
Morning Run, Date: 17 September 2026, Distance: 2.06 km, Average Pace: 10:52/km,
Moving Time: 22:25, Elevation Gain: 16 m, Max Elevation: 918 m, Steps: 2,904.
```

The values are read on-device — no network call. Labels it understands: date, distance,
average pace, moving time, elevation gain, max elevation, steps. Order doesn't matter,
one line or several both work. Miles and feet are converted to km and metres. Dates can be
`17 September 2026`, `Sep 17, 2026`, `17/09/2026` or `2026-09-17`.

Every value stays editable on the review screen, and the date is required before saving.
Two sessions on the same date are supported — you'll be asked whether to update the
existing one or add another.

## Where your data lives

In this browser's `localStorage`, on this device only. Nothing is uploaded anywhere and
there is no account.

That also means clearing site data, or deleting the app, erases it. Use **Export backup**
at the bottom of the history page to save a JSON file, and **Import backup** to restore it
or move to another device.

## Updating the app later

Edit `index.html`, bump `VERSION` in `sw.js` (for example `stride-v2`), and push. The
version bump is what makes installed copies fetch the new build instead of serving the
old cached one.
