# Order types

0xMarkets supports five order types. They fall into two groups: **market orders**, which execute immediately, and **trigger orders**, which wait for a price condition before executing.

| Order type | Group | What it does |
|---|---|---|
| **Market** | Immediate | Opens or closes now at the current price |
| **Limit** | Trigger | Opens when the price reaches a level you set |
| **Stop Market** | Trigger | Opens when the price crosses a level you set (breakout entry) |
| **TP / SL** | Trigger | Closes an open position at a profit (TP) or loss (SL) target |
| **TWAP** | Scheduled | Splits a large order into smaller pieces over time |

## Market

Executes as soon as a keeper can fill it, using a freshly signed oracle price. You set an **acceptable price** so the order won't fill if the market has moved past your tolerance. A market order that can't be filled within **5 minutes** expires.

Use it when you want in or out *now*.

## Limit

Opens a position when the market reaches a price you specify — typically a price *better* than the current one (buy lower, sell higher). The order rests until the trigger price is met, then a keeper executes it.

Use it to enter at a target price without watching the market.

## Stop Market

Opens a position when the market *crosses* a price you specify — typically used for breakout entries (e.g. go long only if price breaks above resistance). Unlike a limit, a stop entry triggers in the direction of momentum.

## Take-profit / Stop-loss (TP / SL)

These are exit triggers attached to an open position:

- **Take-profit** closes the position when price reaches your profit target.
- **Stop-loss** closes the position when price reaches your loss limit.

You can set one or both. They're the core tool for managing a position you're not actively watching. See [Managing positions](managing-positions.md).

> A trigger fires when the condition is met, but the fill price is the oracle price at execution. In fast or [gapping markets](market-hours.md), the fill can differ from the trigger level.

## TWAP

A **Time-Weighted Average Price** order breaks a large order into a series of smaller orders executed over a period of time. This reduces the [price impact](price-impact-and-slippage.md) of entering or exiting a large position all at once, at the cost of taking longer to fill and accepting whatever average price the market gives over that window.

Use it for large size where minimizing market impact matters more than immediate execution.

## What's not supported

There is no native **trailing stop** order. To trail a position, adjust your stop-loss manually as the trade moves in your favor.

## Next

- [Opening a trade](opening-a-trade.md)
- [Price impact & slippage](price-impact-and-slippage.md)
- [Pricing & the oracle](pricing-and-oracle.md)
