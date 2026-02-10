# Federated Miners

**Role:** External investors who lock capital through registered principal miners without operating Bittensor infrastructure.

**Also known as:** External Liquidity Providers, Pool Participants, Delegators

---

## Overview

Federated Miners enable anyone with USDC and an EVM wallet to participate in Cartha subnet's liquidity provision without the technical complexity of running Bittensor infrastructure. You lock capital through a registered principal miner's hotkey, maintain full ownership of your position, and can withdraw after your lock period expires.

Your locked USDC provides liquidity for [0xMarkets](https://0xmarkets.io), a decentralized perpetual futures exchange built by the same team behind Cartha. In return, you earn a share of trading fees and ALPHA emissions from the Bittensor subnet.

### General Tensor — The Recommended Starting Point

The 0xMarkets team operates **General Tensor**, an in-house principal miner available to all federated miners. If you're new to Cartha or don't have a specific principal miner in mind, General Tensor offers:

- **Automated distribution** — Rewards are calculated and claimable epoch-by-epoch on the [Principal Miners dashboard](https://cartha.finance/principal-miners)
- **Transparent commission** — Rate is publicly displayed on the dashboard
- **Team-operated** — Run by the same team that built the subnet and the exchange
- **No off-chain agreements needed** — Everything is handled through the dashboard

> You can lock to General Tensor or any other registered principal miner. See [Choosing a Principal Miner](#choosing-a-principal-miner) for guidance.

### Key Benefits

- **No Bittensor Setup Required** — Just an EVM wallet and USDC on Base
- **Non-Custodial** — Your USDC is locked in a smart contract; the principal miner cannot access or withdraw it
- **Direct Withdrawals** — No principal miner approval needed to withdraw after lock expiry
- **Choose Your Manager** — Lock to General Tensor or any registered principal miner
- **Flexible Lock Periods** — 7 to 365 days
- **No CLI Required** — Everything is done through the web interface

### Key Considerations

- **Emissions Go to Principal Miner First** — ALPHA emissions are initially received by the principal miner's Bittensor wallet, then distributed to you (this is the core trust assumption — use a trusted operator like General Tensor to reduce this risk)
- **Your Funds Stay Yours** — The principal miner cannot access your committed USDC; only you can withdraw it after lock expiry
- **LP Risk Applies** — Your USDC provides liquidity for the 0xMarkets DEX; liquidation losses from volatile markets may reduce your capital
- **Rewards Are Not Guaranteed** — Emissions depend on subnet performance, trading volume, and your deposit score

---

## How It Works

### System Architecture

```
┌─────────────────────────────────────────────┐
│     You (Federated Miner)                   │
│     - Lock USDC via EVM wallet              │
│     - Own position via smart contract       │
│     - Receive profit share (off-chain)      │
└─────────────────────────────────────────────┘
                    ↓
         Lock capital to hotkey
                    ↓
┌─────────────────────────────────────────────┐
│     Principal Miner                         │
│     - Registered Bittensor hotkey           │
│     - Manages pool strategy                 │
│     - Receives all ALPHA emissions          │
│     - Distributes to you per agreement      │
└─────────────────────────────────────────────┘
                    ↓
         Performance scoring
                    ↓
┌─────────────────────────────────────────────┐
│     Cartha Subnet Validators                │
│     - Score principal miner performance     │
│     - Distribute ALPHA emissions            │
└─────────────────────────────────────────────┘
```

### Smart Contract Protection

Your position is secured on-chain:

**What You Control:**
- Position ownership (via your EVM wallet)
- Capital withdrawal after lock expiry
- No principal miner approval needed to withdraw
- Independent locking (no CLI or miner coordination required)

**What You Don't Control:**
- ALPHA emissions (sent to principal miner's Bittensor wallet)
- Pool performance (managed by principal miner)
- Liquidation events (market-driven from DEX activity)

---

## Becoming a Federated Miner

To start as a federated miner you need:

- An **EVM wallet** (MetaMask or similar) connected to Base Mainnet
- **Base ETH** for gas fees
- **Base USDC** for your deposit
- A **principal miner's hotkey** (SS58 address) to lock through

> 📘 **Step-by-step instructions:** See the [Federated Miner Guide](../cartha/federated-miner-guide.md) for a complete walkthrough on setting up your wallet, locking funds, using the Principal Miner dashboard, and claiming ALPHA rewards — no CLI required.

---

## Choosing a Principal Miner

### General Tensor (In-House Option)

The simplest way to start is by locking to **General Tensor**, the principal miner operated by the 0xMarkets team:

| Detail | Info |
|--------|------|
| **Operator** | 0xMarkets team (builders of Cartha subnet and 0xMarkets exchange) |
| **Commission** | 3% of ALPHA emissions |
| **Distribution** | Automated — rewards are calculated per epoch and claimable directly from the dashboard |
| **Dashboard** | [cartha.finance/principal-miners](https://cartha.finance/principal-miners) — view performance, earnings, and claim rewards |

To lock to General Tensor, copy the hotkey from the [Principal Miners page](https://cartha.finance/principal-miners) and use it when locking via "Become an LP".

### Evaluating Other Principal Miners

If you prefer a different operator, evaluate them on:

- **Track record and reputation** — Past performance and distribution history
- **Commission rate** — The percentage they take from your rewards
- **Distribution method** — Automated (Cartha Rewards System) vs. manual
- **Communication** — Active channels (Discord, Telegram, email) and responsiveness
- **Pool strategy** — Which markets they operate in and why

### Where to Find Principal Miners

- **General Tensor:** [cartha.finance/principal-miners](https://cartha.finance/principal-miners) — the team-operated default
- **Leaderboard:** [cartha.finance/leaderboard](https://cartha.finance/leaderboard) — view top-performing miners
- **Community:** [Discord](https://discord.gg/zGkW2kTsGM) and Telegram groups
- **Direct Outreach:** Post your capital amount and preferred lock duration in community channels

### Red Flags

Avoid principal miners who:
- Promise guaranteed returns
- Request capital outside of Cartha vaults
- Refuse to disclose their commission rate or terms
- Don't use the automated distribution system without clear justification
- Have no track record or references

### Green Flags

Look for principal miners who:
- Use the automated Cartha Rewards System for transparent distribution
- Provide transparent performance reporting
- Have satisfied federated miners as references
- Disclose all risks and commission upfront
- Maintain consistent distribution history

---

## Understanding the Terms

### If You're Using General Tensor

If you lock to the in-house General Tensor principal miner, the terms are straightforward:

- **Commission rate** is 3% of your ALPHA emissions per epoch
- **Distribution is automated** — rewards accumulate per epoch and you claim them directly from the dashboard
- **No separate agreement needed** — everything is handled through the Cartha Rewards System
- You still need a **Bittensor coldkey** (SS58 address) to claim your ALPHA rewards

### If You're Using Another Principal Miner

Since ALPHA emissions go to the principal miner's wallet first, you need a clear arrangement for profit sharing. Cartha does **not** enforce these agreements on-chain — they are between you and the principal miner.

**What to clarify before locking:**

| Topic | Details |
|-------|---------|
| **Commission Rate** | What percentage does the principal miner take from your rewards? |
| **Distribution Method** | Automated (Cartha Rewards System) or manual? If manual, how often? |
| **Lock Terms** | Preferred pool, lock duration, any minimum amounts |
| **Communication** | How will you reach them? What reporting will they provide? |

> **Tip:** Prefer principal miners who use the automated Cartha Rewards System. This significantly reduces distribution risk because rewards are calculated transparently and you claim directly — no manual transfers required.

---

## Managing Your Position

Once locked, you can manage your position through the [Cartha web interface](https://cartha.finance):

- **View Positions** — See all your active locks, amounts, and expiry dates
- **Top Up** — Add more USDC to an existing position (no principal miner approval needed)
- **Extend Lock** — Increase lock duration for a higher subnet score and better emissions
- **Withdraw** — Claim your principal after lock expiry (minus any liquidation losses)

> 📘 **Detailed instructions:** See the [Federated Miner Guide](../cartha/federated-miner-guide.md) for step-by-step position management with screenshots.

---

## Risks & Protections

### What You're Protected From

| Protection | Details |
|-----------|---------|
| **Principal Theft** | Your USDC is in a smart contract, not the principal miner's wallet |
| **Forced Lock Extension** | Principal miner cannot extend your lock |
| **Arbitrary Terms Changes** | On-chain lock terms are immutable |

### What You're NOT Protected From

| Risk | Details |
|------|---------|
| **Distribution Risk** | If you use a principal miner that doesn't use the automated rewards system, they could fail to distribute your share. **Mitigation:** Use General Tensor or a principal miner on the Cartha Rewards System. |
| **Liquidation Losses** | Your USDC provides DEX liquidity. LP positions can be liquidated in volatile markets; capital loss is permanent and not reimbursed. |
| **Poor Performance** | Low trading volume or a bad subnet score reduces ALPHA emissions. Returns are not guaranteed. |
| **Smart Contract Risk** | Vault contracts are audited but not risk-free. Bugs or exploits could result in loss of locked funds. |
| **Network Risk** | Bittensor network issues or Base chain downtime could delay emissions or transactions. |

### Risk Mitigation

1. **Use a Trusted Operator** — Lock to General Tensor or a principal miner using the automated Cartha Rewards System to minimize distribution risk
2. **Start Small** — Lock a smaller amount first; scale up after verifying payouts work
3. **Diversify** — Spread across multiple pools and potentially multiple principal miners
4. **Monitor Regularly** — Track your position and rewards on the Principal Miners dashboard
5. **Understand LP Risk** — Your capital provides real liquidity on a DEX; liquidation events can and do happen

---

## Economics & Returns

### How Miners Earn

Miners on Cartha earn from two sources:

| Source | Details |
|--------|---------|
| **Trading Fees (50% to LPs)** | Proportional to your locked USDC; based on pool trading volume; paid in USDC (stays in vault) |
| **ALPHA Emissions (31% to miners)** | The subnet emits 7,200 ALPHA per day. Miners collectively receive 31% of that (~2,232 ALPHA/day). Your share is based on your **deposit score** (time × amount × pool weight) relative to all other miners. |

### How Your Share Is Calculated

Your deposit score determines what fraction of the daily miner emissions you receive:

- **Deposit score** = lock duration × locked amount × pool weight
- Your share = your deposit score ÷ total deposit score of all miners
- Emissions are distributed each epoch (weekly cycle: Friday 00:00 UTC → Thursday 23:59 UTC)

Since you're a federated miner, ALPHA emissions go to the **principal miner's Bittensor wallet**. You receive your share per your profit-sharing agreement with them.

> 📘 **Learn more:** See [Fees & Rewards](../how-it-works/fees-and-rewards.md) and [Weekly Epochs](../how-it-works/weekly-epochs.md) for full details on how emissions and fee distribution work.

---

## Frequently Asked Questions

**Can the principal miner steal my USDC?**
No. Your USDC is locked in a Cartha vault smart contract, not the principal miner's wallet. The principal miner cannot access, move, or withdraw your committed funds. Only you can withdraw via your EVM wallet after lock expiry.

**What if the principal miner doesn't pay me?**
If you use a principal miner on the **Cartha Rewards System** (like General Tensor), rewards are calculated automatically and you claim them directly from the dashboard — no manual payment required. For principal miners *not* on the rewards system, you rely on their agreement and reputation. This is why choosing a trusted operator matters.

**What is General Tensor?**
General Tensor is the in-house principal miner operated by the 0xMarkets team. It uses automated epoch-by-epoch distribution, has a publicly disclosed commission rate, and is the recommended starting point for new federated miners. View it at [cartha.finance/principal-miners](https://cartha.finance/principal-miners).

**What happens if the pool gets liquidated?**
Your capital is reduced by the liquidation loss. This is permanent and not reimbursed. LP risk is inherent to the system — your USDC provides real liquidity on the 0xMarkets DEX.

**Can I withdraw before my lock expires?**
No. Lock duration is enforced by smart contracts and cannot be shortened. Plan your lock period carefully.

**Can I lock to multiple principal miners?**
Yes. You can create positions with different principal miners across different pools and lock durations using separate EVM wallets.

**Is there a minimum lock amount?**
Yes, 100,000 USDC is the minimum lock amount for principal miners. Check with your specific principal miner for their minimum requirements for federated miners.

**What if the principal miner stops operating?**
Your USDC is still safe in the vault. You can withdraw after your lock expires. However, ALPHA emissions will stop if the miner de-registers from the subnet.

**How does General Tensor's commission work?**
General Tensor takes a 3% commission from your gross ALPHA rewards each epoch. The remaining 97% is yours to claim. Commission is deducted automatically — you always see your net claimable amount on the dashboard.

---

## Getting Started

> 📘 **Ready to become a federated miner?** Follow the [Federated Miner Guide](../cartha/federated-miner-guide.md) for complete step-by-step instructions on wallet setup, locking funds, and claiming rewards.

### Resources

- **[Principal Miners Guide](principal-miners.md)** — Understanding your manager
- **[Federated Miner Guide](../cartha/federated-miner-guide.md)** — Full setup, locking, and claiming walkthrough
- **[Interface Guide](../testnet/cartha-interface.md)** — How to use the Cartha interface
- **[Weekly Epochs](../how-it-works/weekly-epochs.md)** — How epoch timing and rewards work
- **[FAQ](../faq.md)** — Common questions
- **[Risk Disclosure](../legal-and-risk.md)** — Full risk information

### Support

- **Discord**: https://discord.gg/zGkW2kTsGM
- **Website**: https://cartha.finance
- **Email**: support@0xmarkets.io

---

**Disclaimer**: Federated mining involves significant risks including potential capital loss from liquidations, smart contract vulnerabilities, network failures, and reliance on principal miner distribution. General Tensor is operated by the 0xMarkets team with automated distribution, but the same LP and smart contract risks apply. Cartha provides infrastructure only and does not guarantee returns. Rewards depend on subnet performance and trading volume. Always do your own research and consult appropriate advisors before committing funds.
