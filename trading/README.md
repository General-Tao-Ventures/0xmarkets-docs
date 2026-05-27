# Trading on 0xMarkets

> ⚠️ **Trading is currently in testnet.** The exchange runs on **Base Sepolia** (testnet). No real funds are at risk. Mainnet trading will launch in a future release — see the [Roadmap](../roadmap.md).

## What is 0xMarkets

0xMarkets is a decentralized perpetual futures exchange deployed on Base Sepolia.

* **Oracle-based pricing** — prices are sourced from aggregated exchange data via Pyth Network, ensuring accurate and tamper-resistant price feeds
* **Up to 500x leverage** on FX pairs, crypto assets, commodities, and real-world assets (RWAs)
* **USDC-only collateral** — all markets use USDC as the sole collateral token, simplifying position management

## Getting Started

1. **Connect a wallet** — MetaMask, Rabby, or any WalletConnect-compatible wallet
2. **Fund your wallet with ETH on Base Sepolia** — you need ETH to pay gas fees for transactions
3. **Navigate to [app.0xmarkets.io](https://app.0xmarkets.io/#/)** to browse available markets and open positions

### Key Pages

| Page | URL |
|------|-----|
| Trade | [app.0xmarkets.io/#/](https://app.0xmarkets.io/#/) |
| Pools | [app.0xmarkets.io/#/pools](https://app.0xmarkets.io/#/pools) |
| Leaderboard | [app.0xmarkets.io/#/leaderboard](https://app.0xmarkets.io/#/leaderboard) |
| Stats | [app.0xmarkets.io/#/stats](https://app.0xmarkets.io/#/stats) |

## Multichain Trading

0xMarkets Account enables trading from any supported chain without manually bridging funds.

* Funds deposited on any supported network are automatically bridged to the settlement chain
* Your balance is usable across all supported networks
* No need to switch chains or manage bridging separately

## RPC URLs

0xMarkets automatically selects reading RPCs for reliability, but transaction RPCs depend on your wallet configuration.

* If transactions fail or take too long, try changing the RPC URL in your wallet settings
* Use [chainlist.org](https://chainlist.org) to find alternative Base Sepolia RPC endpoints
* Multiple RPC providers are available — switching can resolve intermittent connection issues
