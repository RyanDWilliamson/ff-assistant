# ff-assistant

A personal, self-hosted assistant for my Yahoo Fantasy Football league.

It reads my league data through the Yahoo Fantasy Sports API and surfaces it
conversationally — weekly matchup summaries, roster and injury status, standings,
and free-agent availability — so I can check on my team without opening the app.

## Status

Early. Pending Yahoo Fantasy Sports API access approval.

## Scope

- **Read-only.** The Yahoo Fantasy Sports API provides read access only; this
  project makes no write requests and performs no roster transactions.
- **Single user.** Runs locally against my own Yahoo account, authorized via
  OAuth 2.0. There is no hosted deployment, no account system, and no third-party
  access.
- **Single league.** Personal use for one NFL league.

## Data used

| Resource | Purpose |
| --- | --- |
| `users;use_login=1/games;game_keys=nfl/leagues` | Identify my leagues |
| `league/{league_key}/settings` | Scoring and roster rules |
| `league/{league_key}/standings` | League standings |
| `league/{league_key}/scoreboard` | Weekly matchups and scores |
| `team/{team_key}/roster` | Roster, starters, player status |
| `league/{league_key}/players;status=FA` | Free agents for waiver decisions |
| `league/{league_key}/transactions` | Adds, drops, and trades |

Responses are cached locally. Request volume is a few calls per day, concentrated
around game days. No bulk collection, no crawling, and no redistribution of Yahoo
data.

## Auth

OAuth 2.0 authorization code flow against
`https://fantasysports.yahooapis.com/fantasy/v2`. Client credentials and tokens
are held in a local secret store and are never committed to this repository.

## License

Personal project. Not affiliated with, endorsed by, or sponsored by Yahoo.
