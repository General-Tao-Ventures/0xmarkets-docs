# Rewards

ALPHA rewards on Cartha flow from two sources:

1. **Token emissions** — newly issued ALPHA each epoch, distributed across participants
2. **Fee distribution** — trading fees from 0xMarkets, split across LPs, stakers, and the protocol treasury

Together they define the return profile for everyone in the system:

| Participant | Earns from emissions | Earns from fees |
|-------------|---------------------|-----------------|
| **Miners (LPs)** | 31% of ALPHA emissions | 50% of trading fees (USDC) |
| **Validators** | 41% of ALPHA emissions | 20% of liquidation fees (USDC) |
| **Incentive pool** | 10% of ALPHA emissions | — |
| **veALPHA stakers** | — | 40% of trading fees (pro-rata by ve balance) |
| **Protocol treasury** | 18% (owner emissions) | 10% of trading fees |

See:

* [Token Emissions](token-emissions.md) — the emission schedule, deposit-score math, and weekly epoch timing
* [Fee Distribution](fee-distribution.md) — how trading and liquidation fees are sourced and split
