# Oracle security

Because every trade on 0xMarkets is priced against an oracle rather than an order book, the integrity of that price feed is the most important security property of the exchange. This page explains how prices are kept honest — what stops a bad price from reaching your trade, and what stops anyone from front-running you. For how pricing works in normal trading, see [Pricing & the oracle](../trading/pricing-and-oracle.md).

> **0xMarkets launches in Beta.** The oracle setup described here reflects the Beta launch and will expand shortly after, as the secondary feed and final hardening are switched on.

## Signed prices, verified on-chain

At Beta launch, prices come from **Pyth Pro**, a low-latency oracle that streams cryptographically **signed** prices for every market 0xMarkets lists.

- Each price is signed at the source.
- The exchange verifies that signature on-chain before it will use the price.
- A price without a valid signature is rejected. Trades cannot execute on an unsigned or tampered price.

This means the price your trade fills at isn't something the front-end or a keeper can simply assert — it has to be a genuine, signed reading the contracts can verify.

## Dual-oracle design

0xMarkets is built around a **dual-oracle design** for resilience. Pyth Pro is the primary feed at launch, and support for a **secondary oracle — Chainlink Data Streams — is already built into the contracts.** The secondary feed will be enabled **shortly after Beta launch.**

Running two independent low-latency feeds lets the exchange cross-check prices and keep operating if one source degrades, reducing reliance on any single provider. Until the secondary feed is switched on, the on-chain guards below apply to the primary Pyth Pro feed.

## On-chain price guards

Before the exchange will accept an oracle price, the contracts enforce several checks so a trade can't execute on bad data:

- **Signature verification** — only prices carrying a valid oracle signature are accepted.
- **Staleness check** — a price older than the maximum allowed age (a few minutes) is rejected. If the oracle stops updating — for example when an underlying FX or commodity market closes for the weekend — trades that need a fresh price simply won't execute. See [Market hours](../trading/market-hours.md).
- **Deviation check** — a price that deviates too far from a reference is rejected, guarding against a single bad print moving your fill.
- **Request expiration** — a submitted order that isn't executed with a fresh signed price within about **5 minutes** expires instead of filling on a stale one.

## Two-step execution as front-running protection

0xMarkets prices every trade with a **two-step model**, and that design is itself a security feature:

1. **You submit** an order from your wallet. Your collateral is escrowed. No price is attached yet.
2. **A keeper executes** it in a second transaction, attaching a freshly signed oracle price.

Because the price is only attached at execution and must be freshly signed, no one can see your pending order and jump ahead of it at a stale price. Your [acceptable price](../trading/pricing-and-oracle.md) protects you from any adverse move between submit and execution, and an order that can't be executed in time expires rather than filling on a bad price.

## What this protects you from

- **Fake or tampered prices** — rejected by signature verification.
- **Stale prices** — rejected by the staleness check and request expiration.
- **A single manipulated print** — caught by the deviation check.
- **Front-running on submission** — prevented by attaching the signed price only at execution.

These guards harden further over time as the dual-oracle setup is completed and tuned during Beta.

## Next

- [Pricing & the oracle](../trading/pricing-and-oracle.md)
- [Insurance fund](insurance-fund.md)
- [Risk disclosures](risk-disclosures.md)
