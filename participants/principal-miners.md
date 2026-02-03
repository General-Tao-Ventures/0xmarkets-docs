# Principal Miners

**Role:** Registered Bittensor miners who accept external capital and act as investment managers for federated liquidity providers.

**Also known as:** Investment Managers, Pool Operators, Delegated Miners

---

## Overview

Principal Miners are the bridge between traditional Bittensor mining and external capital markets. They maintain registered hotkeys on the Cartha subnet and can optionally accept capital from external investors (federated miners) to pool liquidity and scale their operations.

### Two Operating Modes

**1. Private Mode (Traditional)**
- Lock only your own capital
- Manage your own USDC positions
- Receive emissions directly to your Bittensor wallet

**2. Public Mode (Investment Manager)**
- Accept capital from external investors (federated miners)
- Pool multiple capital sources under your hotkey
- Manage investment strategy and pool selection
- Negotiate profit-sharing arrangements
- Receive all emissions (must distribute to federated miners per agreement)

---

## Requirements

### Technical Requirements

- ✅ Registered Bittensor hotkey on Cartha subnet (SN35)
- ✅ Sufficient TAO for registration fees
- ✅ EVM wallet (MetaMask, Coinbase Wallet, etc.)
- ✅ USDC for initial liquidity position
- ✅ Base network ETH for gas fees

### Operational Requirements

- 📊 Understanding of liquidity provision risks
- 🔐 Secure wallet management practices
- 📈 Ability to monitor positions and pool performance
- 💼 (Optional) Business structure for accepting external capital

---

## How to Become a Principal Miner

### Step 1: Register on Cartha Subnet

```bash
# Install Cartha CLI
pip install cartha-cli

# Register your hotkey
cartha miner register \
  --wallet-name your-coldkey \
  --wallet-hotkey your-hotkey \
  --network finney
```

**Testnet Registration:**
```bash
cartha miner register \
  --wallet-name your-coldkey \
  --wallet-hotkey your-hotkey \
  --network test
```

### Step 2: Create Your First Position

```bash
# Interactive mode (recommended)
cartha vault lock

# Or with all parameters
cartha vault lock \
  --wallet-name your-coldkey \
  --wallet-hotkey your-hotkey \
  --pool BTCUSD \
  --amount 100000 \
  --lock-days 365 \
  --owner-evm 0xYourEVMAddress
```

**Minimum Requirements:**
- 100,000 USDC minimum lock amount
- 1-1825 days lock duration (up to 5 years)

### Step 3: Choose Your Operating Mode

**Private Mode:**
- Lock only your own capital
- No additional setup required
- Receive 100% of your earned emissions

**Public Mode (Investment Manager):**
- Share your hotkey with potential federated miners
- Negotiate profit-sharing terms
- Set up distribution mechanism
- Monitor multiple positions under your hotkey

---

## Accepting External Capital (Public Mode)

### How Federated Miners Lock to You

Federated miners can lock capital to your hotkey in two ways:

**Option 1: Via Cartha Interface** ✅ **Recommended**
1. Federated miner visits https://cartha.finance/create-lock
2. Enters your hotkey address (SS58 format)
3. Selects pool, amount, and lock duration
4. Completes the lock transaction
5. Position is created under their EVM wallet

**Option 2: Via CLI with Your Signature**
1. You generate a lock URL using the CLI
2. Share the URL with the federated miner
3. They complete the transaction in the frontend
4. Position is created under their specified EVM address

### Your Hotkey Address

Your federated miners will need your **Bittensor hotkey address** (SS58 format):
- Starts with `5` (e.g., `5GrwvaEF5zXb26Fz9rcQpDWS57CtERHpNehXCPcNoHGKutQY`)
- 48 characters long
- Found in your wallet or via: `btcli wallet list`

### Smart Contract Architecture

All positions are tracked on-chain:
- Each federated miner's position is independent
- They own their position via their EVM wallet
- Your hotkey is linked to all positions for emission tracking
- **Critical**: Emissions flow to YOUR Bittensor wallet, not theirs

---

## Emission Distribution

### How Emissions Work

