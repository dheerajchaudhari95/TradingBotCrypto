# Trading Bot — Project Root

This repository contains two independent bot versions. Each version is self-contained and independently shareable.

---

## V1 — EmaAtrTrend (Daily Swing Strategy)

**Status:** Extended paper-trading observation (dry-run active)

**Strategy:** EMA20/EMA50 crossover with SMA200 regime filter, ATR-based trailing stop, 1% fixed-fractional risk sizing.

**Validated:** Full backtest 2017–2026 across BTC/USDT and ETH/USDT. 20 trades, profitable net result, known outlier concentration in 2020–2021.

**Folder:** `V1/`

Run from inside `V1/`:
```
cd V1
docker compose run --rm freqtrade trade -v --logfile user_data/logs/freqtrade.log --db-url sqlite:////freqtrade/user_data/tradesv3.dryrun.sqlite --config user_data/config.json --strategy EmaAtrTrend --dry-run
```

---

## V2 — BreakoutV1 (4H Breakout Strategy)

**Status:** Pre-validation / in development

**Strategy:** 4H candle breakout strategy. Not yet backtested or deployed.

**Folder:** `V2/`

---

## Project Rules

> **V2 must never reference a V1 file by path.**
> If V2 needs something from V1 (e.g. a utility script, a data file), it must be **copied into V2 first**. No cross-version imports or path references are permitted.

This rule ensures each folder is independently shareable — you can zip up either `V1/` or `V2/` and hand it to someone else with no dangling dependencies.

---

## Folder Structure

```
Trading Bot/
├── README.md          ← this file
├── V1/                ← fully self-contained, live paper-trading
│   ├── user_data/     ← strategies, data, logs, SQLite DB
│   ├── docs/
│   ├── docker-compose.yml
│   ├── .env           ← credentials (not committed)
│   └── ...
└── V2/                ← in-development breakout strategy
    ├── user_data/
    │   ├── strategies/
    │   ├── data/
    │   └── logs/
    └── docs/
```
