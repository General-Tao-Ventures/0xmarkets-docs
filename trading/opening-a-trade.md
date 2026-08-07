# Opening a trade

Opening a position takes four decisions: **direction, market, size, and leverage.** This page walks through each and explains what happens after you confirm.

## 1. Choose a direction

- **Long** — you profit if the price goes up.
- **Short** — you profit if the price goes down.

Perpetual futures let you go either way on any market. You are not buying the underlying asset; you are taking a leveraged position on its price.

## 2. Choose a market

Pick from any of the listed markets across three asset classes — FX, commodities, and crypto. See the full list and per-market details in [Markets](../reference/markets.md).

## 3. Set your collateral and size

- **Collateral** is the USDC you put up to back the position. It is also the most you can lose on the trade (plus fees).
- **Position size** is your collateral multiplied by your leverage. A $1,000 collateral position at 20x leverage controls a $20,000 position.

Your size determines your exposure: a 1% move in the market changes a $20,000 position by $200 — a 20% swing on $1,000 of collateral.

## 4. Set your leverage

Leverage multiplies both your gains and your losses. 0xMarkets supports high leverage, but the maximum available depends on the asset class **and** your position size — larger positions get lower maximum leverage. See [Leverage & margin](leverage-and-margin.md) for the full ladder.

Higher leverage means a smaller price move will liquidate you. Choose deliberately.

## 5. Review and confirm

Before you confirm, the interface shows:

- **Entry price** — the price your position will open at, including [price impact](price-impact-and-slippage.md).
- **Liquidation price** — the price at which your position would be liquidated.
- **Opening fee** — see [Fees](fees.md).
- **Acceptable price / slippage** — the worst price you're willing to accept. If the market moves past it before your order fills, the order is cancelled rather than filled at a bad price.

## What happens after you confirm

0xMarkets uses a **two-step execution model** for fairness and front-running protection:

1. You submit the order from your wallet. Your collateral is escrowed. (You pay normal network gas for this transaction; the keeper's execution gas is covered by the protocol, not by you.)
2. A **keeper** picks up your order and executes it against a freshly signed oracle price, usually within seconds.

Because of this, your fill uses the price at *execution* time, not the moment you clicked. Your **acceptable price** is the guardrail: the order will not fill at a price worse than the limit you set. A market order that cannot be executed within **5 minutes** expires and can be cancelled, returning your collateral.

> **Market vs. trigger orders.** A market order fills as soon as the keeper can execute. Limit, stop, and TP/SL orders wait until the price condition you set is met. See [Order types](order-types.md).

## Costs to be aware of

Opening a position incurs an **opening fee**. While the position is open, you pay (or in some cases receive) **funding** and pay a **borrowing fee**. See [Fees](fees.md) and [Funding & borrowing](funding-and-borrowing.md).

## Next

- [Managing positions](managing-positions.md) — adjust collateral, set stops, partial close
- [Closing a trade](closing-a-trade.md) — take profit or cut a loss
- [Liquidations](liquidations.md) — how to avoid being liquidated
