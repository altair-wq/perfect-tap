# Perfect Tap — 2-Day Build Plan

Realistic schedule. Times include the "wait, why doesn't this work" tax.
Each block has a clear deliverable. If you fall behind, cut from the END, not the start.

---

## PRE-DAY-0 (Your PM does this RIGHT NOW, in parallel)

These have lead time. Start them before you write any code.

- [ ] **Apple Developer Program** ($99/yr). Sign up at developer.apple.com.
      Approval: 24–48 hrs, sometimes 7 days. THIS IS THE CRITICAL PATH.
- [ ] **Google Play Console** ($25 one-time). Sign up at play.google.com/console.
      Usually instant, but requires identity verification (1–2 days).
- [ ] **AppLovin account** (free) at applovin.com. Approve takes ~1 day.
- [ ] **Buy a domain** for the privacy policy URL. Anything cheap.
      Privacy policy can be auto-generated at termly.io or app-privacy-policy-generator.firebaseapp.com.
- [ ] **Pick the app name** and check availability on both stores.
      "Perfect Tap" is taken. Suggestions: "Tap Zone", "Zone Tap", "Bar Tap Bar",
      "Perfect Stop", "Tap True", "Zonely". Brainstorm 10, pick one.
- [ ] **Buy a Mac or rent one** — required to submit to Apple. MacInCloud.com is
      ~$30/mo if you don't have one. No way around this.

---

## DAY 1 — Build the Game (8–10 hours)

### Block 1: Setup (1 hr)
- [ ] Install Node.js LTS if not installed
- [ ] `npm init -y` in the project folder
- [ ] `npm install @capacitor/core @capacitor/cli @capacitor/ios @capacitor/android`
- [ ] `npx cap init "YourGameName" "com.yourcompany.yourgame" --web-dir=src`
- [ ] Open `src/index.html` in browser. Verify the prototype works on desktop.
- [ ] Open it on your phone via local network (`python -m http.server 8000` in src/, then visit YOUR_IP:8000 from phone). Verify it feels good on mobile.

### Block 2: Polish the core loop (3 hrs)
The prototype is already playable. Spend this block making it FEEL right.
- [ ] Play it 50 times. Note every moment that feels off.
- [ ] Tune `CFG` values. Most likely: `startSpeed`, `speedRamp`, `zoneWidth`.
- [ ] Add a SOUND TOGGLE button on menu (top-right corner).
- [ ] Add a VIBRATE TOGGLE button next to it.
- [ ] Improve the "MISS" moment — bigger shake, longer flash, slower fade-out before game over screen. The miss must feel BAD.
- [ ] Improve the "PERFECT" moment — bigger particle burst, satisfying double-beep, screen tint.

### Block 3: Settings & state (1 hr)
- [ ] Save sound/vibrate preferences in localStorage
- [ ] Save high score (already done in prototype, verify it persists across refresh)
- [ ] Add a small "settings" gear icon on the menu
- [ ] Reset-high-score button in settings (with confirm)

### Block 4: Mobile feel & edge cases (2 hrs)
- [ ] Test on iPhone (Safari) — make sure audio works after first tap (it should)
- [ ] Test on Android Chrome — make sure vibration works
- [ ] Test rotating the phone — does the game break? Lock to portrait in Capacitor config.
- [ ] Test with a SIM cut to airplane mode — does anything break? (shouldn't, no network calls)
- [ ] Test backgrounding the app mid-game — pause when hidden? Add `document.visibilitychange` handler.
- [ ] Test with system font scaling at max — does UI break? Use `rem` or fixed `px`.
- [ ] Add an app icon design. Use Figma or buy one on icons8/Iconscout for $5.

### Block 5: First Capacitor build (1–2 hrs)
- [ ] `npx cap add ios`
- [ ] `npx cap add android`
- [ ] `npx cap sync`
- [ ] `npx cap open android` — run on a real Android phone via USB. Verify it works.
- [ ] `npx cap open ios` — run on iPhone via Xcode (need that Mac). Verify it works.

END OF DAY 1: game runs as a native app on at least one real phone.

---

## DAY 2 — Ship It (8–10 hours)

### Block 6: Ads integration (2–3 hrs) — the part that will frustrate you
Use the Capacitor Community AdMob plugin first (simpler than MAX for v1).
You can switch to AppLovin MAX later for better revenue.

- [ ] `npm install @capacitor-community/admob`
- [ ] Sign in to admob.google.com, create app + ad units (banner, interstitial, rewarded)
- [ ] Add ad unit IDs to the app
- [ ] Show banner on menu screen
- [ ] Show interstitial every 3rd game over
- [ ] Test with AdMob TEST IDs first, not real ones — your account will get banned if you click your own real ads.

### Block 7: Store assets (2 hrs)
This is the part everyone underestimates.
- [ ] App icon at 1024x1024 (master) + auto-generate all sizes with capacitor-assets or appicon.co
- [ ] Splash screen
- [ ] 5–8 screenshots per platform. Use a real device, take real screenshots.
      iOS sizes: 6.7" (1290x2796) and 6.5" (1284x2778) required minimum.
      Android: ~1080x1920 portrait.
- [ ] Short description (80 chars max for Google Play)
- [ ] Long description (4000 chars)
- [ ] Keywords list (App Store has 100-char keyword field, use it)
- [ ] Privacy policy URL (live on your domain)
- [ ] "What's New" text for first version

See `docs/store-listing.md` for templates.

### Block 8: Final QA (1 hr)
- [ ] Play 20 full games, no crashes
- [ ] All buttons work
- [ ] Sounds toggle works
- [ ] Vibration toggle works
- [ ] Ad shows after 3rd game over
- [ ] No console errors
- [ ] No layout breaks on small phone (iPhone SE) or tall phone (Pixel 8 Pro)

### Block 9: Submit (2–3 hrs)
**Google Play first** — easier and faster review.
- [ ] In Android Studio: Build → Generate Signed Bundle (AAB), save the keystore SOMEWHERE SAFE (lose it = can't update ever again)
- [ ] Play Console → create app → fill in everything → upload AAB to Internal Testing
- [ ] Add yourself + your PM as testers, install via the test link, verify
- [ ] Then promote to Production (or stay in Closed Testing first if you want)

**App Store**:
- [ ] In Xcode: Product → Archive → Distribute App → App Store Connect → Upload
- [ ] In App Store Connect: create app, fill in all metadata, attach the build, answer the privacy questions (lots of them), submit for review
- [ ] Apple will likely reject the first submission for SOMETHING. Read the rejection carefully, fix, resubmit.

END OF DAY 2: Both submissions are filed. Now you wait.

---

## DAY 3+ (Not in the 2-day budget, but real)

- Google Play: 24–48 hrs review typically
- Apple App Store: 24 hrs to 7 days. First submission for new accounts is usually slower.
- When live: tell exactly 5 friends and your Twitter, then move on. Don't refresh installs all day.
- Watch crash reports daily for the first week (Crashlytics or Sentry — add in v1.1).

---

## What if you fall behind?

Cut in this order:
1. AppLovin MAX — keep AdMob only (saves 2 hrs)
2. Android submission — ship iOS only first, Android day 3 (Android is easier, do later)
3. Rewarded ad — keep only banner + interstitial
4. Settings screen — put toggles directly on menu
5. iOS submission — ship Android only first (if you don't have a Mac access)

NEVER cut: app icon, screenshots, privacy policy. Stores reject without these.
