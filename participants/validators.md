# Validators

Validators play a critical role in the 0xMarkets Liquidity Provider by scoring miners based on their USDC liquidity positions and publishing weights to the Bittensor network.

## Responsibilities

- Score miners based on locked USDC amounts, lock duration, and pool weights
- Publish normalized weights to Bittensor every epoch
- Filter expired and deregistered miner positions throughout the week
- Submit rankings to the 0xMarkets leaderboard after each weight publication

## How Validators Score Miners

Every validator runs the same transparent, deterministic scoring algorithm. Miners are scored based on three factors:

### 1. USDC Amount

The USDC amount used for scoring is the **epoch-frozen original amount** — the amount locked at Friday 00:00 UTC when the epoch starts. Mid-epoch top-ups are recorded as `pending_amount` and do not count until the following epoch. This freeze prevents manipulation during the scoring window.

### 2. Lock Duration Boost

Each position earns a proportional boost based on how long the USDC is locked:

```
lock_boost = min(lock_days, 365) / 365
```

A position locked for 365 days achieves the maximum boost of `1.0`. A position locked for 182 days achieves `0.5`. Longer commitments are rewarded proportionally.

### 3. Pool Weight

Each liquidity pool has a weight multiplier. Currently all pools use equal weight (`1.0`) in pre-DEX mode. After the full 0xMarkets liquidity layer launches, pool weights will be sourced on-chain from the target allocation contracts.

### Full Scoring Formula

```
position_score = pool_weight × amount_usdc × lock_boost
miner_score    = Σ position_score_i   (sum across all active positions)
```

Principal miners with a total vault balance below **100,000 USDC** receive a score of `0` regardless of lock duration. Since the principal miner's score drives all ALPHA emissions for their vault, federated miners inside that vault also receive no rewards for the epoch.

## Weight Distribution

After scoring all miners, validators normalize scores into Bittensor weights:

```
remaining_weight = 75.6098%   (after incentive pool allocation)
weight(miner_i)  = (score_i / total_score) × 75.6098%
```

| Recipient | Allocation |
| --- | --- |
| **Incentive Pool** | 24.3902% (fixed) |
| **Qualified miners** | 75.6098% (proportional to score) |
| Subnet owner hotkey | 75.6098% (emission burning when no miners qualify) |

## Minimum Compute Requirements

To run a validator for the 0xMarkets Liquidity Provider, you need:

- **CPU**: 2 cores minimum
- **RAM**: 4 GB minimum
- **Disk**: 20 GB SSD
- **Network**: Stable internet connection with minimal downtime

## Getting Started

See the [Validator Guide](../cartha/validator-guide.md) for complete setup instructions.
