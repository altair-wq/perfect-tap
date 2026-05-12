# Perfect Tap

A 2-day mobile game build. Ships to iOS and Android. Built to learn the full shipping pipeline, not to make money.

## Quick start

```bash
# Open the prototype directly
open src/index.html

# Or serve it locally so you can test on your phone:
cd src && python3 -m http.server 8000
# Then on your phone (same WiFi): http://YOUR_COMPUTER_IP:8000
```

## Day-by-day

- **Pre-day-0**: Admin (PM does this — see `docs/pm-workstream.md`)
- **Day 1**: Build the game, get it running natively on a real phone (`docs/PLAN.md`)
- **Day 2**: Integrate ads, produce store assets, submit to both stores
- **Day 3+**: Wait for review, fix any rejections

## Files

```
perfect-tap/
├── CLAUDE.md                # Context for Claude Code sessions
├── README.md                # This file
├── src/
│   └── index.html           # Entire game in one file
└── docs/
    ├── PLAN.md              # Hour-by-hour 2-day build plan
    ├── pm-workstream.md     # What your PM does in parallel
    ├── store-listing.md     # Copy + ASO templates
    └── v2-ideas.md          # Parking lot for everything that's NOT in v1
```

## Tech stack
- HTML5 + Canvas, vanilla JS, no build step
- Capacitor 6 for native iOS + Android wrapping
- AdMob for ads (v1), AppLovin MAX as future upgrade
- localStorage for state, no backend

## Principles
1. Ship velocity > feature count. v1 ships in 2 days or we learn what blocked us.
2. Every "wouldn't it be cool" goes to `v2-ideas.md`, not the code.
3. The mechanic is done. Spend all the polish budget on *feel*.
4. PM owns the cut list. Dev owns the code. No scope creep.
5. The game is the excuse to learn the pipeline. The pipeline is the actual product.
