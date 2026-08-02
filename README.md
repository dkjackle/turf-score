# Turf Score

A handy overs-and-score tracker for turf cricket — used purely as a web
link, no install needed. Share the link to score a match; share it (with a
watch code) for others to follow live from another phone.

## Live link
Once Pages is enabled for this repo (Settings → Pages → Deploy from branch → `main` → `/ (root)`):

`https://<your-username>.github.io/<repo-name>/`

## Features
- Overs/balls/runs/wickets tracking with an over-by-over dot view
- Optional batsman/bowler name tracking, with strike rotation and bowling figures
- Optional pre-added squad lists so mid-match batsman/bowler picks are a dropdown, not retyping
- Match history saved on the scoring device
- Optional live share: a 6-character code others can use to watch from another phone in real time
- Man of the Match / top scorer / best bowling figures shown at match end
- Fall of wickets and current partnership
- Share the result or the live-watch link on WhatsApp

## Setting up "Share live score" (one-time, ~5 minutes)

Watching a live match from a second phone needs a real shared database on
the internet — a webpage alone can't sync between two separate devices.
This app uses a free Firebase Realtime Database for that:

1. Go to https://console.firebase.google.com and sign in with any Google account.
2. **Add project** → give it any name → you can skip Google Analytics → **Create project**.
3. In the left sidebar: **Build → Realtime Database → Create Database**.
4. Pick any location, then choose **Start in test mode** → **Enable**.
   (Test mode allows open read/write for 30 days — fine for personal use.
   You can tighten the rules to `/live` only later if you want.)
5. Copy the **database URL** shown at the top of that page.
6. Open `index.html` in this repo, find this line near the top of the `<script>`:
   ```js
   var FIREBASE_DB_URL = 'https://YOUR-PROJECT-default-rtdb.firebaseio.com';
   ```
   Replace it with your real URL, save, then:
   ```bash
   git add index.html
   git commit -m "Configure live share"
   git push
   ```
7. GitHub Pages redeploys automatically in about a minute.

Test mode rules expire after 30 days — Firebase will email you a reminder.
When that happens, go to **Realtime Database → Rules** and extend or set:
```json
{ "rules": { "live": { ".read": true, ".write": true } } }
```

## Files
- `index.html` — the app
- `manifest.json` — app name, icon, colors (kept for a nice icon/theme if opened as a tab; not required)
- `icons/` — app icon at required sizes
