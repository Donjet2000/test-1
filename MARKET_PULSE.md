# Market Pulse — Automated Market Analysis Agent

An automated agent that tracks US equity indices, a large-cap watchlist, and
BTC/ETH, and publishes a daily and weekly analysis report.

## Dashboard

Live report: https://claude.ai/code/artifact/af9ef5e3-823d-483c-a1ad-569cc7201154

The page has two tabs:

- **Daily** — latest index closes (S&P 500, Dow Jones, Nasdaq Composite), BTC/ETH
  prices, a watchlist table, and a short plain-language readout of what moved
  the market that day.
- **Weekly** — a week-over-week recap of the same indices/watchlist, the
  week's standout movers, and a brief look-ahead to the coming week.

## Watchlist

- **Indices**: S&P 500, Dow Jones Industrial Average, Nasdaq Composite
- **Equities**: AAPL, MSFT, AMZN, GOOGL, META, NVDA, TSLA
- **Crypto**: BTC, ETH

## How it updates

Two scheduled Routines (Claude Code Remote triggers) re-research the market
and rewrite the report in place — same URL every time, only the numbers and
narrative change:

| Routine | Schedule (UTC) | What it does |
|---|---|---|
| Market Pulse — Daily Update | `30 21 * * 1-5` (weekdays, ~5:30pm ET) | Refreshes the Daily tab from that day's close |
| Market Pulse — Weekly Wrap | `0 20 * * 0` (Sundays, ~4pm ET) | Refreshes the Weekly tab with the past week's recap |

Each firing spins up a fresh Claude session that:

1. Reads the current published report.
2. Uses web search against public finance sources (Yahoo Finance, CNBC, etc.)
   to get current prices, % changes, and the news driving the move.
3. Rewrites only the relevant tab's numbers, deltas, and narrative.
4. Republishes to the same artifact URL.

No data is fabricated between updates — data source is genuinely re-pulled at
each run, so a stale figure means the next scheduled run hasn't fired yet, not
that it's simulated.

## Notifications

- **Daily Update** — sends a push notification and an email (to the account
  owner's inbox) each time it finishes, with a one-to-two-line takeaway of
  the day's move.
- **Weekly Wrap** — push notification not yet enabled; see below.

## Changing the watchlist or schedule

The Routines are managed via the Claude Code Remote `list_triggers` /
`update_trigger` tools (trigger IDs `trig_01PLjdA24rjMmE8B7zEN66vn` for Daily,
`trig_01SniQA11uDK7QdQ5ZocAH4f` for Weekly). To change the tracked symbols,
update the Routine prompts via `update_trigger`; to change cadence, update the
cron expression the same way. Notification settings can only be set at
creation time, not via `update_trigger` — changing them requires deleting and
recreating the Routine (same cron/prompt, plus a `notifications` field).
