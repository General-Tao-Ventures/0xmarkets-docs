# Become a Liquidity Provider

Everything you need to start providing liquidity on the **0xMarkets Liquidity Engine** — whether you want to run your own operation or deposit into an existing one.

- **Web interface:** [liquidity.0xmarkets.io](https://liquidity.0xmarkets.io)

---

## Two ways to provide liquidity

There are two paths to backing the 0xMarkets markets and earning ALPHA. Pick the one that fits your setup.

| | Principal Miner | Federated Miner |
|---|---|---|
| **What you do** | Register a Bittensor hotkey, lock your own USDC, optionally accept external capital | Lock USDC through someone else's hotkey |
| **Bittensor setup** | Required (coldkey + hotkey + TAO for registration) | Not required |
| **CLI needed** | Yes, for subnet registration | No |
| **Earn from** | All emissions under your hotkey (your capital + federated miners') | Your proportional share of the principal miner's emissions |
| **Commission** | You set it (and keep it) | You pay it (typically 3–10%) |
| **Min. portfolio** | 100,000 USDC total locked (yours + federated) to start earning | No protocol minimum (set by the principal miner) |
| **Infra** | Always-on distribution node required (public mode) | None |
| **Complexity** | Higher — run infra, manage distributions | Lower — just lock and track |
| **Best for** | Operators, teams, large capital | Individual LPs, passive earners |

### I want to run my own miner

Go to the **[Principal Miner Guide](principal-miner-guide.md)** — covers Bittensor wallet setup, subnet registration, locking funds, deploying the rewards system, and applying to get listed.

### I want to deposit into an existing miner

Go to the **[Federated Miner Guide](federated-miner-guide.md)** — covers wallet setup, choosing a principal miner, locking funds, and claiming ALPHA. No CLI or Bittensor knowledge needed.

---

## Common setup (both paths)

Both principal and federated miners need an EVM wallet on Base with ETH and USDC.

### 1. Add Base mainnet to your wallet

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
- Or transfer from a centralized exchange that supports Base USDC withdrawals

---

## Available pools

Both principal and federated miners can lock into any of these per-market vaults. Each vault backs one market and is risk-isolated from the others.

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

**Network:** Base mainnet (Chain ID: 8453)

---

## How earnings work

Liquidity providers earn from two independent sources:

| Source | Details |
|--------|---------|
| **Trading-fee yield** | A share of trading fees in your market accrues to the vault, raising its NAV per share. **50% of trading fees** go to the LP pool. Paid in USDC, realised when you withdraw — no separate claim. |
| **ALPHA emissions** | The subnet directs ALPHA to LPs via Bittensor weights. Your share is set by your **deposit score**. Claimed separately to a Bittensor coldkey. |

> Daily ALPHA emissions are split **41% validators, 31% liquidity providers (miners), 18% subnet owner, 10% incentive pool.** LPs share the 31% miner allocation by deposit score. See [Fees & rewards](../how-it-works/fees-and-rewards.md).

### Deposit score

Your deposit score determines your share of daily ALPHA emissions:

- **Score** = `amount_USDC × min(lock_days, 365) / 365`
- **Your share** = your score ÷ total score of all miners
- Longer locks = higher score per dollar = bigger share

### Epoch cycle

The 0xMarkets Liquidity Engine runs on a **7-day epoch cycle**: Friday 00:00 UTC → Thursday 23:59 UTC.

- Lock by **Thursday 23:00 UTC** to be included in the next epoch (the indexer needs up to 15 minutes buffer)
- Positions locked after Friday 00:00 UTC go into the *following* week's epoch

> Learn more: [Weekly Epochs](../how-it-works/weekly-epochs.md) · [Fees & Rewards](../how-it-works/fees-and-rewards.md)

---

## Managing positions

Once locked, manage your positions at [liquidity.0xmarkets.io/manage](https://liquidity.0xmarkets.io/manage):

| Action | Description |
|--------|-------------|
| **Top Up** | Add more USDC to an existing position |
| **Extend** | Increase lock duration for a higher score |
| **Withdraw** | Reclaim principal after lock expiry, once the 7-day cooldown has passed |

### Withdrawal

When your lock expires and the 7-day cooldown has passed:

1. Go to "My Positions"
2. Click **"Withdraw"** on the expired position
3. Confirm the transaction in your wallet
4. USDC is returned to your connected EVM wallet

> The 7-day cooldown runs from lock creation, not expiry — for any lock of 30+ days it has already elapsed by the time the lock expires. See [How to Withdraw](how-to-withdraw.md).

---

## Risks

All liquidity providers face these risks regardless of path:

| Risk | Details |
|------|---------|
| **You are the trader's counterparty** | Your USDC backs real positions. When traders profit, the vault pays; outlier moves, concentration, or skilled flow can move LP capital faster than fees cushion it. Capital loss is permanent. |
| **Smart contract** | Vault contracts are audited but not risk-free. |
| **Network** | Bittensor or Base issues could delay emissions or transactions. |
| **No guaranteed returns** | Emissions and fee yield depend on subnet performance and trading volume. |

See [Risk disclosures](../security/risk-disclosures.md) for the full picture.

---

## Next

- [Principal Miner Guide](principal-miner-guide.md) — run your own miner operation
- [Federated Miner Guide](federated-miner-guide.md) — deposit into an existing miner
- [The Liquidity Interface](interface.md) — the web app for locking and managing
- [Principal Miner Dashboard](principal-miner-dashboard.md) — track earnings and performance

---

> 0xMarkets is in **Beta** — live and fully functional, and being actively refined. Visit the [Liquidity Interface](https://liquidity.0xmarkets.io) to start.
