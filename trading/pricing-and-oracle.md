# Pricing & the oracle

0xMarkets is not an order-book exchange. There is no bid/ask book of resting orders matched against each other. Instead, every trade is priced against a **real-time oracle price**, adjusted for your size. This page explains where prices come from and how a trade gets filled.

> **0xMarkets is in Beta.** The exchange is live and fully functional, and we're actively refining it as it matures. The oracle setup described here reflects the Beta launch and expands shortly after.

## Where prices come from

At Beta launch, prices are supplied by **Pyth Pro** — a low-latency oracle service that streams cryptographically signed prices for every market 0xMarkets lists. Each price is signed at the source, so it can be verified on-chain — the exchange only accepts prices that carry a valid signature.

The oracle provides a **signed minimum and maximum price** (a bid and an ask) for each market. Longs open at the higher price and close at the lower; shorts the reverse. That gap is the [spread](price-impact-and-slippage.md).

## Dual-oracle design

0xMarkets is built around a **dual-oracle design** for resilience. Pyth Pro is the primary feed at launch, and support for a **secondary oracle — Chainlink Data Streams — is already built into the contracts.** The secondary feed will be enabled **shortly after Beta launch.**

Running two independent low-latency feeds lets the exchange cross-check prices and keep operating if one source degrades, reducing reliance on any single provider. Until the secondary feed is switched on, the safety guards below apply to the primary Pyth Pro feed.

## Two-step execution

To price every trade fairly and prevent front-running, 0xMarkets uses a **two-step model**:

1. **You submit** an order from your wallet. Your collateral is escrowed.
2. **A keeper executes** it in a second transaction, attaching a freshly signed oracle price.

This means your fill uses the oracle price at *execution* time — typically seconds after you submit — not the price at the instant you clicked. Your [acceptable price](price-impact-and-slippage.md) protects you from any adverse move in that gap, and a market order that can't be executed within **5 minutes** expires.

The benefit of this design: no one can see your order and jump ahead of it at a stale price, because the price is only attached at execution and must be freshly signed.

## How a trade is priced

Your execution price is the oracle price, adjusted for the effect of your trade on market balance:

```
execution price = oracle price ± price impact ± spread
```

See [Price impact & slippage](price-impact-and-slippage.md) for how the adjustment works.

## Price safety guards

The exchange enforces several checks before it accepts an oracle price, so trades can't execute on bad data:

- **Staleness check** — a price older than the maximum age (a few minutes) is rejected. If the oracle stops updating (for example, when an underlying market closes for the weekend), trades that need a fresh price won't execute. See [Market hours](market-hours.md).
- **Deviation check** — a price that deviates too far from a reference is rejected, guarding against a single bad print.
- **Signature verification** — only prices signed by the oracle are accepted.

## Why this matters to you

- Your fill is always anchored to a verifiable, real-time market price — not to whatever happens to be resting in a thin order book.
- You can't be front-run on submission.
- You're protected from stale or manipulated prices by the on-chain guards.
- The trade-off is that fills happen a moment after you submit, which is why the **acceptable price** exists.

## Next

- [Price impact & slippage](price-impact-and-slippage.md)
- [Market hours](market-hours.md)
- [Order types](order-types.md)
