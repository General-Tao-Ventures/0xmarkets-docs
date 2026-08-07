# How it works

This section covers the **protocol-level machinery** behind 0xMarkets — how liquidity is committed, how rewards are earned, and how the network keeps trading deep and decentralized. If you're here to trade, the [Trading](../trading/README.md) rail has everything you need; this section is the layer underneath it.

The pieces fit together like this:

- **Liquidity providers (miners)** supply USDC into per-market vaults on **Bittensor Subnet 35 (SN35)** — the 0xMarkets Liquidity Engine. They provide capital; they do **not** price trades. Pricing comes from the [Pyth Pro oracle](../trading/pricing-and-oracle.md) and on-chain price impact.
- **[Weekly epochs](weekly-epochs.md)** — liquidity commitments and emissions run on a fixed 7-day cycle (Friday 00:00 UTC → Thursday 23:59 UTC). Lock by Thursday 23:00 UTC to give the indexer time to detect your position before the freeze.
- **[Fees & rewards](fees-and-rewards.md)** — how trading fees are split, how Alpha emissions are distributed, and how lock expiry and withdrawals work.
- **Safety** — trades are priced and guarded by the oracle; positions that breach maintenance margin are liquidated, and a per-market insurance fund backstops extreme events. See [Liquidations](../trading/liquidations.md) and [Insurance fund](../security/insurance-fund.md).
- **Governance** — staking Alpha mints **veALPHA**, which votes on how the exchange distributes its trading fees (with LP pool weights next). Rolling out progressively. See [Staking & Governance (veALPHA)](../alpha-token/vealpha.md).

## Next

- [Weekly epochs](weekly-epochs.md)
- [Fees & rewards](fees-and-rewards.md)
- [Alpha Token](../alpha-token/README.md)
