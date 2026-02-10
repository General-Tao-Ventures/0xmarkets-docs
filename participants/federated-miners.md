# Federated Miners

**Role:** External investors who lock capital through registered principal miners without operating Bittensor infrastructure.

**Also known as:** External Liquidity Providers, Pool Participants, Delegators

---

## Overview

Federated Miners enable anyone with USDC and an EVM wallet to participate in Cartha subnet's liquidity provision without the technical complexity of running Bittensor infrastructure. You lock capital through a registered principal miner's hotkey, maintain full ownership of your position, and can withdraw after your lock period expires.

### Key Benefits

- **No Bittensor Setup Required** — Just an EVM wallet and USDC
- **Full Capital Control** — You own your position via smart contracts
- **Direct Withdrawals** — No principal miner approval needed to withdraw
- **Choose Your Manager** — Lock to any registered principal miner
- **Flexible Lock Periods** — 1 day to 5 years
- **No CLI Required** — Everything can be done through the web interface

### Key Considerations

- **Emissions Go to Principal Miner** — ALPHA emissions are sent to the principal miner's Bittensor wallet, not your EVM wallet
- **Profit-Sharing Agreement** — Establish distribution terms with the principal miner separately
- **Your Funds Stay Yours** — Principal miner cannot access your capital; you maintain full control
- **LP Risk Applies** — Liquidation losses from providing DEX liquidity may occur

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

> 📘 **Step-by-step instructions:** See the [Miner Guide](../cartha/miner-guide.md) for a complete walkthrough on setting up your wallet, obtaining tokens, and locking funds via the web interface. Federated miners can skip straight to the wallet setup and lock steps — no subnet registration needed.

---

## Choosing a Principal Miner

### What to Research

Before locking, evaluate potential principal miners on:

- **Track record and reputation** — Past performance and distribution history
- **Profit-sharing terms** — Percentage split, fees, distribution frequency
- **Communication** — Active channels (Discord, Telegram, email) and responsiveness
- **Pool strategy** — Which markets they operate in and why

### Where to Find Principal Miners

