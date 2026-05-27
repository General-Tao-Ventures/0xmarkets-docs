# How to Withdraw

Once your lock period has expired and the cooldown has passed, you can withdraw your USDC back to your EVM wallet.

- **Web Interface**: [liquidity.0xmarkets.io/manage](https://liquidity.0xmarkets.io/manage)

---

## Overview

Withdrawing from the 0xMarkets Liquidity Provider returns your locked USDC principal (plus any accrued vault value) to your connected EVM wallet. Withdrawal is only available after **both** conditions are met:

1. **Lock period has expired** — the duration you set when locking has fully elapsed
2. **7-day cooldown has passed** — a mandatory waiting period counted from the lock *creation* date, not the expiry date

> **Important**: The 7-day cooldown begins when you first create the lock, not when it expires. For most positions (locked for 30+ days), the cooldown has already passed by the time the lock expires.

---

## Understanding the Cooldown Period

| Lock Duration | Cooldown Status at Expiry |
|--------------|--------------------------|
| Less than 7 days | Cooldown still active at expiry — must wait for 7 days from lock creation |
| 7 days exactly | Cooldown completes exactly at expiry |
| More than 7 days | Cooldown already passed before expiry — withdraw immediately at expiry |

For example, if you lock for 30 days on January 1:

- **Cooldown ends**: January 8 (7 days after lock creation)
- **Lock expires**: January 31 (30 days after lock creation)
- **Withdraw available**: January 31 (lock expiry is the binding constraint here)

If you lock for 3 days on January 1:

- **Lock expires**: January 4
- **Cooldown ends**: January 8
- **Withdraw available**: January 8 (cooldown is the binding constraint here)

> See [Fees & Rewards](../how-it-works/fees-and-rewards.md) for full details on how the cooldown period works.

---

## Prerequisites

Before withdrawing, confirm:

- ✅ **Lock period has expired** — position shows **"Expired"** status on My Positions
- ✅ **Cooldown has passed** — the Withdraw modal will confirm "Ready" status
- ✅ **EVM wallet connected** — the exact wallet that owns the lock position
- ✅ **Base Mainnet selected** — Chain ID: 8453
- ✅ **ETH in wallet** — a small amount needed for gas fees

---

## Step-by-Step: How to Withdraw

### Step 1: Navigate to My Positions

Go to [liquidity.0xmarkets.io/manage](https://liquidity.0xmarkets.io/manage) and connect your EVM wallet.

<figure><img src="../.gitbook/assets/miner-dashboard-position-page.png" alt="My Positions — Portfolio Summary and Position Cards"><figcaption>My Positions page — active positions show Top Up and Extend buttons; expired positions show the Withdraw button</figcaption></figure>

### Step 2: Locate Your Expired Position

Find the position you want to withdraw from. Expired positions are identified by:

- **Status badge**: Shows **"Expired"** in a distinct color (no longer "Active" or "In Next Epoch")
- **Expiration date**: Shown as a past date
- **Available actions**: A **"Withdraw"** button appears below the Extend and Top Up buttons

<figure><img src="../.gitbook/assets/what-expired-look-like.png" alt="Expired Position with Withdraw Button"><figcaption>An expired position showing the Withdraw button and Expired status badge</figcaption></figure>

> If the position shows as **Active** or **In Next Epoch**, your lock has not yet expired. You cannot withdraw until the lock duration and cooldown have both fully elapsed.

### Step 3: Click "Withdraw"

Click the **"Withdraw"** button on the expired position card. A **Confirm Withdrawal** modal will appear.

### Step 4: Review the Withdrawal Details

<figure><img src="../.gitbook/assets/withdraw-popup.png" alt="Confirm Withdrawal Popup"><figcaption>The withdrawal confirmation modal showing all position details and the amount you will receive</figcaption></figure>

The modal displays all the information you need to verify before proceeding:

| Field | Description |
|-------|-------------|
| **Pool** | The pool your USDC was locked in (e.g., BTC/USD) |
| **Lock Duration** | Original lock duration you selected |
| **Expiration Date** | When the lock expired |
| **Status** | Must show **"Expired"** to proceed |
| **Total Committed** | The total USDC you originally locked |
| **Amount to Receive** | The USDC you will get back (principal ± vault performance) |
| **Cooldown Status** | Must show **"Ready"** — if it shows a date, you must wait |
| **Position Owner** | The EVM address that owns this lock |
| **Connected Wallet** | Your currently connected wallet |

> **Wallet match check**: The modal will visually confirm that your connected wallet matches the position owner address. If they don't match, disconnect your wallet and reconnect with the correct one.

### Step 5: Confirm the Cooldown is "Ready"

In the modal, check the **Cooldown** field:

- ✅ **"Ready"** — you can proceed with withdrawal immediately
- ⏳ **Shows a future date** — you must wait until that date before withdrawing. Close the modal and come back later.

### Step 6: Execute the Withdrawal

Once you've reviewed all details and confirmed the cooldown is Ready:

1. Click **"Confirm Full Withdrawal"**
2. Your wallet will prompt you to sign and submit the withdrawal transaction
3. Review the transaction in your wallet (check the gas fee) and confirm
4. Wait for the transaction to be confirmed on-chain

You'll see a **success confirmation** screen with:

- Withdrawn amount
- Destination EVM address
- Transaction hash with a link to BaseScan

### Step 7: Verify Your Balance

After the transaction confirms:

1. Check your EVM wallet balance — the USDC should appear within a few minutes
2. Return to [My Positions](https://liquidity.0xmarkets.io/manage) and refresh — the withdrawn position will no longer appear

---

## What Happens to Your USDC?

When you withdraw:

- **Principal returned**: Your locked USDC is returned in full, assuming no liquidation events
- **Vault performance**: If the vault gained value (from trading fees), you may receive slightly more than you locked. If there were losses, you may receive slightly less.
- **Gas fees**: A small amount of ETH is spent on the withdrawal transaction — this is not deducted from your USDC
- **ALPHA rewards**: Unclaimed ALPHA earnings are **not** affected by withdrawal. You can still claim them after withdrawing your principal.

> The 0xMarkets liquidity vaults provide real DEX liquidity. LP positions can experience losses in volatile markets. See [Safety & Liquidations](../how-it-works/safety-and-liquidations.md) for details.

---

## After Withdrawing

Once you've withdrawn:

### Your ALPHA Rewards Are Still Available

Withdrawing your USDC does **not** forfeit any accumulated ALPHA rewards. Any ALPHA you earned while locked is still claimable from the principal miner's dashboard.

- Go to [liquidity.0xmarkets.io/principal-miners](https://liquidity.0xmarkets.io/principal-miners)
- Navigate to your principal miner's page
- Claim any outstanding ALPHA rewards as usual

> See [How to Claim Rewards](claim-rewards.md) for the full guide.

### Creating a New Position

If you want to re-enter with a new lock:

1. Go to [liquidity.0xmarkets.io](https://liquidity.0xmarkets.io)
2. Start a new lock from scratch via your principal miner or using the "Become an LP" flow
3. The deposit process is identical to your first lock

> Consider timing your new lock before **Thursday 23:00 UTC** to be included in the upcoming epoch.

---

## Troubleshooting

### "Withdraw" button not appearing

- **Lock hasn't expired yet**: Check the expiration date on your position card — the Withdraw button only appears after the lock expires
- **Wallet not connected**: Connect your EVM wallet that owns the lock
- **Wrong wallet connected**: Disconnect and reconnect with the wallet that created the lock
- **Wrong network**: Switch to Base Mainnet (Chain ID: 8453)
- **Try refreshing**: Click the **Refresh** button on the My Positions page

### Cooldown shows a future date (not "Ready")

The 7-day cooldown has not yet passed. This can happen if:
- Your lock duration was shorter than 7 days
- You are checking very shortly after lock expiry

Wait until the date shown in the cooldown field, then return to withdraw.

### "Wrong wallet" warning in the confirmation modal

The wallet you have connected does not match the owner of this lock position. To fix:

1. Click **"Disconnect"** in the modal or your wallet app
2. Connect the correct wallet (the one used to create the lock)
3. The owner address is shown in the modal — use it to identify the right wallet

### Transaction failed in wallet

- **Insufficient ETH**: Ensure you have ETH on Base for gas fees
- **Network congestion**: Try again with a higher gas limit
- **Stale transaction**: If you were on the modal for a while, close it and reopen to refresh the transaction data
- Check the error message in your wallet for more specific guidance

### USDC not showing in wallet after transaction confirms

- ERC-20 tokens sometimes need to be manually added to your wallet. Import USDC:
  - Contract: `0x833589fCD6eDb6E08f4c7C32D4f71b54bdA02913` (USDC on Base)
- Wait a few minutes — balance updates can sometimes lag
- Verify the transaction succeeded on [BaseScan](https://basescan.org)

### Position still showing after withdrawal

- Click **Refresh** on the My Positions page
- If it persists, wait a few minutes for the indexer to update and refresh again
- If the transaction confirmed on-chain, the USDC is in your wallet even if the UI is slow to update

---

## Related Guides

- **[How to Top Up & Extend](how-to-top-up-and-extend.md)** — Add more USDC or increase your lock duration
- **[How to Claim Rewards](claim-rewards.md)** — Claim your ALPHA earnings after withdrawing
- **[Federated Miner Guide](federated-miner-guide.md)** — Full guide to locks, rewards, and position management
- **[Fees & Rewards](../how-it-works/fees-and-rewards.md)** — Understand vault performance and the cooldown period
- **[Safety & Liquidations](../how-it-works/safety-and-liquidations.md)** — Learn about vault risk and LP liquidations
