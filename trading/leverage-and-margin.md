# Leverage & margin

Leverage lets you control a position larger than your collateral. 0xMarkets offers high leverage, but the maximum you can use depends on **two things**: the asset class you're trading, and how large your position is.

## Maximum leverage by asset class

Each asset class has a headline maximum:

| Asset class | Maximum leverage |
|---|---|
| **FX** (EUR, GBP, JPY) | up to **500x** |
| **Commodities** (gold, silver, oil) | up to **200x** |
| **Crypto** (BTC, ETH, TAO) | up to **100x** |

These are the ceilings. The leverage actually available to you also depends on your position size — see the ladder below.

## The leverage ladder

The maximum leverage **decreases as your position size grows.** A small position can use the highest leverage; a large position is capped lower. This protects both you and the liquidity pool from outsized risk on a single position.

At launch, the ladder is set as follows. The tier is based on your **position notional** (collateral × leverage), not your collateral.

**FX**

| Position size | Max leverage |
|---|---|
| up to $50,000 | 200x |
| up to $200,000 | 150x |
| up to $500,000 | 100x |
| up to $1,000,000 | 50x |
| up to $2,500,000 | 25x |
| above $2,500,000 | 10x |

**Commodities**

| Position size | Max leverage |
|---|---|
| up to $50,000 | 100x |
| up to $200,000 | 75x |
| up to $500,000 | 50x |
| up to $1,000,000 | 25x |
| up to $2,500,000 | 15x |
| above $2,500,000 | 5x |

**Crypto**

| Position size | Max leverage |
|---|---|
| up to $25,000 | 50x |
| up to $100,000 | 25x |
| up to $250,000 | 15x |
| up to $500,000 | 10x |
| up to $1,000,000 | 5x |
| above $1,000,000 | 3x |

> **Launch note.** The ladder above is the configuration for the initial mainnet launch. The headline maximums (500x / 200x / 100x) are the ceilings the ladder will expand toward over time as the exchange and its liquidity grow.

## Maintenance margin

To keep a position open, your equity must stay above a **maintenance margin** — a minimum fraction of your collateral. If it falls below, the position is liquidated.

0xMarkets uses a **dynamic maintenance margin** that scales with how aggressively you're leveraged, through the **Maintenance Margin Rate (MMR)**:

```
MMR = clamp(  (Your Leverage ÷ Market's Max Leverage) × 20%,   min 1%,   max 20%  )
```

- A position near its market's maximum leverage carries the highest MMR — up to a **20%** ceiling (less room before liquidation).
- A conservatively-leveraged position floors at **1%** (lots of room).

In practice: the higher your leverage, the closer your liquidation price sits to your entry. The lower your leverage, the more the market can move against you before you're at risk. See [Liquidations](liquidations.md) for the full formula, a worked example, and what a liquidation costs.

## A worked example

You open a **$2,000 collateral** long on EUR/USD at **20x** leverage:

- Position size = $2,000 × 20 = **$40,000** notional → within the ≤$50k FX tier, so 20x is allowed.
- A **+1%** move in EUR/USD = +$400 → **+20%** on your collateral.
- A **−1%** move = −$400 → **−20%** on your collateral.

Because you're well below the 200x cap for this size, your maintenance margin is low and your liquidation price is comfortably far from entry. Push the leverage toward the cap and that margin for error shrinks fast.

## Next

- [Liquidations](liquidations.md)
- [Fees](fees.md)
- [Markets](../reference/markets.md)
