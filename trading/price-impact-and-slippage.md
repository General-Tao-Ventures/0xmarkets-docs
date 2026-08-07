# Price impact & slippage

Two things can make your fill price differ from the price you saw on screen: **price impact** (caused by your own size) and **slippage** (caused by the market moving between submission and execution). 0xMarkets gives you control over both.

## Price impact

0xMarkets prices trades against the balance of long and short open interest in a market, not an order book. Your trade's effect on that balance determines its price impact:

- A trade that **worsens** the imbalance (adds to the heavier side) pays **negative price impact** — a slightly worse fill.
- A trade that **improves** the imbalance (takes the lighter side) earns **positive price impact** — a slightly better fill.

The effect grows with size: a small trade barely moves the price, a large trade moves it more. Price impact is **capped** so it can never exceed a set maximum (±0.5% at launch), bounding the worst case on any single trade.

This is the same balancing mechanism behind the two-tier [trading fee](fees.md) and the [funding fee](funding-and-borrowing.md): the system consistently rewards trades that bring a market toward balance and charges those that push it away.

**To minimize price impact on large size,** use a [TWAP order](order-types.md) to split the trade into smaller pieces over time.

## Slippage and your acceptable price

Because 0xMarkets uses [two-step execution](pricing-and-oracle.md) — you submit, a keeper executes against a fresh oracle price moments later — the market can move between those two steps. **Slippage** is that difference.

You control it with an **acceptable price**: the worst price you're willing to accept.

- If the execution price is within your tolerance, the order fills.
- If the market has moved past your acceptable price, the order is **not filled** — it's cancelled (or left resting, for trigger orders) and your collateral is untouched.

This is a hard guarantee enforced at settlement: **you will never be filled at a price worse than your acceptable price.** Set it tighter for more protection (and a higher chance of missing the fill in fast markets), or looser to prioritize getting filled.

## Spread

The oracle provides a separate buy-side and sell-side price (a bid and an ask). You open longs at the higher price and close at the lower, and vice versa for shorts — the gap between them is the **spread**, a normal cost of trading that's already reflected in your quoted entry and exit prices.

## Putting it together

Your effective fill =

```
oracle price  ±  price impact (your size's effect on balance)
              ±  spread
```

…and that fill is only accepted if it's within your **acceptable price**. Everything is shown to you before you confirm.

## Next

- [Pricing & the oracle](pricing-and-oracle.md)
- [Order types](order-types.md) — including TWAP
- [Fees](fees.md)
