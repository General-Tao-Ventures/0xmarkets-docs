# Providing Liquidity

Every trade on 0xMarkets has a counterparty: a pool of capital supplied by **liquidity providers (LPs)**. When traders lose, the pool collects; when traders win, the pool pays. In exchange for taking that side, LPs earn a share of trading fees plus ALPHA emissions. This section is the operator's manual for becoming an LP.

> A trader and a liquidity provider are not mutually exclusive. The same person can trade the exchange and provide liquidity to it — they are separate activities with separate wallets and separate risk.

## What providing liquidity means

You deposit **USDC** (on Base) into a **per-market vault**. That capital becomes the liquidity traders trade against in that single market. You do **not** quote prices, run a market-making bot, or manage spreads — pricing comes from the [Pyth Pro oracle](../trading/pricing-and-oracle.md) and an on-chain price-impact model. Your job is simply to supply capital and commit it for a chosen term.

Each market has its **own vault**, isolated from the others. A drawdown in one market's vault does not touch the others — risk is contained per market. Vault shares are **non-transferable**: you hold the position, and only you can withdraw it when the term ends.

## The two earning streams

Providing liquidity pays in two independent ways:

1. **Trading-fee yield.** A share of the trading fees paid in your market accrues to the vault, raising the vault's net asset value (NAV) per share. You realise this automatically when you withdraw — there is nothing to claim. The trading-fee split directs **50% to the LP pool** (see [Fees](../trading/fees.md)).
2. **ALPHA emissions.** The Bittensor liquidity subnet (SN35) emits ALPHA, and a portion is directed to LPs via subnet weights. Your share is driven by your **deposit score** — a function of how much USDC you lock and for how long. ALPHA emissions are claimed separately to a Bittensor coldkey (see [Claim Rewards](claim-rewards.md)).

> These streams are independent. Trading-fee yield builds inside the vault (in USDC); ALPHA emissions accrue off the subnet and are claimed to a Bittensor wallet.

## Vault rules at a glance

| Rule | Value |
|---|---|
| **Collateral** | USDC on Base |
| **Vaults** | One per market (risk-isolated) |
| **Vault shares** | Non-transferable |
| **Minimum lock** | 100,000 USDC |
| **Maximum lock** | 365 days |
| **Withdrawal cooldown** | 7 days |
| **Epoch length** | 7 days |

> The **100,000 USDC minimum** applies to a principal miner's total vault (their own capital plus any federated capital locked through them). An individual federated miner locking *through* a principal miner has no protocol-level minimum — the principal miner sets that. See [Become a Liquidity Provider](miner-guide.md).

## Who can provide liquidity

Anyone with USDC on Base and an EVM wallet. There are two paths:

- **Principal miner** — you register a Bittensor hotkey, lock your own USDC, and optionally accept external capital from federated miners. Requires Bittensor setup and an always-on distribution node if you run in public mode.
- **Federated miner** — you lock USDC *through* an existing principal miner's hotkey using only an EVM wallet. No Bittensor node, no CLI. You earn your proportional share of that miner's emissions, minus their commission.

If you have capital but no Bittensor setup, start as a federated miner. See [Become a Liquidity Provider](miner-guide.md) to choose your path.

## Markets you can back

| Pool | Vault token | Address |
|---|---|---|
| BTC/USD | cvBTC | [`0xD090239EaE0d756726b6afd57E0b23A24FCABe86`](https://basescan.org/address/0xD090239EaE0d756726b6afd57E0b23A24FCABe86) |
| ETH/USD | cvETH | [`0x47EbDBE398733664250356F7F19fd516a5f1Dd0a`](https://basescan.org/address/0x47EbDBE398733664250356F7F19fd516a5f1Dd0a) |
| TAO/USD | cvTAO | [`0x47C563FFa0aB3e952561a72D3F09ec2c8ADb7FD5`](https://basescan.org/address/0x47C563FFa0aB3e952561a72D3F09ec2c8ADb7FD5) |
| GOLD/USD | cvGOLD | [`0xabc777A16E41CF6E2F02A768D1f9f4d8aa68e58F`](https://basescan.org/address/0xabc777A16E41CF6E2F02A768D1f9f4d8aa68e58F) |
| SILVER/USD | cvSILVER | [`0x48682e7Bf092219e27D27F7A8d01b2538A828998`](https://basescan.org/address/0x48682e7Bf092219e27D27F7A8d01b2538A828998) |
| EUR/USD | cvEUR | [`0x8AE6DDb449b3D8d1fE961483Fbe1329b5e4cbD86`](https://basescan.org/address/0x8AE6DDb449b3D8d1fE961483Fbe1329b5e4cbD86) |
| GBP/USD | cvGBP | [`0x9Eed917485e08FdFee977629bf933E8C0B33e539`](https://basescan.org/address/0x9Eed917485e08FdFee977629bf933E8C0B33e539) |
| JPY/USD | cvJPY | [`0xf2e3f581A7dE8B055c0122E3bFb445A67b485831`](https://basescan.org/address/0xf2e3f581A7dE8B055c0122E3bFb445A67b485831) |

**Network:** Base mainnet (Chain ID: 8453). **Web interface:** [liquidity.0xmarkets.io](https://liquidity.0xmarkets.io).

## Network details

- **Liquidity network:** 0xMarkets Liquidity Engine on **Bittensor Subnet 35 (SN35)**, on the `finney` (Bittensor mainnet) network
- **EVM chain:** Base mainnet (Chain ID: `8453`)
- **What you need:** an EVM wallet with ETH (gas) and USDC (liquidity); a Bittensor coldkey to claim ALPHA; TAO only if you register your own hotkey as a principal miner

## Security

The 0xMarkets Liquidity Engine contracts were audited by **Hashlock**. A comprehensive end-to-end review with HackenProof is in progress. See [Audits](../security/audits.md).

> 0xMarkets is in **Beta** — live and fully functional, and being actively refined. Some parameters will be tuned as it matures.

## Next

- [The Liquidity Interface](interface.md) — the web app for locking and managing positions
- [Become a Liquidity Provider](miner-guide.md) — choose your path and get started
- [Federated Miner Guide](federated-miner-guide.md) — lock through an existing miner, no Bittensor setup
- [Risk disclosures](../security/risk-disclosures.md) — the risks of providing liquidity
