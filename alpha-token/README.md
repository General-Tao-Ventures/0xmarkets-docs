# Alpha Token

**ALPHA** is the native token of the [Cartha subnet (SN35)](../cartha/README.md). It coordinates the protocol's three economic surfaces:

1. **Emissions** — newly issued ALPHA distributed to miners, validators, and the incentive pool every epoch
2. **Fees** — trading fees from 0xMarkets, split across LPs, veALPHA stakers, and the treasury
3. **Governance (veALPHA)** — ALPHA holders lock for veALPHA to direct emissions and adjust protocol parameters

## At a Glance

| Stream | Allocation |
|--------|-----------|
| **ALPHA emissions to miners (LPs)** | 31% |
| **ALPHA emissions to validators** | 41% |
| **ALPHA emissions to incentive pool** | 10% |
| **ALPHA emissions to owner / protocol ops** | 18% |
| **Trading fees to LPs** | 50% |
| **Trading fees to veALPHA stakers** | 40% |
| **Trading fees to protocol treasury** | 10% |

Detailed mechanics:

* [Rewards › Token Emissions](rewards/token-emissions.md) — how the emission schedule and deposit-score math work
* [Rewards › Fee Distribution](rewards/fee-distribution.md) — how trading fees are split and paid out
* [Incentives / Campaigns](incentives.md) — how the 10% incentive pool is deployed
* [Referrals](../referrals.md) — affiliate program and trader rebates

## Governance (veALPHA)

Locking ALPHA produces **veALPHA**:

* **Longer locks** earn more voting weight *and* a larger share of fees
* **Alpha Voting** directs ALPHA emissions to specific vaults
* **Fees Voting** adjusts fee splits and other protocol parameters

veALPHA is the protocol's steering wheel — the parties most aligned with long-term success (long-locked holders) have the most say in how emissions and fees route.

## Why ALPHA Matters to Each Participant

* **Traders** — earn ALPHA from the incentive pool via the leaderboard and IB program
* **LPs (miners)** — earn ALPHA emissions proportional to deposit score, on top of USDC trading fees
* **Validators** — earn ALPHA for liquidation execution and subnet maintenance
* **Long-term holders** — lock ALPHA → veALPHA → claim a slice of every trading fee + direct emissions

ALPHA flows the same way every epoch — miner activity, trading volume, and validator performance all feed back into the same token economy.
