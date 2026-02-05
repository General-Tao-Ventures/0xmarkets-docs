# Fees & rewards

* **Trading fees → 50% to miners (LPs)**.&#x20;
* **10% of trading fees → protocol treasury** (+ optional share of funding payments).&#x20;
* **ALPHA emissions**: paid via vaults based on a **deposit score** (time × amount).&#x20;

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