```
Cartha Subnet Validators
         ↓
    Score miners based on performance
         ↓
Bittensor Emissions (TAO)
         ↓
YOUR Bittensor Wallet (Principal Miner)
         ↓
    (You must distribute to federated miners)
         ↓
Federated Miners' Wallets
```

### Important: YOU Control Distribution

- ✅ All TAO emissions go to your Bittensor wallet
- ✅ You are responsible for distributing to federated miners
- ✅ Cartha does NOT enforce profit-sharing agreements
- ✅ Distribution mechanism is entirely up to you

### Distribution Strategies

**Option 1: Manual Distribution**
- Track each federated miner's share
- Send TAO periodically from your wallet
- Simple but time-intensive

**Option 2: Smart Contract Escrow**
- Create a custom distribution contract
- Automatically split emissions based on capital contribution
- Requires development work

**Option 3: Off-Chain Agreement**
- Legal contract with federated miners
- Manual accounting and distribution
- Relies on trust and legal enforcement

---

## Managing Multiple Positions

### Position Tracking

Each position under your hotkey includes:
- Federated miner's EVM address (position owner)
- Pool selection (BTCUSD, ETHUSD, etc.)
- Lock amount and duration
- Expiration date

### Viewing All Positions

**Via CLI:**
```bash
cartha miner status \
  --wallet-name your-coldkey \
  --wallet-hotkey your-hotkey
```

**Via Frontend:**
- Visit https://cartha.finance/manage
- Connect your EVM wallet
- View all positions owned by you

**Via Verifier API:**
```bash
curl "https://cartha-verifier.run.app/v1/miner/status-by-hotkey?hotkey=5G..."
```

### Total Locked Capital

Your subnet score is based on the **sum of all positions** under your hotkey:
- Your own capital
- All federated miner capital
- Across all pools
- Weighted by lock duration and amount

---

## Profit Sharing & Agreements

### Setting Terms

Before accepting external capital, establish clear terms:

**Capital Contribution:**
- Minimum investment amount
- Maximum pool size
- Accepted lock durations

**Profit Split:**
- What percentage of emissions goes to federated miners?
- Is it pro-rata (based on capital contribution)?
- Are there any performance fees?

**Distribution Schedule:**
- Weekly, monthly, or quarterly distributions?
- Minimum distribution threshold?
- What happens to unclaimed distributions?

**Risk Disclosure:**
- LP liquidation risks
- Impermanent loss risks
- Smart contract risks
- Your own operational risks

### Recommended Agreement Structure

```markdown
# Federated Miner Agreement - [Your Name/Entity]

## Terms
- Principal Miner Hotkey: 5G...
- Minimum Investment: 100,000 USDC
- Lock Duration: 90-365 days
- Profit Split: 70% to Federated Miner, 30% to Principal Miner
- Distribution: Monthly, within 7 days of emission receipt

## Risks
- LP liquidation may result in capital loss
- Emissions not guaranteed (depend on subnet performance)
- Principal miner does not control market conditions
- Smart contract risks apply

## Principal Withdrawal Protection
- Federated miners can withdraw their principal after lock expiry
- No principal miner approval required
- Emissions belong to principal miner until distributed

## Termination
- Federated miner can choose not to re-lock after expiry
- Principal miner cannot force withdrawal or extension
- All agreements terminate upon position expiry
```

---

## Security & Best Practices

### Protecting Your Hotkey

- 🔐 Never share your private keys
- 🔐 Only share your public hotkey address (SS58)
- 🔐 Use hardware wallets for large capital amounts
- 🔐 Keep your Bittensor coldkey offline

### Monitoring Positions

- 📊 Check miner status regularly via CLI
- 📊 Track emission receipts to your Bittensor wallet
- 📊 Monitor federated miner position expirations
- 📊 Watch for liquidation events in pools

### Communication with Federated Miners

- 📢 Maintain a communication channel (Discord, Telegram, email)
- 📢 Provide regular performance updates
- 📢 Alert federated miners to upcoming expirations
- 📢 Transparent emission reporting

### Risk Management