- **Leaderboard:** Visit [cartha.finance/leaderboard](https://cartha.finance/leaderboard) to view top-performing miners
- **Community:** [Discord](https://discord.gg/7DXG57B6) and Telegram groups
- **Direct Outreach:** Post your capital amount and preferred lock duration in community channels

### Red Flags

Avoid principal miners who:
- Promise guaranteed returns
- Request capital outside of Cartha vaults
- Refuse to provide written agreements
- Don't disclose their Bittensor wallet address
- Have no track record or references

### Green Flags

Look for principal miners who:
- Provide transparent performance reporting
- Have satisfied federated miners as references
- Use clear written agreements
- Disclose all risks upfront
- Maintain consistent distribution history

---

## Understanding the Agreement

Since ALPHA emissions go to the principal miner's wallet, you need a clear arrangement for profit sharing. Cartha does **not** enforce these agreements — they are between you and the principal miner.

### What to Negotiate

| Topic | Details |
|-------|---------|
| **Profit Split** | Percentage of emissions you receive, whether it's pro-rata, any performance fees |
| **Distribution Schedule** | Weekly, monthly, or quarterly; minimum thresholds; method (TAO transfer, stablecoin, etc.) |
| **Lock Terms** | Preferred pool, lock duration, renewal terms |
| **Communication** | Reporting frequency, contact method, response expectations |

### Sample Agreement Template

```markdown
# Federated Miner Agreement

## Parties
- Principal Miner: [Name/Entity]
- Principal Miner Hotkey: 5G...
- Federated Miner: [Your Name/Address]
- Federated Miner EVM: 0x...

## Terms
- Lock Amount: [X] USDC
- Pool: [BTCUSD / ETHUSD / etc.]
- Lock Duration: [X] days

## Profit Split
- Federated Miner: [X]% of ALPHA emissions
- Principal Miner: [X]% management fee

## Distribution
- Frequency: [Monthly / Weekly / etc.]
- Method: TAO transfer to [wallet address]

## Risks Acknowledged
- LP liquidation may result in capital loss
- Emissions not guaranteed
- Smart contract risks apply

## Principal Protection
- Federated miner can withdraw USDC after lock expiry
- No principal miner approval required
```

---

## Managing Your Position

Once locked, you can manage your position through the [Cartha web interface](https://cartha.finance):

- **View Positions** — See all your active locks, amounts, and expiry dates
- **Top Up** — Add more USDC to an existing position (no principal miner approval needed)
- **Extend Lock** — Increase lock duration for a higher subnet score and better emissions
- **Withdraw** — Claim your principal after lock expiry (minus any liquidation losses)

> 📘 **Detailed instructions:** See the [Miner Guide](../cartha/miner-guide.md) for step-by-step position management with screenshots.

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
| **Emission Non-Payment** | If the principal miner doesn't distribute, Cartha doesn't enforce it |
| **Liquidation Losses** | LP positions can be liquidated in volatile markets; capital loss is permanent |
| **Poor Performance** | Low trading volume or bad subnet score reduces returns |
| **Smart Contract Risks** | Potential bugs in vault contracts or Base network issues |

### Risk Mitigation

1. **Start Small** — Lock the minimum amount first; scale up after successful payouts
2. **Diversify** — Spread across multiple principal miners and pools
3. **Due Diligence** — Research history, check references, verify wallet addresses
4. **Legal Protection** — Use written agreements; consider escrow for large amounts
5. **Monitor Regularly** — Track your position and the principal miner's performance

---

## Economics & Returns

### Return Components

| Source | How It Works |
|--------|-------------|
| **Trading Fees (50% to LPs)** | Proportional to your locked USDC; based on pool trading volume; paid in USDC (stays in vault) |
| **ALPHA Emissions** | Based on total pool capital, lock duration, and principal miner's subnet score; paid to principal miner's wallet; you receive your share per agreement |

### Return Estimates

*These are estimates — actual returns vary based on market conditions and principal miner performance.*

| Scenario | Capital | Duration | Estimated APY |
|----------|---------|----------|---------------|
| Conservative | 100,000 USDC | 6 months | 5–10% |
| Moderate | 250,000 USDC | 1 year | 10–20% |
| Optimistic | 500,000+ USDC | 2 years | 20–35% |
| Risk (liquidation) | Any | Any | -10% to -50% capital loss |

---

## Frequently Asked Questions

**Can the principal miner steal my USDC?**
No. Your USDC is locked in a Cartha vault smart contract, not the principal miner's wallet. Only you can withdraw via your EVM wallet after lock expiry.

**What if the principal miner doesn't pay me?**
Cartha doesn't enforce profit-sharing agreements. You must rely on legal agreements, reputation, or escrow. This is why due diligence is critical.

**What happens if the pool gets liquidated?**
Your capital is reduced by the liquidation loss. This is permanent and not reimbursed. LP risk is inherent to the system.

**Can I withdraw before my lock expires?**
No. Lock duration is enforced by smart contracts. Plan your lock period carefully.

**Can I lock to multiple principal miners?**
Yes. You can diversify across multiple principal miners with different pools and lock durations.

**Is there a minimum lock amount?**
Yes, 100,000 USDC is the minimum lock amount.

**What if the principal miner stops operating?**
Your principal is still safe in the vault. You can withdraw after expiry. However, emissions will stop if the miner de-registers.

---

## Getting Started

> 📘 **Ready to become a federated miner?** Follow the [Miner Guide](../cartha/miner-guide.md) for complete step-by-step instructions on wallet setup, obtaining tokens, and locking funds.

### Resources

- **[Principal Miners Guide](principal-miners.md)** — Understanding your manager
- **[Miner Guide](../cartha/miner-guide.md)** — Full setup and locking walkthrough
- **[Interface Guide](../testnet/cartha-interface.md)** — How to use the Cartha interface
- **[Weekly Epochs](../how-it-works/weekly-epochs.md)** — How epoch timing and rewards work
- **[FAQ](../faq.md)** — Common questions
- **[Risk Disclosure](../legal-and-risk.md)** — Full risk information

### Support

- **Discord**: https://discord.gg/7DXG57B6
- **Website**: https://cartha.finance
- **Email**: support@0xmarkets.io

---

**Disclaimer**: Federated mining involves significant risks including potential capital loss from liquidations and reliance on principal miner distribution. Cartha provides infrastructure only and does not guarantee returns, enforce agreements, or assume responsibility for principal miner actions. Always do your own research and consult appropriate advisors.
