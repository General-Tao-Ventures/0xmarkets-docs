# Deposit USDC

**USDC on Base is the collateral for every market** on 0xMarkets — FX, commodities, and crypto. To trade, you need USDC in your connected wallet.

## What you need

- **USDC on Base** — your trading collateral.
- A little **ETH on Base** — to pay normal network gas on your own transactions (placing or cancelling an order). You don't pay the keepers that execute your trades — that cost is covered by the protocol. See [Pricing & the oracle](../trading/pricing-and-oracle.md) for how keeper execution works.

## Getting USDC onto Base

You need USDC held on the **Base network**, in the same wallet you connected. A few common ways to get there:

- Buy or transfer USDC directly on Base from an exchange that supports Base withdrawals.
- Bridge USDC from another chain to Base, then send it to your wallet.

The exact steps depend on the wallet and the exchange or bridge you use, so follow their instructions. Whatever route you take, the end state is the same: **USDC sitting on Base in your connected wallet**, with a little ETH on Base alongside it for gas.

## How collateral works

The USDC you commit to a position is your **collateral**. It backs the position and is **the most you can lose on that trade** (plus fees). If the market moves far enough against you, the position is liquidated and your collateral for it is lost — it does not go negative, and it cannot pull from the rest of your wallet. See [Liquidations](../trading/liquidations.md) for exactly when that happens and what it costs.

You decide how much collateral to put behind each position when you open it — you don't pre-fund a single house account. Your USDC stays in your wallet until you open a trade.

## Next

- [Place your first trade](place-your-first-trade.md)
- [Leverage & margin](../trading/leverage-and-margin.md) — how collateral and leverage set your position size
- [Liquidations](../trading/liquidations.md) — protecting your collateral
