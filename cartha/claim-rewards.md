# How to Claim Rewards

Quick guide for federated miners: claim your ALPHA rewards from the Principal Miner Dashboard (e.g. General Tensor).

---

## Prerequisites

- **EVM wallet** — same wallet you used to lock your USDC
- **Bittensor coldkey** — SS58 address where ALPHA will be sent

### Don't have a Bittensor wallet?

- **Talisman** (recommended): [talisman.xyz](https://www.talisman.xyz/) — browser extension, no CLI needed. Create a wallet, add Bittensor account, copy your coldkey SS58.
- **CLI**: `btcli wallet create` — see [Bittensor docs](https://docs.learnbittensor.org/btcli#btcli-wallet)

---

## Video Walkthrough

<video controls width="100%">
  <source src="../.gitbook/assets/principal-miner-dashboard/Cartha-claim-rewards-with-GTV.mp4" type="video/mp4">
  Your browser does not support the video tag.
</video>

---

## Steps

1. Go to [cartha.finance/principal-miners](https://cartha.finance/principal-miners) and pick your principal miner (e.g. **General Tensor**)
2. **Connect your EVM wallet** — the one you used to lock your USDC
3. Scroll to your earnings summary and click the green **"Claim Rewards"** button

![Claim Rewards Button](../.gitbook/assets/claim-button-click.png)

4. The **Claim Rewards** modal will appear. Enter the amount (or click **MAX**) and paste your **Bittensor coldkey** (SS58 address)

![Claim Rewards Modal](../.gitbook/assets/claim.png)

![Enter Claim Details](../.gitbook/assets/input-claim.png)

5. Click **"Sign & Claim"** — you'll be prompted to sign a message with your connected EVM wallet to verify ownership
6. Once confirmed, you'll see a **"Claim Successful"** screen. Your ALPHA is sent to your Bittensor coldkey.

![Claim Successful](../.gitbook/assets/claim-successful-federated-miner.png)

---

## Related Guides

- **[Principal Miner Dashboard](principal-miner-dashboard.md)** — Full dashboard walkthrough and earnings breakdown
- **[Federated Miner Guide](federated-miner-guide.md)** — Complete setup, deposit, and claim flow
- **[Deposit via Principal Miner](federated-miner-deposit-principal.md)** — How to lock your first position
