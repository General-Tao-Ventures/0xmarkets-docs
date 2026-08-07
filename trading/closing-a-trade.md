# Closing a trade

You can close a position at any time, in full or in part. This page covers how a close is executed and how your PnL settles.

## Ways to close

- **Market close** — close now at the current market price. The most common way to exit.
- **Take-profit / stop-loss** — close automatically when a trigger price is reached. Set these in advance (see [Managing positions](managing-positions.md)).
- **Partial close** — close a portion of your size and realize that share of the PnL, leaving the rest open.

A close is executed the same way as an open: you submit it, and a keeper executes it against a freshly signed oracle price. You can set an **acceptable price** to protect against slippage on the exit.

## How your PnL settles

When you close, your profit or loss is calculated and paid in **USDC** into your collateral, then your remaining collateral is returned to your wallet:

```
Final payout = collateral
             + realized PnL
             − closing fee
             − accrued borrowing fee
             ± accrued funding
```

- **Realized PnL** is the price difference between your entry and exit, times your position size. See [PnL & profit settlement](pnl-and-settlement.md) for the exact formula.
- **Closing fee** is charged on the size you close. See [Fees](fees.md).
- **Borrowing and funding** are netted out for the time you held the position. See [Funding & borrowing](funding-and-borrowing.md).

If the position is profitable, you receive your collateral plus profit minus fees. If it's at a loss, you receive your collateral minus the loss and fees. You can never lose more than your collateral — if losses reach that point, the position is liquidated first (see [Liquidations](liquidations.md)).

## Price impact on close

Closing a large position can move the price against you, just as opening one does — this is [price impact](price-impact-and-slippage.md). Closing a position that *rebalances* the market (for example, closing a long when the book is long-heavy) can instead earn you a small price improvement.

## Next

- [PnL & profit settlement](pnl-and-settlement.md)
- [Fees](fees.md)
- [Price impact & slippage](price-impact-and-slippage.md)
