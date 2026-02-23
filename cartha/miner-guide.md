# Miner Guide

Everything you need to start mining on Cartha — whether you want to run your own operation or deposit into an existing one.

- **Web Interface**: [cartha.finance](https://cartha.finance)

---

## Two Ways to Mine

There are two paths to providing liquidity and earning ALPHA on Cartha. Pick the one that fits your setup:

| | Principal Miner | Federated Miner |
|---|---|---|
| **What you do** | Register a Bittensor hotkey, lock your own USDC, optionally accept external capital | Lock USDC through someone else's hotkey |
| **Bittensor setup** | Required (coldkey + hotkey + TAO for registration) | Not required |
| **CLI needed** | Yes, for subnet registration | No |
| **Earn from** | All emissions under your hotkey (your capital + federated miners') | Your proportional share of the principal miner's emissions |
| **Commission** | You set it (and keep it) | You pay it (typically 3–10%) |
| **Min. portfolio** | $100K total locked USDC (yours + federated) to start earning | No minimum (set by the principal miner) |
| **Infra** | Always-on distribution node required (public mode) | None |
| **Complexity** | Higher — run infra, manage distributions | Lower — just lock and track |
| **Best for** | Operators, teams, large capital | Individual LPs, passive earners |

### I want to run my own miner

Go to the **[Principal Miner Guide](principal-miner-guide.md)** — covers Bittensor wallet setup, subnet registration, locking funds, deploying the rewards system, and applying to get listed.

### I want to deposit into an existing miner

Go to the **[Federated Miner Guide](federated-miner-guide.md)** — covers wallet setup, choosing a principal miner, locking funds, and claiming ALPHA rewards. No CLI or Bittensor knowledge needed.

---

## Common Setup (Both Paths)

Both principal and federated miners need an EVM wallet on Base with ETH and USDC.

### 1. Add Base Mainnet to Your Wallet

Open MetaMask (or any EVM wallet) and add Base:

```
Network Name: Base
RPC URL: https://mainnet.base.org
Chain ID: 8453
Currency Symbol: ETH
Block Explorer URL: https://basescan.org
```

Or use [Chainlist](https://chainlist.org/) — search "Base" and click "Add to MetaMask".

### 2. Get Base ETH (for gas)

- Bridge from Ethereum via the [Base Bridge](https://bridge.base.org/)
- Or transfer from a centralized exchange that supports Base withdrawals

### 3. Get Base USDC (for liquidity)

- Bridge from Ethereum via the [Base Bridge](https://bridge.base.org/)
- Or transfer from a centralized exchange that supports Base withdrawals

---

## Available Pools

Both principal and federated miners can lock into any of these pools:

| Pool Name | Vault Token | Address |
|-----------|-------------|---------|
| BTC/USD | cvBTC | [`0xD090239EaE0d756726b6afd57E0b23A24FCABe86`](https://basescan.org/address/0xD090239EaE0d756726b6afd57E0b23A24FCABe86) |
| ETH/USD | cvETH | [`0x47EbDBE398733664250356F7F19fd516a5f1Dd0a`](https://basescan.org/address/0x47EbDBE398733664250356F7F19fd516a5f1Dd0a) |
| GOLD/USD | cvGOLD | [`0xabc777A16E41CF6E2F02A768D1f9f4d8aa68e58F`](https://basescan.org/address/0xabc777A16E41CF6E2F02A768D1f9f4d8aa68e58F) |
| EUR/USD | cvEUR | [`0x8AE6DDb449b3D8d1fE961483Fbe1329b5e4cbD86`](https://basescan.org/address/0x8AE6DDb449b3D8d1fE961483Fbe1329b5e4cbD86) |
| GBP/USD | cvGBP | [`0x9Eed917485e08FdFee977629bf933E8C0B33e539`](https://basescan.org/address/0x9Eed917485e08FdFee977629bf933E8C0B33e539) |
| JPY/USD | cvJPY | [`0xf2e3f581A7dE8B055c0122E3bFb445A67b485831`](https://basescan.org/address/0xf2e3f581A7dE8B055c0122E3bFb445A67b485831) |

**Network**: Base Mainnet (Chain ID: 8453)

---

## How Earnings Work

Miners earn from two sources:

| Source | Details |
|--------|---------|
| **Trading Fees (50% to LPs)** | Proportional to your locked USDC; based on pool trading volume; paid in USDC (stays in vault) |
| **ALPHA Emissions (31% to miners)** | The subnet emits 7,200 ALPHA per day. Miners collectively receive ~2,232 ALPHA/day. Your share is based on your **deposit score**. |

### Deposit Score

Your deposit score determines your share of daily emissions:

- **Score** = `amount_USDC × min(lock_days, 365) / 365`
- **Your share** = your score ÷ total score of all miners
- Longer locks = higher score per dollar = bigger share

### Epoch Cycle

Cartha operates on a **weekly epoch cycle**: Friday 00:00 UTC → Thursday 23:59 UTC.

- Lock by **Thursday 23:00 UTC** to be included in the next epoch (the indexer needs up to 15 minutes buffer)
- Positions locked after Friday 00:00 UTC go into the *following* week's epoch

> Learn more: [Weekly Epochs](../how-it-works/weekly-epochs.md) · [Fees & Rewards](../how-it-works/fees-and-rewards.md)

---

## Managing Positions

Once locked, manage your positions at [cartha.finance/positions](https://cartha.finance/positions):

| Action | Description |
|--------|-------------|
| **Top Up** | Add more USDC to an existing position |
| **Extend** | Increase lock duration for a higher score |
| **Withdraw** | Claim principal after lock expiry + 7-day cooldown |

### Withdrawal

When your lock expires and the 7-day cooldown has passed:

1. Go to "My Positions"
2. Click **"Withdraw"** on the expired position
3. Confirm the transaction in your wallet
4. USDC is returned to your connected EVM wallet

> The 7-day cooldown starts from lock creation, not expiry. See [Fees & Rewards](../how-it-works/fees-and-rewards.md) for details.

---

## Risks

All miners face these risks regardless of path:

| Risk | Details |
|------|---------|
| **Liquidation** | Your USDC provides real DEX liquidity. LP positions can be liquidated in volatile markets — capital loss is permanent. |
| **Smart Contract** | Vault contracts are audited but not risk-free. |
| **Network** | Bittensor or Base chain issues could delay emissions or transactions. |
| **No Guaranteed Returns** | Emissions depend on subnet performance and trading volume. |

---

## Next Steps

- **[Principal Miner Guide →](principal-miner-guide.md)** — Run your own miner operation
- **[Federated Miner Guide →](federated-miner-guide.md)** — Deposit into an existing miner
- **[Miner Dashboard →](principal-miner-dashboard.md)** — Track your earnings and performance
- **[Earning Estimator](https://cartha.finance/principal-miners)** — Model your returns before committing

---

**Ready to start?** Visit [cartha.finance](https://cartha.finance) and start earning ALPHA today.
