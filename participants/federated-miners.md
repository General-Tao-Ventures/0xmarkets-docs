# Federated Miners

**Role:** External investors who lock capital through registered principal miners without operating Bittensor infrastructure.

**Also known as:** External Liquidity Providers, Pool Participants, Delegators

---

## Overview

Federated Miners enable anyone with USDC and an EVM wallet to participate in Cartha subnet's liquidity provision without the technical complexity of running Bittensor infrastructure. You lock capital through a registered principal miner's hotkey, maintain full ownership of your position, and can withdraw after your lock period expires.

### Key Benefits

- ✅ **No Bittensor Setup Required** - Just an EVM wallet and USDC
- ✅ **Full Capital Control** - You own your position via smart contracts
- ✅ **Direct Withdrawals** - No principal miner approval needed to withdraw
- ✅ **Choose Your Manager** - Lock to any registered principal miner
- ✅ **Flexible Lock Periods** - 1 day to 5 years

### Key Considerations

- ⚠️ **Emissions Go to Principal Miner** - You must negotiate profit-sharing terms
- ⚠️ **No Cartha Enforcement** - Distribution agreements are between you and the principal miner
- ⚠️ **LP Risk Applies** - Liquidation losses are not reimbursed
- ⚠️ **Trust Required** - Principal miner controls emission distribution

---

## Quick Start

### 1. Get USDC and ETH

**Mainnet (Base):**
- USDC: Purchase on exchanges or bridge to Base
- ETH: For gas fees (small amount needed)

**Testnet (Base Sepolia):**
- ETH Faucet: https://console.optimism.io/faucet
- USDC Faucet: https://cartha.finance/faucet

### 2. Set Up Your Wallet

Install and configure an EVM wallet:
- **MetaMask** (browser extension)
- **Coinbase Wallet** (mobile or browser)
- **WalletConnect** (mobile wallets)

Add Base network:
```
Network Name: Base
RPC URL: https://mainnet.base.org
Chain ID: 8453
Currency Symbol: ETH
Block Explorer: https://basescan.org
```

Or for testnet (Base Sepolia):
```
Network Name: Base Sepolia
RPC URL: https://sepolia.base.org
Chain ID: 84532
Currency Symbol: ETH
Block Explorer: https://sepolia.basescan.org
```

### 3. Choose a Principal Miner

Find a principal miner to lock through:

**Research:**
- Track record and reputation
- Profit-sharing terms
- Distribution frequency
- Communication channels
- Pool strategy

**Get Their Hotkey:**
- 48-character SS58 address (starts with `5`)
- Example: `5GrwvaEF5zXb26Fz9rcQpDWS57CtERHpNehXCPcNoHGKutQY`

### 4. Lock Your Funds

**Option A: Via Lock UI** ✅ **Recommended**

Visit: https://cartha.finance/create-lock

1. Connect your EVM wallet
2. Enter principal miner's hotkey
3. Select pool (BTCUSD, ETHUSD, EURUSD)
4. Enter amount (minimum 100,000 USDC)
5. Set lock duration (1-1825 days)
6. Approve USDC spending
7. Complete lock transaction

**Option B: Via Shared URL**

If the principal miner provides a lock URL:
1. Click the URL (format: `https://cartha.finance/lock?phase=1&...`)
2. Connect your wallet
3. Verify the parameters match your agreement
4. Complete Phase 1: Approve USDC
5. Complete Phase 2: Lock position

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
│     - Receives all TAO emissions            │
│     - Distributes to you per agreement      │
└─────────────────────────────────────────────┘
                    ↓
         Performance scoring
                    ↓
┌─────────────────────────────────────────────┐
│     Cartha Subnet Validators                │
│     - Score principal miner performance     │
│     - Distribute TAO emissions              │
└─────────────────────────────────────────────┘
```

### Smart Contract Protection

Your position is secured on-chain:

**What You Control:**
- Position ownership (via your EVM wallet)
- Principal withdrawal after expiry
- No principal miner approval needed to withdraw

**What You Don't Control:**
- TAO emissions (go to principal miner's Bittensor wallet)
- Pool performance (managed by principal miner)
- Liquidation events (market-driven)

---

## Understanding the Agreement

### What to Negotiate

Before locking, establish clear terms with the principal miner:

**Profit Split:**
- What percentage of TAO emissions do you receive?
- Is it pro-rata based on capital contribution?
- Are there any performance fees?

**Distribution:**
- How often will you receive distributions?
- What's the distribution method? (TAO transfer, stablecoin, etc.)
- Minimum distribution threshold?

**Lock Terms:**
- Preferred pool selection (BTCUSD, ETHUSD, etc.)
- Lock duration (longer = higher subnet score)
- Renewal terms after expiry

**Communication:**
- How will the principal miner report performance?
- What's the contact method? (Discord, Telegram, email)
- Response time expectations?

### Sample Agreement Template

```markdown
# Federated Miner Agreement

