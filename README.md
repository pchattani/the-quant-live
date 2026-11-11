# The Quant Sports: live scores feed

Serves one small file, `https://pchattani.github.io/the-quant-live/live.json`: the score, period, clock and status of
the games on today's boards (NBA, WNBA, NFL, NHL, MLB, college football, basketball and hockey, rugby union tests).
[The Quant Sports](https://pchattani.github.io/the-quant-sports/) and its sport pages read it every few seconds
while games are on, so a score is the same on every page and does not wait for an hourly site build.

- `live_feed.py` reads the scoreboards (ESPN's site API, the NHL's web API, the MLB Stats API) with an identified
  User-Agent, each board only as often as it needs: every 30 seconds with a game on, every 30 minutes with nothing
  near.
- `.github/workflows/live.yml` runs it in a loop and deploys the file to GitHub Pages when something changed.
- Live win chances come from the sites' own live models: the loop also checks out the public build repo
  ([pchattani/quant-sports](https://github.com/pchattani/quant-sports)) and runs its `scripts/live_chances.py` on the
  games in progress (the Hardwood's NBA and WNBA model first), with the model numbers the site's last build
  published.
- `.github/workflows/watchdog.yml` restarts the loop if it stops.

The files here are copies: the source is the private engine repository (`scripts/live_feed.py`, `live_repo/`).
Scores belong to their leagues and sources; this feed is non-commercial and credited on the sites' terms pages.
