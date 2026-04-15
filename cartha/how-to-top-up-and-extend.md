# How to Top Up & Extend Your Lock

Grow your position and improve your deposit score without starting from scratch — top up to add more USDC or extend your lock duration on any active position.

- **Web Interface**: [liquidity.0xmarkets.io/manage](https://liquidity.0xmarkets.io/manage)

---

## Prerequisites

Before you can top up or extend, you'll need:

- ✅ **An active lock position** — visible on the [My Positions](https://liquidity.0xmarkets.io/manage) page
- ✅ **EVM wallet connected** — the same wallet used to create the lock
- ✅ **Base Mainnet** selected in your wallet (Chain ID: 8453)
- ✅ **ETH on Base** — for gas fees
- ✅ **USDC on Base** — required for Top Up; not needed for Extend

> If you don't have an active position yet, see the [Federated Miner Guide](federated-miner-guide.md) to create your first lock.

---

## Understanding Deposit Score

Both actions — topping up and extending — increase your **deposit score**, which directly determines your share of daily ALPHA emissions.

**Deposit score formula:**

```
score = amount_USDC × min(lock_days, 365) / 365
```

| Action | Effect on Score |
|--------|----------------|
| **Top Up** | Increases the `amount_USDC` component |
| **Extend** | Increases the `lock_days` component (capped at 365) |
| **Both** | Multiplies both components for maximum impact |

> **Best practice**: For the highest deposit score, combine a large USDC amount with the longest lock duration you're comfortable with.

---

## How to Top Up (Add More USDC)

Topping up adds additional USDC to an existing lock position. The new USDC is subject to the same lock duration as your original position.

### Step 1: Navigate to My Positions

Go to [liquidity.0xmarkets.io/manage](https://liquidity.0xmarkets.io/manage) and connect your EVM wallet if not already connected.

<figure><img src="../.gitbook/assets/miner-dashboard-position-page.png" alt="My Positions — Portfolio Summary and Position Cards"><figcaption>My Positions page showing all your active positions with quick action buttons</figcaption></figure>

You'll see all your active positions listed as cards. Each card shows:

- Pool name (e.g., BTC/USD, ETH/USD)
- Current locked amount (USDC)
- Lock duration (days remaining / total days)
- Expiration date
- Current status (Active, In Next Epoch, etc.)

### Step 2: Click "Top Up"

Find the position you want to add funds to and click the **"Top Up"** button on that position card.

> If you don't see a **Top Up** button, make sure your wallet is connected and you're on the correct network (Base Mainnet).

### Step 3: Enter the Additional Amount

A **Top Up** modal will appear showing:

- **Pool** — which pool you're topping up
- **Current locked amount** — your existing USDC balance in this position
- **Lock expiration** — when the lock expires (unchanged by top up)
- **Amount field** — enter how much additional USDC to add

Enter the amount of USDC you want to add and review the details.

> **Note**: There is no minimum top-up amount, but you must have sufficient USDC in your wallet plus ETH for gas.

### Step 4: Approve USDC (if needed)

If you haven't already approved the vault contract to spend your USDC, you'll be prompted to **Approve** first:

1. Click **"Approve"** — this authorizes the vault contract to transfer your USDC
2. Sign the approval transaction in your wallet
3. Wait for the approval transaction to confirm on-chain

This is a standard ERC-20 approval. You only need to approve once per vault, or when adding an amount that exceeds your previous approval.

### Step 5: Confirm the Top Up

After approval (or if you had a sufficient existing approval):

1. Review the final top-up summary:
   - Additional USDC amount
   - New total locked amount after top up
   - Pool and expiration date
2. Click **"Confirm Top Up"**
3. Sign the transaction in your wallet
4. Wait for the transaction to confirm — you'll see a success confirmation with a BaseScan link

### Step 6: Verify on My Positions

After the transaction confirms, return to the [My Positions](https://liquidity.0xmarkets.io/manage) page and click **Refresh**. Your position card should now reflect the updated locked amount.

> The verifier may take up to 15 minutes to index the top-up. If the amount hasn't updated after 15 minutes, check the transaction on [BaseScan](https://basescan.org).

---

## How to Extend Lock Duration

Extending increases the number of days your USDC is locked. This directly increases your deposit score, giving you a larger share of ALPHA emissions without requiring any additional USDC.

> **Important**: You can only extend to a *longer* duration — you cannot shorten an existing lock.

### Step 1: Navigate to My Positions

Go to [liquidity.0xmarkets.io/manage](https://liquidity.0xmarkets.io/manage) and connect your EVM wallet.

### Step 2: Click "Extend"

Find the position you want to extend and click the **"Extend"** button on that position card.

### Step 3: Choose a New Lock Duration

An **Extend Lock** modal will appear showing:

- **Pool** — which pool you're extending
- **Current lock duration** — your current lock days (e.g., 30 days)
- **Current expiration date** — when the lock currently expires
- **Duration selector** — choose your new total lock duration

Select a new duration that is **longer than your current remaining lock time**. Common options include 30, 60, 90, 180, and 365 days.

| Lock Duration | Effect on Score |
|--------------|----------------|
| 30 days | score × (30/365) |
| 90 days | score × (90/365) |
| 180 days | score × (180/365) |
| 365 days | score × 1.0 (maximum) |

> **Tip**: Locking for 365 days gives you the maximum possible score multiplier. Even if you can't commit to a full year, extending from 30 to 90 days triples your score per dollar.

### Step 4: Review the Extension

The modal will show:

- New lock duration (days)
- New expiration date
- Estimated impact on your deposit score
- Gas cost estimate

Review the new expiration date carefully — this is when you'll be able to withdraw your USDC (subject to the 7-day cooldown).

### Step 5: Confirm the Extension

1. Click **"Confirm Extension"**
2. Sign the transaction in your wallet
3. Wait for the transaction to confirm — you'll see a success confirmation

### Step 6: Verify on My Positions

Return to [My Positions](https://liquidity.0xmarkets.io/manage) and refresh. Your position card should now show the updated lock duration and new expiration date.

---

## Epoch Timing Considerations

Both top up and extend transactions take effect at the start of the next epoch.

- The 0xMarkets Liquidity Provider operates on a **weekly epoch cycle**: Friday 00:00 UTC → Thursday 23:59 UTC
- Complete your top up or extension before **Thursday 23:00 UTC** to be included in the upcoming epoch
- Changes made after Friday 00:00 UTC will take effect in the *following* week's epoch
- The indexer needs up to **15 minutes** to detect new transactions — give yourself a buffer

> See [Weekly Epochs](../how-it-works/weekly-epochs.md) for full details on epoch timing and scoring.

---

## Multiple Positions

If you want to create a separate position rather than modifying an existing one:

| Scenario | Result |
|----------|--------|
| Same hotkey + Same pool + **Different EVM wallet** | Creates a new, separate position |
| Same hotkey + Same pool + **Same EVM wallet** | Must use **Top Up** — the contract won't allow a duplicate |

---

## Troubleshooting

### "Top Up" or "Extend" button not visible

- Make sure your wallet is connected to the correct account (the one that owns the lock)
- Ensure you're on **Base Mainnet** (Chain ID: 8453)
- Click **Refresh** on the My Positions page
- If your position shows as **Expired**, you can no longer extend — you must withdraw first

### Approval transaction failed

- Check you have enough ETH for gas
- Try increasing the gas limit in your wallet
- Make sure you haven't already approved a higher amount for another session

### Position not updated after transaction confirms

- Wait up to 15 minutes for the verifier to index your transaction
- Click **Refresh** on the My Positions page
- If still not updated, verify the transaction succeeded on [BaseScan](https://basescan.org) using your transaction hash

### "New duration must be longer than current duration" error

- You cannot set a lock duration shorter than your current remaining lock time
- Choose a new duration that extends *beyond* the current expiration date

---

## Related Guides

- **[How to Withdraw](how-to-withdraw.md)** — Withdraw USDC after your lock expires
- **[How to Claim Rewards](claim-rewards.md)** — Claim your ALPHA earnings
- **[Federated Miner Guide](federated-miner-guide.md)** — Complete setup and deposit guide
- **[Weekly Epochs](../how-it-works/weekly-epochs.md)** — How epoch timing affects your earnings
- **[Fees & Rewards](../how-it-works/fees-and-rewards.md)** — Full breakdown of emissions and scoring
