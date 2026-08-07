# PnL & profit settlement

Your profit or loss is the difference between where you entered and where you exited, scaled by your position size. This page explains the exact calculation, how it settles, and the one pool-level rule that can affect very large winning trades.

## How PnL is calculated

For a **long** position:

```
PnL = (exit price − entry price) × position size (in units of the asset)
```

For a **short** position, it's reversed:

```
PnL = (entry price − exit price) × position size
```

Your displayed **unrealized PnL** is what you'd realize if you closed right now, already net of the [funding and borrowing](funding-and-borrowing.md) you've accrued. When you close, it becomes **realized PnL**.

## How it settles

PnL settles in **USDC**, into your collateral. On close you receive:

```
payout = collateral + realized PnL − closing fee − accrued borrowing ± accrued funding
```

- A **winning** trade returns your collateral plus profit, minus fees.
- A **losing** trade returns your collateral minus the loss and fees.
- You can never lose more than your collateral — if a loss would exceed it, the position is [liquidated](liquidations.md) first.

Profits are paid from the liquidity pool backing the market — the [LPs](../getting-started/what-is-0xmarkets.md) on the other side of your trade. When you win, they pay; when you lose, they receive.

## The profit cap (rarely relevant)

There is one pool-level protection worth knowing about, though most traders will never encounter it.

To keep a market solvent, the total *open profit* of all traders on one side of a market is capped relative to the size of the liquidity pool backing it (at launch, **90%** of the pool). This is **not** a cap on your individual trade. It only comes into play in an extreme case — when one side of a market is enormously profitable all at once and that combined profit would otherwise exceed most of the pool. In that situation, open profits on that side are scaled down proportionally until the pool can cover them.

For an ordinary position in a reasonably balanced market, your PnL is paid in full as calculated above. The cap exists so the exchange can always honor winning trades; it's a backstop, not a typical outcome.

> A related mechanism, **auto-deleveraging (ADL)**, can close some of the most profitable positions early if a market gets close to that limit, to keep it solvent. Like the cap, it's an edge-case protection, not part of normal trading.

## Next

- [Closing a trade](closing-a-trade.md)
- [Fees](fees.md)
- [Liquidations](liquidations.md)
