# Principal Miners

**Role:** Registered Bittensor miners who provide liquidity and can optionally accept external capital, acting as investment managers for federated liquidity providers.

**Also known as:** Investment Managers, Pool Operators, Delegated Miners

---

## Overview

Principal Miners are the bridge between Bittensor mining and external capital markets. They maintain registered hotkeys on the Cartha subnet and lock USDC into market vaults to provide liquidity. Optionally, they can accept capital from external investors (federated miners) to pool liquidity and scale their operations.

### Two Operating Modes

**1. Private Mode (Traditional)**
- Lock only your own capital
- Manage your own USDC positions
- Receive 100% of your earned emissions directly

**2. Public Mode (Investment Manager)**
- Accept capital from external investors (federated miners)
- Pool multiple capital sources under your hotkey
- Manage investment strategy and pool selection
- Negotiate profit-sharing arrangements
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
    (You distribute to federated miners, if any)
         ↓
Federated Miners' Wallets
```

### Key Points

- All ALPHA emissions go to **your** Bittensor wallet
- You are responsible for distributing to federated miners (if operating in public mode)
- Cartha does **not** enforce profit-sharing agreements
- The distribution mechanism is entirely up to you

### Distribution Strategies

| Strategy | Description | Trade-off |
|----------|-------------|-----------|
| **Manual Distribution** | Track shares and send TAO periodically | Simple but time-intensive |
| **Smart Contract Escrow** | Custom contract to auto-split emissions | Requires development |
| **Off-Chain Agreement** | Legal contract with manual accounting | Relies on trust and legal enforcement |

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

## Profit Sharing & Agreements

If you accept external capital, establish clear terms before federated miners lock to your hotkey.

### What to Define

| Topic | Details |
|-------|---------|
| **Minimum Investment** | Capital threshold and accepted lock durations |
| **Profit Split** | Percentage to federated miners, pro-rata basis, performance fees |
| **Distribution Schedule** | Weekly, monthly, or quarterly; minimum threshold; method |
| **Risk Disclosure** | LP liquidation, impermanent loss, smart contract risks |

### Recommended Agreement Structure

```markdown
# Federated Miner Agreement — [Your Name/Entity]

## Terms
- Principal Miner Hotkey: 5G...
- Minimum Investment: 100,000 USDC
- Lock Duration: 90–365 days
- Profit Split: 70% to Federated Miner, 30% to Principal Miner
- Distribution: Monthly, within 7 days of emission receipt

## Risks
- LP liquidation may result in capital loss
- Emissions not guaranteed (depend on subnet performance)
- Smart contract risks apply

## Principal Withdrawal Protection
- Federated miners can withdraw principal after lock expiry
- No principal miner approval required

## Termination
- Federated miner can choose not to re-lock after expiry
- Principal miner cannot force withdrawal or extension
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
| **Distribution Responsibility** | You must manually distribute emissions; no automatic enforcement |
| **Performance Risk** | Poor pool performance or liquidation events reduce emissions and may cause federated miners to leave |
| **Regulatory Risk** | Accepting external capital may trigger securities regulations; consult legal counsel |

### Technical Risks

| Risk | Details |
|------|---------|
| **Smart Contract Risk** | Vault contract bugs (audited but not risk-free) |
| **Liquidation Risk** | LP positions can be liquidated; capital loss is permanent |
| **Impermanent Loss** | Inherent to liquidity provision; volatile markets increase IL |

---

## Economics & Returns

### Revenue Sources

| Source | How It Works |
|--------|-------------|
| **Trading Fees (50% to LPs)** | Distributed proportionally to all LPs; based on pool selection; paid in USDC |
| **ALPHA Emissions** | Based on total locked capital, lock duration, and subnet score; paid in TAO |

### Return Estimates

*These are estimates — actual returns vary.*

| Scenario | Capital | Duration | Estimated APY |
|----------|---------|----------|---------------|
| Baseline | 100,000 USDC | 1 year | 5–15% |
| Optimistic | 500,000+ USDC | 2+ years | 15–30%+ |
| Risk (liquidation) | Any | Any | -10% to -50% capital loss |

### Example: Public Mode Economics

| Item | Value |
|------|-------|
| Your capital | 200,000 USDC |
| Federated miner capital | 800,000 USDC |
| **Total pool** | **1,000,000 USDC** |
| Profit split | 80% to federated miners, 20% to you |

**If annual emissions = 100,000 TAO:**
- Federated miners receive: 80,000 TAO (split pro-rata)
- Your management fee: 20,000 TAO
- Your emission share on 200k capital: ~20,000 TAO
- **Your total: ~36,000 TAO** (36% of emissions with 20% of capital)

---

## Getting Started

> 📘 **Ready to become a principal miner?** Follow the [Miner Guide](../cartha/miner-guide.md) for complete step-by-step instructions on wallet creation, subnet registration, and locking funds.

### Resources

- **[Miner Guide](../cartha/miner-guide.md)** — Full setup and registration walkthrough
- **[Federated Miners Guide](federated-miners.md)** — How external investors participate
- **[Cartha CLI](https://github.com/General-Tao-Ventures/cartha-cli)** — Command reference
- **[Weekly Epochs](../how-it-works/weekly-epochs.md)** — How epoch timing and rewards work
- **[FAQ](../faq.md)** — Common questions

### Support

- **Discord**: https://discord.gg/7DXG57B6
- **Website**: https://cartha.finance
- **Email**: support@0xmarkets.io

---

**Disclaimer**: Principal miners are independent operators. Cartha provides the infrastructure but does not guarantee returns, enforce profit-sharing agreements, or assume responsibility for principal miner actions. All participants should conduct their own due diligence and consult appropriate advisors.
