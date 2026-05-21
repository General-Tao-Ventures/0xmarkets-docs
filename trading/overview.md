# Trading Overview

0xMarkets is a decentralized perpetual futures exchange offering up to **500x leverage** on FX pairs, commodities, crypto, and other real-world assets (RWAs). Trading is permissionless — no KYC, no whitelist — and all positions are collateralized in USDC.

## Why 0xMarkets

* **Oracle-based pricing** — prices stream from aggregated exchange data via [Pyth Network](https://pyth.network/), cross-verified by validators on the [Cartha](../cartha/README.md) subnet
* **Up to 500x leverage** on supported markets
* **USDC-only collateral** — one collateral token across all markets, no margin token swaps to manage
* **Deep, isolated liquidity** — each market draws from its own Cartha vault, so risk in one market does not bleed into others
* **Multichain accounts** — fund your account on any supported network; balances bridge automatically to the settlement chain

## Supported Markets

Markets cover four asset classes:

* **Crypto** — BTC/USD, ETH/USD (24/7)
* **FX** — EUR/USD, GBP/USD, USD/JPY (Sunday 5PM ET → Friday 5PM ET)
* **Metals** — GOLD/USD
* **Commodities** — WTI/USD

See [Market Hours](market-hours.md) for the full schedule.

## How a Trade Works

1. **Connect a wallet** — MetaMask, Rabby, or any WalletConnect-compatible wallet
2. **Deposit USDC** as collateral (see [Collateral](collateral.md))
3. **Choose a market** and select long or short
4. **Pick a leverage tier** — interface will warn before max leverage is exceeded
5. **Submit the order** — a keeper executes against the oracle price (see [Order Types](order-types.md))
6. **Manage the position** — adjust collateral, set take-profit / stop-loss, or close at any time

Fees are detailed in [Trading Fees](fees.md). Margin breaches are handled per [Liquidations](liquidations.md).

## Earning While Trading

Traders can earn from the **incentive pool** — 10% of total Cartha ALPHA emissions — via:

* **Weekly leaderboard rewards** based on volume and activity
* **Introducing Broker (IB) rebates** for referred trading volume

Track rewards at [liquidity.0xmarkets.io/leaderboard](https://liquidity.0xmarkets.io/leaderboard). See [Alpha Token › Incentives](../alpha-token/incentives.md) for the full mechanism.

## RPC Reliability

0xMarkets auto-selects reading RPCs, but **transaction** RPCs come from your wallet config. If transactions stall or fail, swap the Base RPC URL in your wallet using endpoints from [chainlist.org](https://chainlist.org).

> Risk: Perpetual futures with leverage are high-risk products. See [Legal & risk](../legal-and-risk.md) before trading.
