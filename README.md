# StudyPulse — Website / PWA

A responsive web build of the Study Stress & Burnout Detector. Works on
phones, tablets, laptops and desktops, and can be installed as an app
(PWA) on any of them.

## Run it locally
No build step needed — it's static files.

```
cd website
python3 -m http.server 8080
```
Then open http://localhost:8080 in your browser.

## Deploy it
Upload the whole `website/` folder as-is to any static host:
GitHub Pages, Netlify, Vercel, Cloudflare Pages, or a school server.
Everything is relative-pathed, so it works from a subfolder too.

## Files
- `index.html` — the entire app (UI + logic)
- `manifest.json` — PWA metadata (name, icons, colors) so it can be
  "Added to Home Screen" on phones/tablets or installed on desktop
  Chrome/Edge
- `service-worker.js` — caches the app shell so it keeps working with a
  flaky or offline connection
- `icons/` — app icons (192px, 512px, plus maskable versions for Android)

## Floating mini-monitor (Picture-in-Picture)
Once a session is running, click **⧉ Float** in the top bar (Chrome/Edge
116+, desktop only). It opens a small always-on-top window with the
stress ring, WPM, backspace count, and its own compact typing box — the
popped-out window gets real OS keyboard focus, so typing has to happen
in that little box (not the main tab) for the tracking to keep working
while it's floating. Click "Back to tab" (or close the window) to bring
the widget back into the dashboard; your stats carry over since it's
the same session.


- Layout uses `clamp()` sizing and two breakpoints (600px / 900px) so the
  UI reflows from a single-column phone layout to a two-column
  tablet/desktop layout, with a bottom tab bar on phones/tablets and a
  top tab bar on desktop.
- Mobile viewport height uses the `100dvh`/`100svh` trick (with a JS
  fallback) so the layout doesn't jump when the phone's address bar
  shows/hides.
- All inputs are 16px+ so iOS Safari doesn't auto-zoom on focus.
- `env(safe-area-inset-*)` padding keeps content clear of notches and
  the home-indicator bar on notched phones.
- The typing box auto-scrolls into view when the on-screen keyboard
  opens.
- An extra landscape breakpoint shrinks the stress ring so short
  landscape phone screens don't get cramped.
