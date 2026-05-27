# Delegated Miner

A **Delegated Miner** is an LP who provides liquidity through a registered **principal miner's hotkey** without operating any Bittensor infrastructure themselves. You lock USDC, the principal miner runs the subnet-side machinery, and rewards flow back to you according to a profit-sharing agreement.

> "Delegated Miner" is the protocol-facing name for what some surfaces and older docs call a **Federated Miner**. The two terms refer to the same role.

## Why Delegated Mining Exists

Running a Cartha principal miner requires:

* A registered Bittensor hotkey with TAO for registration
* A node that participates in subnet operations
* Active management of pool exposure and emissions

Most LPs don't want any of that. Delegated mining keeps the technical floor at "have an EVM wallet and USDC", while still earning the LP share of trading fees and a slice of ALPHA emissions.

## What You Get

* **31% of ALPHA emissions** flows to miners (split among all miners by deposit score) — your principal miner receives your portion and forwards it under your agreement
* **50% of trading fees** is paid directly into your vault in USDC — no principal-miner intermediation
* **Full ownership** of your locked USDC — only your wallet can withdraw it after lock expiry

## How It Works

```
  Delegated Miner (you)
       │
       │  lock USDC on-chain
       ▼
  Cartha Vault  ── trading fees ──►  paid directly to vault (USDC)
       │
       │  capital backs the principal miner's score
       ▼
  Principal Miner (hotkey)
       │
       │  receives ALPHA emissions
       ▼
  Distribution
       │
       └─► your share, per agreement / Cartha Rewards System
```

* Your **USDC** is custody'd by the vault smart contract, **not** by the principal miner
* The **principal miner cannot withdraw, move, or freeze** your locked capital
* The principal miner **does** receive your share of ALPHA emissions on Bittensor — that's where the trust assumption lives

## General Tensor (Recommended Default)

The 0xMarkets team operates **General Tensor**, the in-house principal miner. It's the recommended starting point for delegated miners.

| Detail | Info |
|--------|------|
| **Operator** | 0xMarkets team |
| **Commission** | 3% of ALPHA emissions |
| **Distribution** | Automated via Cartha Rewards System — calculated per epoch, claim directly from the dashboard |
| **Dashboard** | [liquidity.0xmarkets.io/principal-miners](https://liquidity.0xmarkets.io/principal-miners) |

To use General Tensor, copy its hotkey from the principal miners page and paste it when you lock via the "Become an LP" flow.

## Choosing a Different Principal Miner

Evaluate based on:

* **Track record** — distribution history, satisfied references, time operating
* **Commission** — what percentage of your ALPHA they take
* **Distribution method** — automated (Cartha Rewards System) is far lower trust than manual transfers
* **Communication** — how to reach them, what reporting they provide
* **Pool strategy** — which markets they back

**Red flags**: guaranteed returns, capital requests outside Cartha vaults, refusal to disclose commission, no track record.

**Green flags**: automated distribution, transparent reporting, satisfied delegated miners as references, clear disclosure of all terms upfront.

## Smart-Contract Protections

| What's protected on-chain | What relies on the principal miner |
|---------------------------|------------------------------------|
| Your USDC principal | ALPHA emission distribution |
| Withdrawal after lock + cooldown | Subnet performance / score |
| Lock terms (cannot be shortened or extended by anyone else) | Operational continuity |
| Trading fee accrual to the vault | — |

## Requirements

* **EVM wallet** (MetaMask, Rabby, etc.) on Base Mainnet
* **Base ETH** for gas
* **Base USDC** for the lock
* **Principal miner hotkey** (SS58 address) — General Tensor's is on the dashboard
* **Bittensor coldkey** (SS58 address) to claim your ALPHA payouts

## Risks

| Risk | Mitigation |
|------|------------|
| Principal miner fails to distribute | Use General Tensor or any miner on the Cartha Rewards System |
| LP losses from trader PnL / liquidations | See [Risk Management](risk-management.md) |
| Smart-contract risk | Audited by Hashlock — see [Security › Audits](../security/README.md) |
| Subnet performance below expectations | Diversify pools and principal miners |
| Network outages (Bittensor / Base) | Out of protocol control; positions resume when networks recover |

## Step-by-Step Walkthroughs

For setup, locking, and claiming, see the how-tos:

* [Become a Federated/Delegated Miner](../testnet/miner-guide.md) — testnet walkthrough
* [Deposit via Principal Miner](federated-miner-deposit-principal.md)
* [Direct Deposit (Any Hotkey)](federated-miner-deposit-direct.md)
* [Claim Rewards](claim-rewards.md)

> See [Legal & risk](../legal-and-risk.md) for full risk disclosures before locking capital.
