# Perfect Tap — Project Context

## What this is
A hyper-casual timing game shipping to iOS App Store and Google Play.
Built in 2 days as a learning project for end-to-end mobile shipping pipeline.
Core loop: tap to stop a moving indicator inside a "perfect zone."
Speed ramps with every perfect tap. One miss = game over.

## Stack
- HTML5 + Canvas (single-file prototype in `src/index.html`)
- Capacitor 6.x wraps it as a native iOS + Android app
- AppLovin MAX for ad mediation (rewarded + interstitial)
- localStorage for high score (no backend, no accounts)
- No build tooling — raw HTML/JS, edit and refresh

## File map
- `src/index.html` — entire game (HTML, CSS, JS in one file)
- `capacitor.config.json` — native app config (added in Day 2)
- `ios/` and `android/` — generated Capacitor native projects
- `docs/` — store listing copy, screenshots checklist, post-mortem template

## Conventions
- All gameplay tuning lives in the `CFG` object at top of the script. Never hardcode numbers elsewhere.
- Audio uses Web Audio synth, no sound files. Keeps bundle tiny.
- Haptics via `navigator.vibrate` — Android works, iOS Safari ignores it (Capacitor plugin needed for iOS haptics — Day 2 task).
- 60fps target. Profile with Chrome DevTools Performance if it dips.
- Mobile-first. Never test desktop-only. Always preview on real phone via local network or TestFlight.

## What ships in v1 (don't add anything else)
- Core tap loop
- Perfect / Good / Miss feedback
- Combo counter
- Local high score
- Game over → play again
- Interstitial ad every 3rd game over
- Rewarded ad: "Continue with one extra life" on first miss (optional, Day 2)
- Banner ad on menu screen only
- Sound on/off toggle
- Vibration on/off toggle

## Explicitly NOT in v1
- Skins, cosmetics, IAP
- Daily challenges
- Leaderboards (no backend)
- Multiple game modes
- Achievements
- Tutorial beyond the hint text
- Accounts, cloud save

Every "wouldn't it be cool if" idea goes in `docs/v2-ideas.md`, not the code.

## Don't touch
- `ios/App/Pods/` and `android/app/build/` — generated, regenerated on every `npx cap sync`
- `node_modules/` — obvious

## Build commands
- Local dev: `open src/index.html` (or use any static server)
- Sync to native: `npx cap sync`
- Open iOS: `npx cap open ios`
- Open Android: `npx cap open android`

## Tuning notes (changes that took the longest to dial in)
- `CFG.startSpeed`: 0.7 cycles/sec is the sweet spot. Below 0.5 feels too easy. Above 1 feels punishing on level 1.
- `CFG.speedRamp`: 0.05 per perfect. After ~20 perfects you're at 1.7, which is brutal but fair.
- `CFG.zoneWidth`: 0.18 (good) and 0.06 (perfect). Don't go below 0.04 for perfect — finger size becomes the limiter.
- Miss bar should always be ~30% of screen, never tiny — players need to *see* they missed.
