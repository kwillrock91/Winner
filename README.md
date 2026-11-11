# WINNER Live — deployable web app

## Run locally
Install Node.js 20 or newer. From this directory:

```bash
ODDS_API_KEY=YOUR_KEY npm start
```

Visit http://localhost:3000. Without a key, ESPN scoreboards still work; the odds screen explicitly reports unconfigured status.

## Publish publicly
1. Create a GitHub repository with these files (keep .env files and keys out of Git).
2. On Render, create a **Web Service** from the repository; select Node, start command `npm start`.
3. Add secret environment variable `ODDS_API_KEY` in the hosting dashboard.
4. Deploy and share the generated HTTPS URL. Open it in Safari on iPhone and use Share > Add to Home Screen.
5. Confirm your odds subscription supports requested bookmakers, leagues and refresh quota. A free tier may be insufficient for polling several leagues every minute.

## Data & caveats
- `/api/odds?league=NBA` requests American h2h/spreads/totals from DraftKings, FanDuel and BetMGM via The Odds API. Only provider-returned markets are displayed. Player props and sportsbook-quoted same-game parlays require separate eligible endpoints/plans.
- `/api/scores?league=NBA&date=2026-11-11` reads ESPN's public scoreboard endpoint. It is an unofficial feed; availability and usage terms can change.
- Caches: odds 60 seconds per league, scores 30 seconds per league/date. Browser refreshes once per minute. Public traffic may still exhaust odds quotas across leagues; use a longer cache or managed provider for scale.
- Browser-local saved tickets do not sync between devices. A database and authentication are required for private cross-device syncing.
- Parlay odds are calculated by multiplying decimal prices; correlated or same-game combinations may be restricted or repriced by sportsbooks. This tool does not place bets.
