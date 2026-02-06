# Fees & rewards

## Trading Fees Distribution

* **50% → Miners (LPs)**: Distributed to liquidity providers based on their vault deposits
* **40% → veALPHA stakers**: Pro-rata distribution based on veALPHA balance
* **10% → Protocol treasury** (+ optional share of funding payments)

## ALPHA Emission Distribution

ALPHA emissions are distributed across participants each epoch:

* **31% → Miners (LPs)**: Allocated via vaults based on **deposit score** (time × amount × pool weight)
* **41% → Validators**: Rewards for liquidation execution and subnet maintenance
* **10% → Traders & IBs**: Weekly leaderboard rewards and introducing broker rebates
* **18% → Owner emissions**: Protocol development and operations

### Trader Rewards

Traders on 0xMarkets earn **10% of total ALPHA emissions** through:

* **Weekly leaderboards**: Trade volume and activity earn points converted to ALPHA rewards
* **IB (Introducing Broker) rebates**: Earn rewards for referred trading volume
* **Leaderboard tracking**: View accumulated rewards at [cartha.finance/leaderboard](https://cartha.finance/leaderboard)

Trader rewards are swept to trader wallets via the liquidity flow controller.

## Lock Expiration & Withdrawals

### Expired Positions

When a lock position expires:

* **Rewards stop automatically**: Validators detect expired positions daily and stop distributing rewards
* **Funds remain in vault**: Your funds stay in the vault earning trading fees
* **Manual withdrawal required**: You must withdraw via the UI when ready

### Withdrawal Requirements

To withdraw an expired position, **both** conditions must be met:

1. **Lock period expired**: Your chosen lock duration (e.g., 3, 7, 30 days) has passed
2. **Cooldown period passed**: A mandatory 7-day cooldown from the initial lock start

**Example Timeline:**
- Lock 3 days starting Dec 11
- Lock expires: Dec 14 (rewards stop)
- Cooldown ends: Dec 18 (7 days from Dec 11)
- Can withdraw: Dec 18 or later

**Note**: The 7-day cooldown starts from lock creation, not from lock expiry. This prevents short-term lock gaming.

### Deregistered Miners

If you deregister from the subnet:
* **Automatic eviction**: Your position is automatically evicted within ~72 minutes
* **Funds returned**: Your funds are automatically returned to your wallet
* **No manual action needed**: The verifier handles this automatically
