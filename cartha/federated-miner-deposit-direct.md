# Direct Deposit (Any Hotkey)

Lock funds by pasting any principal miner's hotkey directly into the **"Become an LP"** form. Use this method if you already have a specific miner's hotkey or want to lock through a miner that isn't listed on the Principal Miners page.

> Make sure you've completed [Step 1: Set Up Your Wallet](federated-miner-guide.md#step-1-set-up-your-wallet) before continuing.

---

## Before You Start

You'll need the **SS58 hotkey address** of the principal miner you want to lock through. This is a 48-character string starting with `5`. You can find hotkeys:

- On the [Principal Miners page](https://cartha.finance/principal-miners)
- On the [Leaderboard](https://cartha.finance/leaderboard)
- Through community channels (Discord, etc.)

---

## Step-by-Step

### 1. Connect Your Wallet

1. Go to [https://cartha.finance](https://cartha.finance)
2. Click **"Connect Wallet"** in the top right corner and select your wallet provider
3. Make sure you're connected to **Base Mainnet** network

### 2. Navigate to "Become an LP"

4. Click **"Become an LP"** in the left navigation bar

### 3. Enter Your Lock Details

5. **Enter the Principal Miner's Hotkey** — Paste the SS58 address of the principal miner you want to lock through

![Paste Hotkey](../.gitbook/assets/paste-your-or-principal-miner-hotkey.png)

The system will verify the hotkey is registered on the subnet.

6. **Select a Pool** — Choose which trading pair you want to provide liquidity for (BTC/USD, ETH/USD, etc.)

![Select Pool](../.gitbook/assets/select-available-pools.png)

7. **Enter Amount** — Specify how much USDC you want to lock

![Enter Amount](../.gitbook/assets/input-amount.png)

8. **Set Lock Duration** — Choose how many days to lock your funds (minimum 7 days, maximum 365 days). Longer lock periods increase your deposit score and share of ALPHA rewards.

![Enter Lock Days](../.gitbook/assets/input-lock-days.png)

### 4. Execute the Transaction

9. **Request Signature & Continue** — Click the button to proceed

![Continue](../.gitbook/assets/continue.png)

10. **Approve USDC** — First, approve the vault contract to spend your USDC. Confirm in your wallet (requires a small gas fee in ETH).

![Approve USDC](../.gitbook/assets/approve-USDC-limit.jpeg)

11. **Lock Position** — After approval, confirm the second transaction to lock your USDC in the vault.

![Lock Position](../.gitbook/assets/check-lock-position.jpeg)

### 5. Verify Your Position

12. **Wait for confirmation** — It may take 30 seconds to 5 minutes for the position to be processed by the verifier.

![Wait for Confirmation](../.gitbook/assets/wait-30s-5m-refresh-to-check-position.jpeg)

13. **View your position** — Navigate to **"My Positions"** in the sidebar to see your active lock.

![My Positions](../.gitbook/assets/final-my-positions-page.png)

You'll see:
- Pool ID and trading pair
- Principal miner hotkey
- Lock status
- Initially locked amount and total committed
- Lock expiration date
- Options to **Extend** or **Top Up** your position

---

## Next Steps

Once your funds are locked, continue with the main guide:

- **[Step 3: Principal Miner Dashboard](federated-miner-guide.md#step-3-principal-miner-dashboard)** — Monitor your position and earnings
- **[Step 4: Claim ALPHA Rewards](federated-miner-guide.md#step-4-claim-alpha-rewards)** — Withdraw your earned ALPHA
- **[Managing Your Position](federated-miner-guide.md#managing-your-position)** — Top up, extend, or withdraw
