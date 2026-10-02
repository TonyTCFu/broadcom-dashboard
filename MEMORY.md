# MEMORY.md

Broadcom Inc. (NASDAQ: AVGO) tracking dashboard. Static single page served by
GitHub Pages. This repo is independent of `spacex-dashboard`, `tempus-dashboard`,
`nvda-dashboard`, `micron-dashboard`, and `lam-research-dashboard`; keep them
separate (own quote.json, own workflow, own public link).

## Deployment
- Public link: https://tonytcfu.github.io/broadcom-dashboard/
- Source: `index.html` at the `main` branch root, generated from the
  `avgo-dashboard` web artifact (re-export on data updates; do not hand-edit).
- GitHub Pages setting: Deploy from a branch / main / /(root).

## Quote snapshot
- `quote.json` at repo root; refreshed by `.github/workflows/quote.yml`
  (cron `*/15 13-21 * * 1-5` UTC, Mon-Fri, plus manual dispatch).
- Source: Nasdaq official API (`api.nasdaq.com/api/quote/AVGO/info`), real-time.
- Page fallback chain: quote.json -> Nasdaq direct -> Yahoo Finance -> Stooq (avgo.us).
- Format: {"symbol":"AVGO","price":..,"netChange":..,"pctChange":..,"prevClose":..,
  "quoteTime":"YYYY-MM-DD HH:MM","status":"intraday|postmarket|close","source":"Nasdaq"}.
- The workflow uses `zoneinfo.ZoneInfo("America/New_York")` for the ET wall
  clock (correct across EDT/EST transitions). Cron 13-21 UTC covers
  09:30-17:00 ET in EDT and 08:00-16:00 ET in EST.

## Icon
- broadcom.com official favicon-96x96.png (1,907 bytes, 96x96, verified real
  PNG) embedded as data URI. broadcom.com/favicon.ico does not exist (404);
  never use it.

## Data baseline
- Price/financials/short/analyst snapshot: 2026-10-01 close ($343.64, -2.15%).
- FQ3 2026 (reported 2026-09-03): revenue $29.59B (+86% YoY), non-GAAP EPS
  $3.32, GAAP EPS $2.68; AI semiconductor revenue $16.7B (+221%, 56% of sales);
  Semiconductor $20.84B / Infrastructure Software (VMware) $8.75B; FCF $13.7B;
  FQ4 guide $34.8B (slightly below consensus, trigger for the post-earnings drop).
- Short interest (FINRA 2026-09-15): 51,922,175 shares, 1.11% of float,
  1.7 days to cover (up from 50,451,889 prior).
- Analyst consensus (stockanalysis, 50 firms): Strong Buy, avg target $531.85,
  median $535; 10-firm named ladder on page (Cantor $600 top, Goldman $435).
- Options (2026-10-01, OptiView only; FlashAlpha has no AVGO data):
  dealer GEX negative (-$15.62B, negative-gamma / trend-amplifying regime),
  call wall $400, put wall $300, max pain $355, P/C OI 1.00,
  30d ATM IV 30.3% (rank 45/100). No Gamma Flip value is displayed.
- FQ4 2026 earnings date unconfirmed: estimates 12/09, 12/10, 12/17 differ by
  source; next dividend declaration date unknown. Marked as pending.
