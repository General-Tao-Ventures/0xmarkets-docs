# Governance (veALPHA)

veALPHA is the vote-escrow governance token of 0xMarkets. By locking ALPHA tokens for a chosen duration, holders receive veALPHA — a non-transferrable, time-weighted balance that entitles them to a share of protocol trading fees and a vote in governance decisions.

The mechanism is inspired by the vote-escrow model pioneered by Curve Finance. It rewards long-term alignment: the longer and larger your lock, the greater your share of rewards and voting power.

***

## Why Lock ALPHA?

Locking ALPHA into veALPHA creates two primary benefits:

1. **USDC yield** — 40% of all trading fees generated on 0xMarkets are distributed to veALPHA holders, paid in USDC each epoch.
2. **Governance power** — veALPHA holders vote on which markets receive what share of ALPHA emissions, influencing how liquidity is incentivised across the platform.

This gives the token a fundamental, stablecoin-denominated value floor:

```
token_value ≈ trading_fees_to_stakers / clearing_yield
```

The more the platform trades, the more valuable locking becomes.

***

## Who Is veALPHA For?

**Miners (LPs)** earn ALPHA as rewards for providing liquidity. Instead of selling those rewards immediately, miners can lock them into veALPHA to compound their returns with a share of USDC trading fees on top of their existing yield.

**ALPHA holders and speculators** can lock tokens to earn a proportional share of exchange revenue — effectively owning a productive stake in the growth of the subnet. Early lockers benefit most: they accumulate a larger veALPHA position before the platform scales, meaning their share of future fees is locked in at a favourable size.

***

## How veALPHA is Calculated

Your veALPHA balance is determined by how much you lock and for how long:

```
veALPHA = ALPHA × lockDuration / maxLockDuration
```

* **Maximum lock duration:** 2 years
* **Minimum lock:** any amount, any duration up to 2 years
* **Non-transferrable:** veALPHA is tied to your wallet and cannot be sold or transferred

**Example:**
* User A locks 7,500 ALPHA for 2 years → **7,500 veALPHA**
* User B locks 5,000 ALPHA for 1 year → **2,500 veALPHA**
* User A holds 75% of the veALPHA supply and receives 75% of rewards

This structure means a smaller holder who locks for longer can earn a proportionally larger share than a bigger holder who locks for a shorter period.

***

## USDC Rewards

Trading fees on 0xMarkets are distributed as follows each epoch:

| Recipient          | Share |
| ------------------ | ----- |
| LP Miners          | 50%   |
| veALPHA stakers    | 40%   |
| Protocol treasury  | 10%   |

The 40% allocated to veALPHA stakers is distributed **pro-rata** based on each holder's veALPHA balance at the snapshot of that epoch. Rewards are claimable in USDC at the end of each epoch. Unclaimed USDC remains in the smart contract until claimed.

***

## Lock Rules

* Locks are epoch-aligned — when you lock, rewards begin from the **next epoch**, not immediately.
* If you already have an active lock, any new lock must be **equal to or longer** than your current remaining duration.
* Extending your lock to a longer duration re-locks your full position to that new term.
* veALPHA is **non-transferrable** and bound to the wallet that created the lock.

***

## Governance & Voting

veALPHA holders vote on how ALPHA emissions are distributed across trading markets (e.g. EUR/USD, XAU/USD, XAU/BTC). Each market has a gauge, and voters allocate their veALPHA weight across gauges each epoch.

The weighted outcome determines each pool's share of ALPHA rewards for the following epoch. This creates a self-correcting system: voters are incentivised to direct rewards toward the most utilised markets, which in turn deepens liquidity and generates more USDC fees for everyone.

veALPHA holders may also vote on exchange parameters and protocol fee settings within defined bounds.

> Governance voting is on the roadmap and will be introduced progressively. Trading fee rewards are live from launch.

