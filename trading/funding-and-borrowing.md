# Funding & borrowing

While a position is open, it accrues two ongoing costs: a **funding fee** and a **borrowing fee**. Both accrue continuously (per second) and are settled when you close, partially close, or get liquidated. They're shown live on your open position so you always know what you've accrued.

## Funding fee

Funding balances the two sides of a market. At any time, one side (longs or shorts) has more open interest than the other. **The heavier side pays the lighter side.**

- If longs outweigh shorts, longs pay funding and shorts receive it.
- If shorts outweigh longs, shorts pay and longs receive.

So funding can be a **cost or a credit**, depending on which side you're on and how the market is balanced. If you're on the lighter side, you may get paid to hold your position.

**How the rate behaves:** funding is *adaptive*. The more imbalanced the market, the faster the funding rate climbs toward its cap; as the market rebalances, the rate decays back down (over roughly 48 hours). The rate is capped per market — at launch, between **75% and 100% per year** depending on the market — which works out to a maximum of roughly **0.2–0.27% per day** in the most extreme, sustained imbalance. In normal conditions it is far lower.

This is the economic force that keeps the perpetual price tracking the underlying market: it makes the crowded side progressively more expensive to hold.

## Borrowing fee

The borrowing fee is a charge for the liquidity your position uses from the pool. Unlike funding, it's always a **cost** (never a credit), and it's paid by the side that's actually drawing on liquidity.

- It accrues continuously based on your position size and how long you hold it.
- The **lighter side of the market pays no borrowing fee** — only the side using up the pool's capacity pays. This further rewards taking the underweighted side of a market.

## How both are settled

Neither fee is charged up front. They accumulate while your position is open and are netted into your PnL when you close:

```
final payout = collateral + realized PnL − closing fee − accrued borrowing ± accrued funding
```

Your live position shows **accrued borrowing fee** and **accrued funding** at all times, so your displayed unrealized PnL already reflects them.

## Practical implications

- **Short-term trades** pay very little funding or borrowing — these costs matter most for positions held for days.
- **Holding the crowded side** of a market in a strong trend can get expensive; funding is designed to make it so.
- **Taking the underweighted side** can mean reduced or zero borrowing fees and possibly *receiving* funding — a real edge for patient traders.

## Next

- [Fees](fees.md) — the open/close trading fee
- [Price impact & slippage](price-impact-and-slippage.md)
- [PnL & profit settlement](pnl-and-settlement.md)
