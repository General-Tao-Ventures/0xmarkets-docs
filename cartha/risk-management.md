# Risk Management

Liquidity providers on Cartha take on directional exposure to trader PnL in the markets they back. This page documents what those risks are and the protocol mechanisms that bound them.

## What an LP Is Exposed To

| Risk | Mechanism |
|------|-----------|
| **Trader PnL** | If traders are net long and price rises, the vault pays out. The vault grows when traders lose. |
| **Liquidation shortfall** | Extreme volatility can close a position too late to cover full losses ("bad debt"). |
| **Oracle anomaly** | A bad price tick can mis-price open positions, briefly. |
| **Lock duration** | Funds are committed until the lock expires *and* the cooldown ends — you cannot withdraw before. |
| **Validator failure** | A missed liquidation can grow a losing position past the point where collateral covers it. |
| **Smart-contract risk** | Bugs in the vault or peripheral contracts. |

## How Each Risk Is Mitigated

### Vault Isolation

Each market has its own vault (see [LP Vaults](lp-vaults.md)). A bad-debt event in one market draws from **that vault and the insurance pool** — not from LPs in other markets. Choose markets you understand and can stomach the exposure to.

### Insurance Pool

A protocol-owned reserve **funded by 50% of every liquidation fee**. The pool absorbs shortfalls before any LP capital is touched.

* Sized to cover expected tail events
* Deployment is governance-controlled by veALPHA holders
* Refilled continuously as liquidations occur

### Validator Cross-Verification and Slashing

Validators:

* Independently confirm Pyth oracle prices before acting on them
* Compete to execute liquidations the instant margin is breached
* Are **slashed** for missed liquidations — they post ALPHA collateral and lose it for failing duty

Slashing aligns validator incentives with LP protection: a validator that lets a liquidation slip past loses money personally.

### Oracle Redundancy

Multiple price providers feed each market. If a primary feed degrades, fallback paths kick in. The interface and on-chain checks both reject anomalous ticks outside the Pyth confidence band.

### Lock and Cooldown

Locks commit capital for the duration you chose, plus a **mandatory 7-day cooldown from lock creation**. This prevents short-term lock gaming and ensures LPs cannot exit mid-epoch when trader PnL is moving against them.

To withdraw an expired position, **both** must be true:

1. The lock duration has elapsed
2. The 7-day cooldown from lock start has passed

If you **deregister from the subnet**, your position is auto-evicted within ~72 minutes and funds return to your wallet — no manual action required.

### Smart-Contract Audits

Vault and core contracts were audited by **Hashlock** in January 2026 and received a **Secure** rating. See [Security › Audits](../security/README.md).

## What LPs Should Watch

* **Net OI imbalance** in your market — large directional skew means larger potential payouts in either direction
* **Vault utilization** — borrowing fees scale with utilization, which improves LP yield but also signals concentrated risk
* **Insurance pool size** vs typical liquidation flow — the pool exists for this purpose, but a healthy reserve is a good signal
* **Market closures** — open trader positions persist across FX/metals/commodities closures; price gaps on reopen can move LP exposure

## Position Hygiene

* **Diversify across markets** to avoid concentrated exposure to one asset's PnL
* **Use shorter locks** when you're unsure about a market or just getting started
* **Monitor your dashboard** at [liquidity.0xmarkets.io/positions](https://liquidity.0xmarkets.io/positions) — verify status, rewards, and expiry
* **Check [Weekly Epochs](../how-it-works/weekly-epochs.md)** for timing — locks not in by Thursday 23:00 UTC miss the next epoch

> Risk: LP returns are not guaranteed. In adverse conditions, vault NAV can decline. Read [Legal & risk](../legal-and-risk.md) before locking capital.
