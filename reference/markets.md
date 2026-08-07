# Markets

0xMarkets is launching its **Beta** with **nine markets** across three asset classes — FX, commodities, and crypto. This is the starting line-up: **the market list grows as liquidity deepens, with new markets and asset classes listed over time.** Every market is **USD-quoted** and **collateralized in USDC** on Base. You trade them all the same way — long or short, with leverage, from your own wallet.

## FX

| Market | Underlying | Quote | Headline max leverage |
|---|---|---|---|
| **EUR/USD** | Euro | USD | up to 500x |
| **GBP/USD** | British pound | USD | up to 500x |
| **USD/JPY** | Japanese yen | USD | up to 500x |

## Commodities

| Market | Underlying | Quote | Headline max leverage |
|---|---|---|---|
| **XAU/USD** | Gold | USD | up to 200x |
| **XAG/USD** | Silver | USD | up to 200x |
| **WTI/USD** | Crude oil (WTI) | USD | up to 200x |

## Crypto

| Market | Underlying | Quote | Headline max leverage |
|---|---|---|---|
| **BTC/USD** | Bitcoin | USD | up to 100x |
| **ETH/USD** | Ethereum | USD | up to 100x |
| **TAO/USD** | Bittensor (TAO) | USD | up to 100x |

## About the leverage numbers

The figures above are **ceilings**, not the leverage you'll get on any given trade. The actual maximum available to you depends on the size of your position: 0xMarkets uses a **leverage ladder** where the cap steps down as your position notional grows. A small position can use the highest leverage; a large one is capped lower.

See [Leverage & margin](../trading/leverage-and-margin.md) for the full ladder per asset class and how maintenance margin works.

## Market hours

- **Crypto** (BTC, ETH, TAO) trades **24/7**.
- **FX** (EUR, GBP, JPY) trades the global FX week — roughly Sunday 5:00 PM ET to Friday 5:00 PM ET.
- **Commodities** (gold, silver, oil) trade the global metals and energy session — roughly Sunday 6:00 PM ET to Friday 5:00 PM ET, with a daily 60-minute break from 5:00 PM to 6:00 PM ET.

Availability follows the oracle: when an underlying market is closed, its price stops updating and new orders on it won't execute until the session resumes. Full schedules in [Market hours](../trading/market-hours.md).

> **Beta note.** Each market's open-interest limit is set conservatively at launch and raised over time as liquidity grows.

## Next

- [Leverage & margin](../trading/leverage-and-margin.md)
- [Fee schedule](fee-schedule.md)
- [Market hours](../trading/market-hours.md)
