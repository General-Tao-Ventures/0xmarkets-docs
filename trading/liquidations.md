# Liquidations

A position is **liquidated** when its losses eat through your margin down to the minimum the system requires to keep it open. This page explains exactly when that happens, what it costs, and how to avoid it.

> **The one thing to know:** a liquidation closes your entire margin. There is no partial refund. If you want to exit before that point and keep what's left, use a [stop-loss](order-types.md).

## When you get liquidated

Every position must hold a minimum amount of collateral called the **maintenance margin**. When your remaining equity (collateral ± unrealized PnL, minus fees) falls to that level, a keeper closes the position automatically. There are no margin calls and no warnings.

The maintenance margin isn't a flat number — it scales with how much leverage you're using, through the **Maintenance Margin Rate (MMR)**:

```
MMR = clamp(  (Your Leverage ÷ Market's Max Leverage) × 20%,   min 1%,   max 20%  )

Maintenance margin (USD) = Your Collateral × MMR
```

In plain terms:

- The closer you trade to a market's maximum leverage, the higher your MMR — up to a ceiling of **20%**.
- The more conservative your leverage, the lower your MMR — down to a floor of **1%**.
- A position right at the market's max leverage carries a 20% MMR; a lightly-leveraged one sits at the 1% floor.

So higher leverage means you're liquidated after a *smaller* adverse move. The trade-off for the bigger position is a thinner safety buffer.

### MMR by leverage (example: an FX market, max 500x)

| Your leverage | MMR | Maintenance margin on $1,000 | Liquidated after an adverse move of about |
|---|---|---|---|
| 500x (max) | 20% | $200 | 0.16% |
| 100x | 4% | $40 | 0.96% |
| 50x | 2% | $20 | 1.96% |
| 20x | 1% (floor) | $10 | 4.95% |

The same formula applies to every market — only the *max leverage* changes (FX 500x, commodities 200x, crypto 100x), which shifts where each leverage level lands on the MMR scale. (Adverse-move figures ignore fees, which bring liquidation slightly sooner.)

## What a liquidation costs you

When your position is liquidated, three things happen in order:

1. **Your position is closed at the current market price.**
2. **Your trading loss is paid to the liquidity providers** who took the other side of your trade — this is the bulk of your margin.
3. **Your remaining margin — the maintenance-margin buffer — is taken as the liquidation fee.**

The net result: **you forfeit 100% of your margin.** The liquidation fee is, in effect, your maintenance margin:

```
Liquidation fee ≈ Maintenance margin = Your Collateral × MMR
```

### Worked example — $1,000 margin, 100x on an FX market

- **MMR** = clamp((100 ÷ 500) × 20%, 1%, 20%) = **4%** → maintenance margin = **$40**.
- You're liquidated when the market moves about **0.96%** against you.
- Position closes at market: roughly **$960** of loss is paid to the liquidity providers.
- Your remaining **~$40** (the maintenance margin) is taken as the **liquidation fee**.
- **Returned to you: $0.**

Had you instead set a stop-loss before that point, you'd have closed as a normal trade — paying only the standard [closing fee](fees.md) and keeping the rest of your margin.

## Where the liquidation fee goes

The liquidation fee is distributed:

| Destination | Share |
|---|---|
| **Insurance pool** | 70% |
| **Alpha buyback** | 30% |

The insurance pool backs the exchange against extreme events; the buyback directs value to the Alpha token. *(Liquidation-fee distribution is set by the protocol and is planned to come under governance control in a future release.)*

## How to avoid liquidation

- **Use lower leverage** — it lowers your MMR and pushes your liquidation point much further away.
- **Add collateral** if a position moves against you — this lowers your effective leverage in real time. See [Managing positions](managing-positions.md).
- **Set a stop-loss** — exit on your own terms and keep your remaining margin instead of forfeiting all of it.

## Next

- [Leverage & margin](leverage-and-margin.md)
- [Managing positions](managing-positions.md)
- [PnL & profit settlement](pnl-and-settlement.md)