- ⚠️ Diversify across multiple pools
- ⚠️ Don't over-leverage with borrowed capital
- ⚠️ Understand liquidation triggers
- ⚠️ Keep emergency reserves for distributions

---

## Risks & Considerations

### Operational Risks

**Emission Distribution Responsibility:**
- You must manually distribute emissions
- No automatic enforcement of agreements
- Legal/reputational risk if you don't pay

**Performance Risk:**
- Poor pool performance = lower emissions
- Liquidation events affect your subnet score
- Federated miners may not re-lock if performance is poor

**Regulatory Risk:**
- Accepting external capital may trigger securities regulations
- Consult legal counsel before operating as an investment manager
- Know your jurisdiction's requirements

### Technical Risks

**Smart Contract Risk:**
- Vault contract bugs (audited but not risk-free)
- EVM chain risks (Base network)

**Liquidation Risk:**
- LP positions can be liquidated
- Capital loss is permanent (not reimbursed by Cartha)
- Affects your score and federated miner returns

**Impermanent Loss:**
- Liquidity provision inherently has IL risk
- Volatile markets increase IL
- May offset TAO emissions

---

## Earnings & Economics

### Revenue Sources

**1. Trading Fees (60% share)**
- Distributed proportionally to all LPs
- Based on your pool selection
- Paid in USDC

**2. ALPHA Emissions**
- Based on your total locked capital
- Based on lock duration (longer = higher weight)
- Based on subnet performance score
- Paid in TAO

### Expected Returns

*Note: These are estimates and not guarantees*

**Baseline Scenario:**
- 100,000 USDC locked for 1 year
- BTCUSD pool (moderate activity)
- Estimated: 5-15% APY from fees + emissions

**Optimistic Scenario:**
- 500,000+ USDC locked for 2+ years
- Multiple pools with high trading volume
- Top-performing miner
- Estimated: 15-30%+ APY

**Risk Scenario:**
- Liquidation event: -10% to -50% capital loss
- Poor subnet score: Minimal emissions
- Low trading volume: <5% APY

### Example Economics (Federated Pool)

**Setup:**
- Principal Miner: 200,000 USDC locked
- Federated Miners: 800,000 USDC locked
- Total Pool: 1,000,000 USDC
- Profit Split: 80% to federated miners, 20% to principal miner

**Annual Emissions Received: 100,000 TAO**

**Distribution:**
- Federated Miners: 80,000 TAO (split pro-rata by capital)
- Principal Miner: 20,000 TAO (management fee)

**Principal Miner Benefits:**
- Emission share for 200k capital: ~20,000 TAO (10% of pool)
- Management fee on 800k external capital: ~16,000 TAO (2% of total emissions)
- **Total: 36,000 TAO** (36% of emissions with only 20% of capital)

---

## Getting Help

### Resources

- **[Miner Guide](testnet/miner-guide.md)** - Complete setup instructions
- **[Cartha CLI Documentation](https://github.com/General-Tao-Ventures/cartha-cli)** - Command reference
- **[Federated Miner Flow](../FEDERATED_MINER_FLOW.md)** - Technical architecture
- **[FAQ](faq.md)** - Common questions

### Community & Support

- **Discord**: https://discord.gg/7DXG57B6
- **Telegram**: [Cartha Miners Group]
- **Email**: support@0xmarkets.io

### For Federated Miners

If you're an external investor looking to lock capital through a principal miner:
- **[Federated Miners Guide](federated-miners.md)** - How to participate
- **Lock UI**: https://cartha.finance/create-lock
- **Risk Disclosure**: Always review terms with the principal miner

---

## Next Steps

1. **Get Started**: Register your hotkey and create your first position
2. **Monitor Performance**: Track your emissions and pool performance
3. **Build Reputation**: Provide consistent returns and transparent reporting
4. **Scale Capital**: Once established, consider accepting external capital
5. **Optimize Strategy**: Diversify across pools and adjust lock durations

---

**Disclaimer**: Principal miners are independent operators. Cartha provides the infrastructure but does not guarantee returns, enforce profit-sharing agreements, or assume responsibility for principal miner actions. All participants should conduct their own due diligence and consult appropriate advisors.