## Parties
- Principal Miner: [Name/Entity]
- Principal Miner Hotkey: 5G...
- Federated Miner: [Your Name/Address]
- Federated Miner EVM: 0x...

## Terms
- Lock Amount: 200,000 USDC
- Pool: BTCUSD
- Lock Duration: 180 days
- Expiry Date: [Auto-calculated]

## Profit Split
- Federated Miner: 75% of TAO emissions
- Principal Miner: 25% management fee

## Distribution
- Frequency: Monthly
- Method: TAO transfer to Bittensor wallet [address]
- Timing: Within 7 days of principal miner receiving emissions

## Risks Acknowledged
- LP liquidation may result in capital loss
- Emissions not guaranteed
- Principal miner does NOT control market conditions
- Smart contract risks apply

## Principal Protection
- You can withdraw USDC principal after lock expiry
- No principal miner approval required
- Withdrawal is your right via smart contract

## Signatures
- Principal Miner: _______________
- Federated Miner: _______________
- Date: _______________
```

---

## Managing Your Position

### Viewing Your Positions

**Via Lock UI:**
1. Visit https://cartha.finance/manage
2. Connect your EVM wallet
3. View all positions, amounts, and expiry dates

**Via Block Explorer:**
1. Visit https://basescan.org (or https://sepolia.basescan.org for testnet)
2. Enter your wallet address
3. View vault contract interactions

### Position Actions

**Top-Up (Add More USDC):**
- Visit https://cartha.finance/manage
- Click "Top Up" on your position
- Add more USDC to increase your share
- No approval from principal miner needed

**Extend Lock:**
- Visit https://cartha.finance/manage
- Click "Extend" on your position
- Extend lock duration for higher subnet score
- Improves your emission share

**Withdraw After Expiry:**
- Wait for lock period to end
- Visit https://cartha.finance/manage
- Click "Withdraw" on expired position
- Receive your principal back (minus any liquidation losses)

---

## Risks & Protections

### What You're Protected From

✅ **Principal Theft**
- Your USDC is in a smart contract, not the principal miner's wallet
- Principal miner cannot withdraw your funds
- You control withdrawal via your EVM wallet

✅ **Forced Lock Extension**
- Principal miner cannot extend your lock
- Position automatically expires per your chosen duration

✅ **Arbitrary Terms Changes**
- Original lock terms are immutable on-chain
- Any changes require a new lock position

### What You're NOT Protected From

⚠️ **Emission Non-Payment**
- If principal miner doesn't distribute TAO, Cartha doesn't enforce it
- You must rely on legal agreements or reputation

⚠️ **Liquidation Losses**
- LP positions can be liquidated in volatile markets
- Capital loss is permanent (not reimbursed)
- This is inherent to liquidity provision

⚠️ **Poor Performance**
- Principal miner's pool strategy may underperform
- Low trading volume = lower fee earnings
- Bad subnet score = lower emissions

⚠️ **Smart Contract Risks**
- Bugs in vault contracts (unlikely but possible)
- EVM chain risks (Base network downtime, reorgs)

### Risk Mitigation Strategies

**1. Start Small**
- Lock minimum amount first (100k USDC)
- Test the principal miner's distribution
- Scale up after successful payouts

**2. Diversify**
- Don't lock 100% with one principal miner
- Use multiple managers with different strategies
- Split across different pools

**3. Due Diligence**
- Research principal miner's history
- Check their communication and transparency
- Ask for references from other federated miners
- Verify their Bittensor wallet address

**4. Legal Protection**
- Use written agreements
- Consider escrow services for large amounts
- Know your jurisdiction's investor protections

**5. Monitor Regularly**
- Track your position via Lock UI
- Monitor principal miner's performance
- Watch for liquidation events
- Stay informed about pool health

---

## Economics & Returns

### Return Components

**1. Trading Fees (60% to LPs)**
- Proportional to your locked USDC
- Based on pool trading volume
- Paid continuously in USDC (stays in vault)

**2. TAO Emissions**
- Based on total pool capital (you + others under same hotkey)
- Based on lock duration
- Based on principal miner's subnet score
- **Paid to principal miner's Bittensor wallet**
- You receive your share per agreement

### Expected Returns

*These are estimates - actual returns vary*

**Conservative Scenario:**
- 100,000 USDC for 6 months
- Moderate pool activity
- 70% profit share with principal miner
- Estimated: 5-10% APY

**Moderate Scenario:**
- 250,000 USDC for 1 year
- Active pool with good principal miner
- 75% profit share
- Estimated: 10-20% APY

**Optimistic Scenario:**
- 500,000+ USDC for 2 years
- Top-performing principal miner
- 80% profit share
- Estimated: 20-35% APY

**Risk Scenario:**
- Liquidation event: -10% to -50% capital loss
- Poor principal miner: Delayed/no distributions
- Low activity pool: <5% APY

### Example Payout Calculation

**Your Position:**
- 200,000 USDC locked
- 12-month lock period
- BTCUSD pool

**Principal Miner's Pool:**
- Your capital: 200,000 USDC
- Other federated miners: 600,000 USDC
- Principal's own capital: 200,000 USDC
- **Total: 1,000,000 USDC**

**Annual Emissions: 100,000 TAO**

**Profit Split (75% to federated miners, 25% to principal):**
- Total to federated miners: 75,000 TAO
- Your share (20% of pool): 15,000 TAO
- Principal miner's management fee: 25,000 TAO

**Trading Fees (Separate):**
- Pool earns 50,000 USDC in fees
- Your share (20%): 10,000 USDC

**Total Returns:**
- 15,000 TAO (distributed by principal miner)
- 10,000 USDC (in vault, claimed at withdrawal)
- **Estimated APY: ~20-30%** (depends on TAO price)

---

## Finding Principal Miners

### Where to Look

**Community Channels:**
- Discord: https://discord.gg/7DXG57B6
- Telegram groups
- Twitter/X announcements

**Leaderboard:**
- Visit https://cartha.finance/leaderboard
- View top-performing miners
- Check their total locked capital
- Reach out to discuss terms

**Direct Outreach:**
- Post in community channels
- Specify your capital amount and lock duration
- Compare offers from multiple principal miners

### Red Flags

⛔ **Avoid Principal Miners Who:**
- Promise guaranteed returns
- Request capital outside of Cartha vaults
- Refuse to provide written agreements
- Don't disclose their Bittensor wallet address
- Have no track record or references
- Pressure you to lock immediately
- Offer terms that seem too good to be true

### Green Flags

✅ **Look for Principal Miners Who:**
- Provide transparent performance reporting
- Have satisfied federated miners (references)
- Use clear written agreements
- Respond promptly to questions
- Disclose all risks upfront
- Have consistent distribution history
- Maintain active communication channels

---

## Withdrawing Your Principal

### When Can You Withdraw?

After your lock period expires:
1. Visit https://cartha.finance/manage
2. Connect your EVM wallet
3. Find your expired position
4. Click "Withdraw"
5. Confirm transaction in your wallet

### What You Receive

**Principal USDC:**
- Original lock amount
- Minus any liquidation losses
- Plus trading fees earned (if not distributed)

**TAO Emissions:**
- Already distributed by principal miner
- Not included in withdrawal (received separately)

### Re-Locking

After withdrawal, you can:
- Lock again with the same principal miner
- Switch to a different principal miner
- Exit entirely

**Tips for Re-Locking:**
- Negotiate improved terms based on track record
- Consider different pools for diversification
- Adjust lock duration based on market outlook

---

## Frequently Asked Questions

### Can the principal miner steal my USDC?

No. Your USDC is locked in a Cartha vault smart contract, not the principal miner's wallet. Only you can withdraw via your EVM wallet after lock expiry.

### What if the principal miner doesn't pay me?

Cartha doesn't enforce profit-sharing agreements. You must rely on legal agreements, reputation, or escrow. This is why due diligence is critical.

### What happens if the pool gets liquidated?

Your capital is reduced by the liquidation loss. This is permanent and not reimbursed. LP risk is inherent to the system.

### Can I withdraw before my lock expires?

No. Lock duration is enforced by smart contracts. Plan your lock period carefully.

### How often will I receive distributions?

This depends on your agreement with the principal miner. Common schedules: weekly, monthly, or quarterly.

### What if the principal miner stops operating?

Your principal is still safe in the vault. You can withdraw after expiry. However, emissions will stop if the miner de-registers.

### Can I lock to multiple principal miners?

Yes! You can diversify across multiple principal miners with different pools and lock durations.

### Is there a minimum lock amount?

Yes, 100,000 USDC is the minimum lock amount.

### What are the gas fees?

Two transactions required:
1. Approve USDC (~$0.10-$1 in ETH)
2. Lock position (~$0.50-$5 in ETH)

Fees vary based on Base network congestion.

---

## Getting Help

### Resources

- **[Principal Miners Guide](principal-miners.md)** - Understanding your manager
- **[Lock UI Guide](../testnet/cartha-lock-ui.md)** - How to use the interface
- **[FAQ](../faq.md)** - Common questions
- **[Risk Disclosure](../legal-and-risk.md)** - Full risk information

### Support

- **Discord**: https://discord.gg/7DXG57B6
- **Website**: https://cartha.finance
- **Email**: support@0xmarkets.io

### Community

Join discussions with other federated miners:
- Share experiences
- Compare principal miner terms
- Get recommendations
- Report issues

---

## Next Steps

1. **Research**: Learn about LP risks and Cartha mechanics
2. **Find Principal Miners**: Compare options and terms
3. **Start Small**: Lock minimum amount first
4. **Monitor**: Track performance and distributions
5. **Scale**: Increase capital after successful payouts

---

**Disclaimer**: Federated mining involves significant risks including potential capital loss from liquidations and reliance on principal miner distribution. Cartha provides infrastructure only and does not guarantee returns, enforce agreements, or assume responsibility for principal miner actions. Always do your own research and consult appropriate advisors.
