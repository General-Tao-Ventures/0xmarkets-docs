# Fees & rewards

This page is the **protocol-level** view of how value flows through 0xMarkets: how trading fees are split, how Alpha emissions reward the network, and how lock expiry and withdrawals work for liquidity providers.

> Looking for what a trade actually costs you? See [Fees](../trading/fees.md) in the Trading rail — it covers the trading-fee rates per asset class, funding, borrowing, and network gas.

## Where trading fees go

Every trading fee paid on the exchange is split across the protocol. These are the **launch values** — the distribution is adjustable by [veALPHA governance](../alpha-token/vealpha.md), with each destination protected by a floor it can't be pushed below.

| Destination | Share | Floor | What it does |
|---|---|---|---|
| **LP pool** | 50% | 30% | Rewards the liquidity providers who back the market traded |
| **Staking pool** | 40% | 30% | Rewards Alpha holders who stake for veALPHA |
| **Treasury** | 10% | 10% | Funds protocol operations and growth |
| **Alpha buyback** | 0% | — | Reserved; directs value to Alpha when enabled |

The floors protect 70% of every fee, leaving 30% that governance can reallocate across the four destinations. Trading fees are paid and distributed in **USDC**.

## Where liquidation fees go

Liquidation fees are routed separately from trading fees (intent):

| Destination | Share |
|---|---|
| **Insurance pool** | 70% |
| **Alpha buyback** | 30% |

The insurance pool backstops each market against extreme events; the buyback directs value to Alpha. *This distribution is set by the protocol and is planned to come under governance control in a future release.* For how liquidations work and what they cost a trader, see [Liquidations](../trading/liquidations.md).

## Alpha emissions

The 0xMarkets Liquidity Engine (Bittensor Subnet 35) emits **Alpha** each epoch and distributes it to the participants who keep the network running:

| Recipient | Share | What it's for |
|---|---|---|
| **Validators** | 41% | The validator emission share — the native yield Alpha holders earn for holding and staking Alpha. |
| **Liquidity providers (miners)** | 31% | Allocated by **deposit score** (locked amount × time). The longer and larger the USDC deposit, the larger the allocation. |
| **Subnet owner** | 18% | Protocol development and operations. |
| **Incentive pool** | 10% | Flexible funding for ecosystem incentives (trading leaderboards, IB rebates, airdrops, community programs). |

Rewards are tracked at [liquidity.0xmarkets.io/leaderboard](https://liquidity.0xmarkets.io/leaderboard).

## Lock expiration & withdrawals

For liquidity providers, locked positions follow a fixed lifecycle.

### Expired positions

When a lock position expires:

- **Rewards stop automatically** — validators detect expired positions daily and stop distributing rewards.
- **Funds remain in vault** — your funds stay in the vault until you withdraw.
- **Manual withdrawal required** — withdraw via the UI when ready.

### Withdrawal requirements

To withdraw an expired position, **both** conditions must be met:

1. **Lock period expired** — your chosen lock duration has passed.
2. **Cooldown period passed** — a mandatory **7-day cooldown** measured from the initial lock start.

**Example timeline:**
- Lock 3 days starting Dec 11
- Lock expires: Dec 14 (rewards stop)
- Cooldown ends: Dec 18 (7 days from Dec 11)
- Can withdraw: Dec 18 or later

The 7-day cooldown starts from lock creation, not from lock expiry. This prevents short-term lock gaming.

### Deregistered miners

If you deregister from the subnet:

- **Automatic eviction** — your position is evicted within ~72 minutes.
- **Funds returned** — your funds are returned to your wallet automatically.
- **No manual action needed** — the verifier handles this.

## Next

- [Weekly epochs](weekly-epochs.md)
- [Alpha Token](../alpha-token/README.md)
- [Fees (trading)](../trading/fees.md)
