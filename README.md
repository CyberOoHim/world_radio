# World Radio — Relax & Listen 📻

> Thousands of live stations, one self-contained page. A cozy, dark-mode PWA for drifting through the world.

**Live Demo:** `https://YOURUSERNAME.github.io/world-radio/` _(replace after deploy)_

![PWA Ready](https://img.shields.io/badge/PWA-ready-7dd3c0?style=flat-square)
![Offline Shell](https://img.shields.io/badge/offline-shell-8b9cf7?style=flat-square)
![No Build](https://img.shields.io/badge/no%20build-vanilla%20JS-070b14?style=flat-square)
![License: MIT](https://img.shields.io/badge/license-MIT-e8c4a0?style=flat-square)

### Features

- **Discover** — Popular worldwide stations by click count
- **Countries** — 200+ countries, filter by continent (uses ISO 3166 flags)
- **Genres / Moods** — 24 curated moods + 120+ tags from Radio Browser
- **Search** — name, city, keyword, debounced
- **Favorites & Recent** — saved in localStorage, persists offline
- **Soft Player** — play/pause, volume, mute, bitrate, error handling, HTTPS upgrade
- **Mobile first** — bottom player, slide-in nav, safe-area insets, 16px input to avoid iOS zoom
- **Installable PWA** — works offline for shell, add to Home Screen

### Install as App

**Android / Desktop Chrome / Edge:**
Open the deployed URL → banner **Install World Radio?** → Install. Or menu → Install app.

**iPhone / iPad (Safari only):**
Open URL in Safari → Share button (square + arrow) → **Add to Home Screen** → Add. Opens standalone, no address bar.

No app store needed. Updates automatically via Service Worker.

### Quick Deploy to GitHub Pages

This repo is already Pages-ready — all paths are relative (`./sw.js`, `./icon-192.png`).

**Web UI (fastest):**
1. Create new public repo `world-radio`
2. Upload these 7 files to the **root** of the repo (not inside a folder):
   ```
   index.html
   manifest.webmanifest
   sw.js
   icon-192.png
   icon-512.png
   icon-192-maskable.png
   icon-512-maskable.png
   apple-touch-icon.png
   ```
3. Settings → Pages → Source: **Deploy from a branch** → `main` / `(root)` → Save
4. Wait ~1 min → `https://YOURUSERNAME.github.io/world-radio/`

**CLI:**
```bash
git init
git add .
git commit -m "init: world radio pwa"
git branch -M main
git remote add origin https://github.com/YOURUSERNAME/world-radio.git
git push -u origin main
# then enable Pages as above
```

### Local Run (no deploy)

**Option A — Same Wi-Fi:**
```bash
python3 -m http.server 8000
# open http://YOUR_LOCAL_IP:8000 on iPad
```

**Option B — Pure iPad only:**
Install **a-Shell mini** → move folder to its Documents → run:
```bash
python3 -m http.server 8000
```
Then open Safari → `http://localhost:8000` → Share → Add to Home Screen. `localhost` is treated as secure, so Service Worker works.

### Project Structure

```
.
├── index.html            # entire app (HTML + CSS + JS, no framework)
├── manifest.webmanifest  # PWA manifest (name, icons, display: standalone)
├── sw.js                 # cache-first shell, network-first API, bypass audio
├── icon-192.png          # any purpose
├── icon-512.png
├── icon-192-maskable.png # maskable (20% safe padding)
├── icon-512-maskable.png
└── apple-touch-icon.png  # 180px for iOS
```

### How It Works

- **API:** [Radio Browser](https://www.radio-browser.info/) community directory. Tries `de1`, `nl1`, `at1`, `fr1` mirrors with 4s timeout fallback.
- **Audio:** Native `<audio>` element, resolves stream via `/json/url/{uuid}` then `url_resolved`. Upgrades `http:` to `https:` when page is secure.
- **State:** Vanilla JS, no build step. Favorites/Recent/Volume in localStorage keys `world-radio:*`.

### PWA Details

- `display: standalone`, `display_override: ["window-controls-overlay"]`
- `theme_color: #0c1222`, `background_color: #070b14`
- Icons: 192/512 any + maskable for adaptive icons
- `sw.js` strategy:
  - Navigation → network-first → cache fallback (`index.html`)
  - `radio-browser.info` → stale-while-revalidate
  - Audio / `.mp3/.aac/.ogg/.m3u8` → never cached (bypass)
  - Everything else → cache-first

To force update after deploy, bump `const CACHE = 'world-radio-v2'` to `v3` in `sw.js`.

### Customization

- **Colors:** edit `:root` CSS vars in `index.html`
- **Moods:** edit `MOOD_TAGS` array at top of script
- **Page size:** change `const PAGE = 40`

### Credits

Streams via [Radio Browser](https://www.radio-browser.info/) — free, open, community-maintained. All station logos/favicons belong to their owners.

### License

MIT — do whatever you want. No attribution required, but a link back is nice.

---
Built for quiet nights and distant signals.
