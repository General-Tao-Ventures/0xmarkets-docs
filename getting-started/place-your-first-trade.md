# Place your first trade

With a wallet connected and USDC on Base ready, you can open your first position. This is the beginner's walkthrough; for the full mechanics see [Opening a trade](../trading/opening-a-trade.md).

## 1. Choose a market

Pick from any of the listed markets across FX, commodities, and crypto. A good first trade is a market you already follow. See the full list in [Markets](../reference/markets.md).

## 2. Pick long or short

- **Long** — you profit if the price goes up.
- **Short** — you profit if the price goes down.

You're not buying the asset; you're taking a leveraged position on its price either way.

## 3. Set collateral and leverage

- **Collateral** is the USDC you put up to back the position. It's also the most you can lose on the trade (plus fees).
- **Leverage** multiplies your position size — and both your gains and your losses. Your **position size** = collateral × leverage. For example, $500 of collateral at 10x controls a $5,000 position.

The maximum leverage you can use depends on the asset class **and** how large your position is — larger positions are capped at lower leverage. This is the **leverage ladder**; see [Leverage & margin](../trading/leverage-and-margin.md) for the full tiers. Start conservative: higher leverage means a smaller price move can liquidate you.

## 4. Review before you confirm

Before confirming, the interface shows the key numbers:

- **Entry price** — the price your position will open at, including [price impact](../trading/price-impact-and-slippage.md).
- **Liquidation price** — the price at which your position would be liquidated. See [Liquidations](../trading/liquidations.md).
- **Fees** — the opening fee for the trade. See [Fees](../trading/fees.md).
- **Acceptable price** — the worst price you're willing to accept. If the market moves past it before your order fills, the order is cancelled rather than filled at a bad price.

## 5. Confirm — and the keeper executes

When you confirm, you sign the order from your wallet and your collateral is escrowed. A **keeper** then picks up your order and executes it against a freshly signed oracle price, usually within seconds. The keeper's gas is covered by the protocol — you only pay normal network gas for your own transaction.

Because of this two-step model, your fill uses the price at *execution* time, not the moment you clicked — and your **acceptable price** is the guardrail against a bad fill. See [Opening a trade](../trading/opening-a-trade.md) for the full detail on execution.

That's it — your position is live. Watch it, manage it, and close it when you're ready.

## Next

- [Managing positions](../trading/managing-positions.md) — adjust collateral, set stop-loss / take-profit, partial close
- [Closing a trade](../trading/closing-a-trade.md) — take profit or cut a loss
- [Liquidations](../trading/liquidations.md) — how to avoid being liquidated

> Nothing here is financial advice. Perpetual futures with leverage carry a high risk of loss.
