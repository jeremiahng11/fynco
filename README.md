# Fynco — Onboarding Simulation

A single-file HTML5 PWA-installable onboarding flow for a multi-currency virtual banking account with Visa card issuance. Built for end-to-end demo and stakeholder walk-throughs.

## What's inside

- **15 screens** — welcome → account type → citizenship → (optional) residence → personal/business info → account preview → KYC overview → ID upload → selfie liveness → proof of address → review → processing → approved → card application → card issued
- **Real camera** for the selfie liveness step (uses `getUserMedia`)
- **Branching flow** — separate paths for Personal vs Business, separate paths for "passport country = residence" vs "different country"
- **PWA installable** — Add to Home Screen on iOS, install prompt on Android/desktop Chrome/Edge
- **Offline-capable** — service worker caches the app shell so it loads even without a connection (after first visit)
- **Dev bar** in the top-right (gold dot) — jump to any screen or reset state

## Local development

```bash
npm install
npm start
```

Camera and service worker work on `localhost` without HTTPS.

> **Why a server and not just opening the file?** Browsers block `getUserMedia` and service workers on `file://` URLs. You need `localhost` or `https://`.

## File structure

```
fynco-onboarding/
├── index.html              # The whole app — UI, logic, styling
├── manifest.webmanifest    # PWA manifest (name, icons, colors)
├── sw.js                   # Service worker (offline caching)
├── icon-192.png            # PWA icon
├── icon-512.png            # PWA icon (large)
├── icon-maskable-512.png   # Android adaptive icon
├── apple-touch-icon.png    # iOS home screen icon
├── favicon.png             # Browser tab favicon
├── package.json            # Node deps + start script
└── README.md
```

## Deploy to Railway

### Via GitHub (recommended)

1. Push this folder to a GitHub repo
2. On [railway.com](https://railway.com): **New Project** → **Deploy from GitHub repo**
3. Pick your repo — Railway auto-detects Node and runs `npm start`
4. Once green: **Settings** → **Networking** → **Generate Domain**
5. Visit the `*.up.railway.app` URL — HTTPS is automatic, camera + PWA install will work

### Via Railway CLI

```bash
npm i -g @railway/cli
railway login
railway init
railway up
railway domain
```

## Installing as a PWA

**On iOS (Safari)** — Tap the Share button, scroll down, tap *Add to Home Screen*. The app will launch full-screen with no browser chrome.

**On Android (Chrome)** — A native install prompt usually appears, or use Chrome's menu → *Install app*. The welcome screen also shows an in-app install button when supported.

**On desktop (Chrome/Edge)** — Look for the install icon in the address bar, or use the in-app install button on the welcome screen.

## Configuration notes

- The `start` script binds to `0.0.0.0:$PORT` — required for Railway's proxy to reach the container.
- `package-lock.json` is gitignored so Railway generates its own on first build.
- No environment variables needed — the app is fully client-side.
- Service worker cache version is the `CACHE` constant in `sw.js`. Bump it after content changes to force clients to refresh.

## Tech

Pure HTML/CSS/JS in a single file. No build step. No framework. Loads Google Fonts (Fraunces, Inter, JetBrains Mono) over the network. The only runtime dependency is `serve` for static hosting.
