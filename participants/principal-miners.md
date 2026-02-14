# Principal Miners

**Role:** Registered Bittensor miners who provide liquidity and can optionally accept external capital, acting as investment managers for federated liquidity providers.

**Also known as:** Investment Managers, Pool Operators, Delegated Miners

---

## Overview

Principal Miners are the bridge between Bittensor mining and external capital markets. They maintain registered hotkeys on the Cartha subnet (SN35) and lock USDC into market vaults to provide liquidity for [0xMarkets](https://0xmarkets.io), a decentralized perpetual futures exchange built by the same team behind Cartha. Optionally, they can accept capital from external investors (federated miners) to pool liquidity and scale their operations.

### General Tensor — The In-House Principal Miner

The 0xMarkets team operates **General Tensor**, a principal miner available to all federated miners. General Tensor is designed to be the default trusted option for participants who want to start earning without vetting third-party operators.

| Detail | Info |
|--------|------|
| **Operator** | 0xMarkets team |
| **Commission** | 3% of ALPHA emissions |
| **Distribution** | Automated epoch-by-epoch via the Cartha rewards system |
| **Trusted Status** | Yes — operated by the team that built the subnet and the exchange |
| **Dashboard** | [cartha.finance/principal-miners](https://cartha.finance/principal-miners) |

> General Tensor is a good starting point, but you are free to lock to any registered principal miner. Always review terms before committing.

### Two Operating Modes

**1. Private Mode (Solo Mining)**
- Lock only your own capital
- Manage your own USDC positions
- Receive 100% of your earned emissions directly

**2. Public Mode (Investment Manager)**
- Accept capital from external investors (federated miners)
- Pool multiple capital sources under your hotkey
- Manage investment strategy and pool selection
- Set a commission rate for your services
- Receive all emissions and distribute to federated miners per agreement

---

## Requirements

### Technical

- Registered **Bittensor hotkey** on Cartha subnet (SN35)
- Sufficient **TAO** for registration fees
- **EVM wallet** (MetaMask, Coinbase Wallet, etc.)
- **USDC** for liquidity positions
- **Base ETH** for gas fees

### Operational

- Understanding of liquidity provision risks
- Secure wallet management practices
- Ability to monitor positions and pool performance
- (Optional) Business structure for accepting external capital

---

## Becoming a Principal Miner

Becoming a principal miner involves three main steps:

1. **Create a Bittensor wallet** (coldkey + hotkey)
2. **Register your hotkey** to the Cartha subnet (SN35)
3. **Lock USDC funds** to provide liquidity via the web interface

> 📘 **Step-by-step instructions:** See the [Miner Guide](../cartha/miner-guide.md) for a complete walkthrough covering wallet creation, subnet registration, and locking funds with screenshots.

---

## Emission Distribution

### How Emissions Flow

```
Cartha Subnet Validators
         ↓
    Score miners based on performance
         ↓
ALPHA Emissions
         ↓
YOUR Bittensor Wallet (Principal Miner)
         ↓
    Distribute to federated miners (minus commission)
         ↓
Federated Miners' Bittensor Wallets
```

### Key Points

- All ALPHA emissions are initially received by **your** Bittensor wallet
- **This is the core trust assumption:** federated miners rely on you to distribute their share
- You are responsible for distributing to federated miners (if operating in public mode)
- Cartha does **not** enforce profit-sharing agreements on-chain
- The distribution mechanism is up to you, but the 0xMarkets team provides tooling to automate it

### Distribution Methods

| Method | Description | Best For |
|--------|-------------|----------|
| **Cartha Rewards System** | Automated epoch-by-epoch distribution via the [Principal Miner Template](https://github.com/General-Tao-Ventures/cartha-principal-miner-template) — federated miners claim directly from your dashboard | Operators who want hands-off, transparent distribution (used by General Tensor) |
| **Manual Distribution** | Track shares and send ALPHA periodically | Small operations with few federated miners |
| **Off-Chain Agreement** | Legal contract with manual accounting | Custom arrangements with specific investors |

> The 0xMarkets team strongly recommends using the automated Cartha Rewards System. Deploy the [open-source template](https://github.com/General-Tao-Ventures/cartha-principal-miner-template) and it handles epoch monitoring, reward scoring, commission deduction, and self-service claiming for your federated miners.

---

## Accepting External Capital (Public Mode)

### How Federated Miners Lock to You

Federated miners can lock capital to your hotkey through the [Cartha web interface](https://cartha.finance). They need your **Bittensor hotkey address** (SS58 format) — a 48-character string starting with `5`.

The process is fully self-service: federated miners enter your hotkey, choose a pool, set an amount and lock duration, and complete the transaction. No CLI or coordination from you is required for the lock itself.

### Smart Contract Architecture

- Each federated miner's position is **independent** and owned by their EVM wallet
- Your hotkey is linked to all positions for emission tracking
- **Federated miners cannot access your funds, and you cannot access theirs**
- Emissions flow to your Bittensor wallet based on total capital under your hotkey

### Total Locked Capital & Scoring

Your subnet score is based on the **sum of all positions** under your hotkey:
- Your own capital
- All federated miner capital
- Across all pools
- Weighted by lock duration and amount

---

## Setting Up the Automated Rewards System

If you want to run the Cartha Rewards System for your federated miners (recommended), the 0xMarkets team provides an open-source template you can deploy on any VPS or cloud provider.

### Principal Miner Template

**Repository:** [github.com/General-Tao-Ventures/cartha-principal-miner-template](https://github.com/General-Tao-Ventures/cartha-principal-miner-template)

The template is a self-contained backend that:

- **Monitors** the Bittensor chain for epoch boundaries
- **Sweeps** accumulated ALPHA from your miner hotkey to an aggregator hotkey
- **Scores** federated miner positions and distributes rewards proportionally (minus your commission)
- **Processes claims** from federated miners who want to withdraw their ALPHA

### Quick Deploy (Docker)

```bash
git clone https://github.com/General-Tao-Ventures/cartha-principal-miner-template.git
cd cartha-principal-miner-template
cp .env.example .env
# Edit .env with your hotkeys, wallet password, commission rate, etc.
docker compose up -d
```

This starts a PostgreSQL database, API server (port 8100), and epoch monitor — everything needed for automated distribution.

### Configuration

At minimum, you need to set:

| Variable | Description |
|----------|-------------|
| `MINER_HOTKEY` | Your Bittensor hotkey (SS58) |
| `MINER_COLDKEY` | Your Bittensor coldkey (SS58) |
| `AGGREGATOR_HOTKEY` | Aggregator hotkey for reward accumulation |
| `WALLET_PASSWORD` | Password to unlock your BT wallet |
| `COMMISSION_RATE` | Your commission (e.g., `0.05` for 5%) |
| `MINER_NAME` | Display name shown on the Cartha listing page |
| `MINER_DESCRIPTION` | Description shown on the listing page |

See the [template README](https://github.com/General-Tao-Ventures/cartha-principal-miner-template#configuration) for the full configuration reference.

### Get Listed on Cartha

After deploying your rewards system, apply to be listed on the [Principal Miners](https://cartha.finance/principal-miners) page so federated miners can discover you:

1. **Deploy & verify** — Make sure your API is accessible (`curl https://your-domain.com/health`)
2. **Apply** — Visit [cartha.finance/principal-miners/apply](https://cartha.finance/principal-miners/apply) and fill in your details
3. **Wait for approval** — The Cartha team reviews applications and notifies you via email
4. **Go live** — Once approved, your miner appears on the listing page and federated miners can lock capital to your hotkey

---

## Profit Sharing & Agreements

If you accept external capital, establish clear terms before federated miners lock to your hotkey.

### What to Define

| Topic | Details |
|-------|---------|
| **Commission Rate** | The percentage you take from federated miner rewards (e.g., 3–10%) |
| **Distribution Method** | Automated (Cartha Rewards System) or manual; frequency and process |
| **Minimum Investment** | Capital threshold and accepted lock durations |
| **Risk Disclosure** | LP liquidation, smart contract risks, distribution risk |

### Recommended Agreement Structure

```markdown
# Principal Miner Terms — [Your Name/Entity]

## Operator
- Principal Miner Hotkey: 5G...
- Operator: [Name/Entity]
- Contact: [Discord/Telegram/Email]

## Terms
- Commission Rate: [X]% of ALPHA emissions
- Distribution: Automated via Cartha Rewards System (epoch-by-epoch)
- Minimum Lock: [X] USDC for [X] days

## What Federated Miners Should Know
- ALPHA emissions go to the principal miner's Bittensor wallet first
- Commission is deducted; remaining rewards are claimable on the Principal Miners dashboard
- Your USDC is locked in a smart contract — the principal miner cannot access it
- You can withdraw your USDC after your lock period expires (no approval needed)

## Risks
- LP liquidation may result in capital loss (your USDC provides DEX liquidity)
- Emissions are not guaranteed (depend on subnet performance and trading volume)
- Smart contract risks apply (audited but not risk-free)
- Distribution risk: you rely on the principal miner to distribute rewards

## Withdrawal
- Federated miners can withdraw principal after lock expiry + 7-day cooldown
- No principal miner approval required
```

---

## Managing Positions

### Viewing Positions

- **Web Interface:** Visit [cartha.finance/positions](https://cartha.finance/positions) — see all positions, amounts, and expiry dates
- **CLI:** `cartha miner status --wallet-name <coldkey> --wallet-hotkey <hotkey>`

### Position Actions

| Action | Description |
|--------|-------------|
| **Top Up** | Add more USDC to an existing position |
| **Extend** | Increase lock duration for a higher subnet score |
| **Withdraw** | Claim principal after lock expiry |

> 📘 **Detailed instructions:** See the [Miner Guide](../cartha/miner-guide.md) for step-by-step position management with screenshots.

---

## Security & Best Practices

### Protecting Your Keys

- Never share your private keys — only share your **public** hotkey address (SS58)
- Use hardware wallets for large capital amounts
- Keep your Bittensor coldkey offline

### Monitoring

- Check miner status regularly via CLI or web interface
- Track emission receipts to your Bittensor wallet
- Monitor federated miner position expirations
- Watch for liquidation events in pools

### Communication (Public Mode)

- Maintain a communication channel (Discord, Telegram, email)
- Provide regular performance updates to federated miners
- Alert federated miners to upcoming expirations
- Share transparent emission reporting

### Risk Management

- Diversify across multiple pools
- Don't over-leverage with borrowed capital
- Understand liquidation triggers
- Keep emergency reserves for distributions

---

## Risks & Considerations

### Operational Risks

| Risk | Details |
|------|---------|
| **Distribution Responsibility** | If not using the automated Cartha Rewards System, you must distribute emissions manually. Failure to distribute damages your reputation and may cause federated miners to leave. |
| **Performance Risk** | Poor pool performance or liquidation events reduce emissions. Federated miners bear the LP risk on their capital, but poor results reflect on you as the operator. |
| **Regulatory Risk** | Accepting external capital may trigger securities regulations depending on your jurisdiction. Consult legal counsel. |

### Technical Risks

| Risk | Details |
|------|---------|
| **Smart Contract Risk** | Vault contracts are audited but not risk-free. Bugs or exploits could result in loss of locked funds. |
| **Liquidation Risk** | LP positions can be liquidated during volatile markets. Capital loss from liquidation is permanent and not reimbursed. |
| **Network Risk** | Bittensor network issues or Base chain downtime could delay emissions or transactions. |

---

## Economics & Returns

### How Principal Miners Earn

| Source | Details |
|--------|---------|
| **Trading Fees (50% to LPs)** | Distributed proportionally to all LPs based on pool deposits; paid in USDC |
| **ALPHA Emissions (31% to miners)** | The subnet emits 7,200 ALPHA per day. Miners collectively receive 31% of that (~2,232 ALPHA/day). Your share is based on your **deposit score** (time × amount × pool weight) relative to all other miners. |

### How Your Share Is Calculated

Your deposit score determines what fraction of the daily miner emissions you receive:

- **Deposit score** = lock duration × locked amount × pool weight
- Your share = your deposit score ÷ total deposit score of all miners
- Emissions are distributed each epoch (weekly cycle: Friday 00:00 UTC → Thursday 23:59 UTC)
- Your score includes **all capital** under your hotkey (your own + federated miners')

### Public Mode: The Benefit of Scale

In public mode, your hotkey's deposit score includes all federated miner capital locked to you. This means more total capital = larger share of the daily ~2,232 ALPHA miner emissions. You then distribute a portion to your federated miners per your agreement and keep the rest as a management fee — giving you leverage on capital you didn't provide yourself.

> 📘 **Learn more:** See [Fees & Rewards](../how-it-works/fees-and-rewards.md) and [Weekly Epochs](../how-it-works/weekly-epochs.md) for full details on how emissions and fee distribution work.

---

## Getting Started

> 📘 **Ready to become a principal miner?** Follow the [Miner Guide](../cartha/miner-guide.md) for complete step-by-step instructions on wallet creation, subnet registration, and locking funds.

> 🛠️ **Want to run automated rewards?** Deploy the [Principal Miner Template](https://github.com/General-Tao-Ventures/cartha-principal-miner-template) and [apply to be listed](https://cartha.finance/principal-miners/apply) on the Cartha frontend.

> 💡 **Want to lock to the in-house principal miner instead?** Visit the [General Tensor dashboard](https://cartha.finance/principal-miners) to federate under the team-operated miner, or see the [Federated Miner Guide](../cartha/federated-miner-guide.md) for a full walkthrough.

### Resources

- **[Principal Miner Template](https://github.com/General-Tao-Ventures/cartha-principal-miner-template)** — Open-source backend for automated reward distribution
- **[Miner Guide](../cartha/miner-guide.md)** — Full setup and registration walkthrough
- **[Federated Miners Guide](federated-miners.md)** — How external investors participate
- **[Federated Miner Guide (Step-by-Step)](../cartha/federated-miner-guide.md)** — Complete walkthrough with screenshots
- **[Cartha CLI](https://github.com/General-Tao-Ventures/cartha-cli)** — Command reference
- **[Weekly Epochs](../how-it-works/weekly-epochs.md)** — How epoch timing and rewards work
- **[FAQ](../faq.md)** — Common questions

### Support

- **Discord**: https://discord.gg/zGkW2kTsGM
- **Website**: https://cartha.finance
- **Email**: support@0xmarkets.io

---

**Disclaimer**: Principal miners are independent operators. Cartha provides the infrastructure but does not guarantee returns, enforce profit-sharing agreements, or assume responsibility for principal miner actions. General Tensor is operated by the 0xMarkets team and uses the automated rewards system, but the same risks (smart contract, liquidation, network) apply to all participants. Always conduct your own due diligence and consult appropriate advisors.
