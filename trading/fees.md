# Fees

Trading on 0xMarkets has two kinds of cost: a **trading fee** when you open and close, and ongoing **funding and borrowing** while a position is open. (You also pay normal network gas for your own transactions — but not the keeper's execution gas, which the protocol covers.) This page covers the trading fee. Funding and borrowing have their [own page](funding-and-borrowing.md).

## Trading fee (open and close)

A trading fee is charged on your **position size**, both when you open and when you close. The rate depends on the asset class — and on whether your trade improves or worsens the balance of the market.

| Asset class | Fee (balancing trade) | Fee (imbalancing trade) |
|---|---|---|
| **FX** | 0.015% | 0.025% |
| **Crypto** | 0.030% | 0.040% |
| **Commodities** | 0.020% | 0.030% |

**Why two rates?** Every market has long and short open interest. A trade that pushes the market further out of balance (e.g. adding to the already-heavier side) pays the higher rate; a trade that brings it *back* toward balance pays the lower rate. This nudges the book toward equilibrium and rewards traders who take the underweighted side. It's the same mechanism behind [price impact](price-impact-and-slippage.md).

## How it's applied

- **On open:** the fee is calculated on your opening position size and deducted from your collateral.
- **On close:** the fee is calculated on the size you're closing and netted out of your payout.

For a $20,000 crypto position opened and later closed, a balancing trade would pay roughly `$20,000 × 0.030% = $6` on each side — about $12 round-trip, before funding and borrowing.

## Network gas

You pay normal **network gas** (in ETH on Base) for the transactions you sign — submitting or cancelling an order. You do **not** pay the keepers that execute your trades: their execution gas is subsidised by the protocol. There is no separate keeper or execution fee charged to you.

## Where trading fees go

Each trading fee is distributed across the protocol:

| Destination | Share | What it does |
|---|---|---|
| **LP pool** | 50% | Rewards the liquidity providers who back the market you trade |
| **veAlpha rewards pool** | 40% | Rewards Alpha holders who lock for veAlpha |
| **Treasury** | 10% | Funds protocol operations and growth |
| **Alpha buyback** | 0% | Reserved; directs value to the Alpha token when enabled |

*These are the launch values. The trading-fee distribution is controlled by veAlpha governance and can be adjusted by governance decisions.*

> Liquidation fees are distributed separately (70% insurance pool / 30% Alpha buyback). See [Liquidations](liquidations.md).

## Referral discounts

A referral program for introducing brokers and affiliates is **coming soon** — it will let referred traders' fees be shared with their referrer. See [Referrals](../referrals.md).

## Next

- [Funding & borrowing](funding-and-borrowing.md)
- [Price impact & slippage](price-impact-and-slippage.md)
- [Fee schedule](../reference/fee-schedule.md) — all rates in one table
