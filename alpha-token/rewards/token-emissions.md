# Token Emissions

ALPHA is issued continuously by the Bittensor subnet and distributed each **epoch** — a fixed 7-day window from Friday 00:00 UTC to Thursday 23:59 UTC.

## Emission Split

Every epoch's ALPHA issuance is split across four buckets:

| Allocation | Recipient | Purpose |
|------------|-----------|---------|
| **31%** | Miners (LPs) | Compensation for providing liquidity to 0xMarkets markets |
| **41%** | Validators | Liquidation execution and subnet maintenance |
| **10%** | Incentive Pool | Flexible allocation — trader leaderboards, IB rebates, airdrops, ecosystem programs |
| **18%** | Owner | Protocol development and operations |

For incentive-pool details, see [Incentives / Campaigns](../incentives.md).

## Daily Issuance

The subnet emits **~7,200 ALPHA per day**, so:

* Miners collectively earn **~2,232 ALPHA/day** (31%)
* Validators collectively earn **~2,952 ALPHA/day** (41%)
* The incentive pool grows by **~720 ALPHA/day** (10%)
* Owner emissions are **~1,296 ALPHA/day** (18%)

## How Miner Rewards Are Calculated

Your share of the 31% miner allocation depends on your **deposit score**:

```
deposit_score = locked_amount × time_factor × pool_weight

your_share = your_deposit_score ÷ sum(all_deposit_scores)
```

* **`locked_amount`** — USDC locked at the epoch freeze (mid-epoch top-ups don't count this epoch)
* **`time_factor`** — increases with chosen lock duration; longer locks earn more
* **`pool_weight`** — set by veALPHA Alpha Voting; some markets attract more emissions than others

## The Weekly Epoch Cycle

Cartha uses a strict weekly cycle. Your score is locked in at the freeze, and it stays put for the rest of the epoch:

| Phase | When | What happens |
|-------|------|--------------|
| **Upcoming** | Friday → Thursday (one cycle before yours) | Verify your lock; you appear as "In Next Epoch" |
| **Freeze** | Friday 00:00 UTC | Snapshot taken; miner list becomes immutable |
| **Active** | Friday → Thursday | You're locked in and earning |
| **Carry-over** | Next Friday 00:00 UTC | Eligible positions roll forward; expired/dereg removed |

**Practical rule**: lock by **Thursday 23:00 UTC** to clear the indexer in time for the next freeze. Locks completed after Friday 00:00 UTC wait a full week before earning.

See [Weekly Epochs](../../how-it-works/weekly-epochs.md) for the full lifecycle, indexer timing, and a timezone reference.

## Reward Claiming

* **For principal miners**: ALPHA arrives directly in your Bittensor hotkey wallet
* **For delegated miners (federated)**: ALPHA arrives in your principal miner's wallet first; you claim your share via the [Principal Miners dashboard](https://liquidity.0xmarkets.io/principal-miners) or per off-chain agreement
* **Track everything** at [liquidity.0xmarkets.io/leaderboard](https://liquidity.0xmarkets.io/leaderboard) and [liquidity.0xmarkets.io/positions](https://liquidity.0xmarkets.io/positions)

## What Stops Emissions

* **Lock expiry** — rewards stop the day the lock period ends
* **Deregistration** — position is auto-evicted within ~72 minutes; USDC returns to your wallet
* **Mid-epoch top-ups** — already-locked emissions continue at the frozen score; the top-up earns at the next freeze
* **Subnet emission halt** — affects all participants equally (very rare)

> Emissions are a function of subnet performance, validator weight publishing, and pool selection. Returns are not guaranteed.
