# Collateral

0xMarkets uses **USDC as the sole collateral token** across every market. This simplifies position management and lets the protocol concentrate liquidity behind one well-understood, fully-redeemable stable asset.

## Why USDC-Only

* **One asset to manage** — no separate margin tokens per market, no swap fees moving between collateral types
* **Predictable funding** — funding and borrowing fees settle in the same unit they accrue in
* **Deeper pools** — every Cartha vault is denominated in USDC, so all liquidity stacks behind every market

## Multichain Accounts

0xMarkets Accounts let you fund positions from **any supported chain** without manually bridging.

* Deposit USDC on any supported network — the protocol bridges to the settlement chain automatically
* Your account balance is available across all supported networks
* No need to switch chains, hold separate gas tokens for bridges, or manage bridging transactions yourself

## Gas

All transactions on the settlement chain require **ETH for gas**. If you're funding from another chain, hold a small ETH balance on the settlement chain to cover order submission, position adjustments, and close transactions.

## Deposits

1. Open the **Account** panel from the trade interface
2. Select the source chain you hold USDC on
3. Enter the deposit amount and approve USDC spending (one-time per chain)
4. Submit the deposit — funds arrive in your 0xMarkets Account, available immediately for trading

## Withdrawals

1. Open the **Account** panel and choose **Withdraw**
2. Pick the destination chain and amount
3. Submit — withdrawals settle to your wallet on the chosen chain after the cross-chain message is relayed

## Collateral and Open Positions

* Open positions reserve a portion of your USDC as **margin**
* Funding and borrowing fees accrue against position collateral, not your free balance
* Margin breaches trigger a [liquidation](liquidations.md); to avoid this, top up collateral on the position or reduce position size before the maintenance margin is hit
