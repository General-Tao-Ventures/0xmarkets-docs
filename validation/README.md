# Validation

Validators on the Cartha subnet are the **price-verification and liquidation-execution layer** of 0xMarkets. They watch markets, score miners, publish weights to Bittensor, and execute liquidations the moment trader margin is breached. They are paid in ALPHA emissions and a share of every liquidation fee — and slashed if they miss their duty.

## What Validators Do

| Responsibility | Detail |
|----------------|--------|
| **Score miners** | Run a deterministic scoring algorithm against the frozen epoch's miner list |
| **Publish weights** | Submit normalized scores to Bittensor every epoch (~72 min cadence on the chain side) |
| **Cross-verify oracle prices** | Independently confirm Pyth feeds before acting on them |
| **Execute liquidations** | Submit liquidation transactions on-chain when a position breaches maintenance margin |
| **Filter expired/dereg positions** | Remove ineligible miners throughout the week |
| **Maintain uptime** | Slashing penalties for missed duty |

## What Validators Earn

* **41% of ALPHA emissions** — for subnet maintenance and weight publishing
* **20% of liquidation fees** in USDC — paid on each successful liquidation
* **No share of trading fees** — that flows to LPs (50%), veALPHA (40%), and treasury (10%)

## Miner Scoring

Every validator runs the same transparent formula:

```
position_score = pool_weight × amount_usdc × lock_boost
miner_score    = Σ position_score_i   (sum across active positions)

lock_boost     = min(lock_days, 365) / 365
```

* **`amount_usdc`** — the **epoch-frozen** locked amount (mid-epoch top-ups don't count until the next freeze)
* **`lock_boost`** — proportional to lock duration, capping at 1.0 for 365-day locks (a 182-day lock earns 0.5)
* **`pool_weight`** — currently equal across pools in pre-DEX mode; on-chain target-allocation contracts will set these post-launch

Principal miners with vault balance below **100,000 USDC** are scored at zero — and so are the delegated miners locked into them.

## Weight Normalization

After scoring, validators publish normalized weights:

| Recipient | Allocation |
|-----------|-----------|
| **Incentive Pool** | 24.3902% (fixed) |
| **Qualified miners** | 75.6098% (proportional to score) |
| Subnet owner hotkey | 75.6098% fallback (when no miners qualify — emission burn) |

## Liquidation Execution

Validators race to detect and submit liquidations:

1. Watch open positions against the live oracle price
2. The first validator to detect a margin breach submits the liquidation
3. Position closes; 10% liquidation fee is split (20% validators / 50% insurance pool / 30% ALPHA buyback & burn)
4. Validator collects the 20% executor share in USDC

This is intentionally competitive — speed of detection and execution determines validator profitability.

## Slashing

Validators post **ALPHA collateral** to participate in liquidation execution. They are slashed for:

* Missing a liquidation that another participant successfully submits
* Publishing inconsistent weights
* Extended downtime
* Cross-verification failures

Slashing aligns validator incentives with LP protection: a validator that lets a liquidation slip risks losing money personally.

## Hardware Requirements

| Resource | Minimum |
|----------|---------|
| **CPU** | 2 cores |
| **RAM** | 4 GB |
| **Disk** | 20 GB SSD |
| **Network** | Stable internet with minimal downtime |

## Getting Started

See the [Validator Guide](../cartha/validator-guide.md) for the complete setup, including hotkey registration, configuration, and operational runbook. The [Testnet Validator Guide](../testnet/validator-guide.md) is the recommended starting point before running on mainnet.

## Related

* [Pricing](../trading/pricing.md) — how oracle validation feeds into the protocol
* [Liquidations](../trading/liquidations.md) — the trader-side view of what validators are doing
* [Risk Management](../cartha/risk-management.md) — how validator action protects LP capital
* [Token Emissions](../alpha-token/rewards/token-emissions.md) — full emission math
