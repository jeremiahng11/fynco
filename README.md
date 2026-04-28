# Fynco — Onboarding Simulation

A single-file HTML5 PWA-friendly onboarding flow for a multi-currency virtual banking account with Visa card issuance. Built for end-to-end demo and stakeholder walk-throughs.

## What's inside

- **15 screens** — welcome → account type → citizenship → (optional) residence → personal/business info → account preview → KYC overview → ID upload → selfie liveness → proof of address → review → processing → approved → card application → card issued
- **Real camera** for the selfie liveness step (uses `getUserMedia`)
- **Branching flow** — separate paths for Personal vs Business, separate paths for "passport country = residence" vs "different country"
- **Dev bar** in the top-right (gold dot) — jump to any screen or reset state

## Local development

```bash
npm install
npm start
```

Opens on `http://localhost:3000` (or the next free port). Camera works on `localhost` without HTTPS.

> **Why a server and not just opening the file?** Browsers block `getUserMedia` on `file://` URLs. You need `localhost` or `https://`.

## Deploy to Railway

### Via GitHub (recommended)

1. Push this folder to a GitHub repo
2. On [railway.com](https://railway.com): **New Project** → **Deploy from GitHub repo**
3. Pick your repo — Railway auto-detects Node and runs `npm start`
4. Once green: **Settings** → **Networking** → **Generate Domain**
5. Visit the `*.up.railway.app` URL — HTTPS is automatic, camera will work

### Via Railway CLI

```bash
npm i -g @railway/cli
railway login
railway init
railway up
railway domain
```

## Configuration notes

- The `start` script uses `$PORT` — Railway injects this at runtime. Don't hardcode a port.
- `package-lock.json` is gitignored so Railway generates its own on first build.
- No environment variables needed — the app is fully client-side.

## Tech

Pure HTML/CSS/JS in a single file. No build step. No framework. Loads Google Fonts (Fraunces, Inter, JetBrains Mono) over the network. The only runtime dependency is `serve` for static hosting.
