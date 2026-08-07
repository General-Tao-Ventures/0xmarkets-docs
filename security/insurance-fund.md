# Insurance fund

When you open a position, the other side of your trade is a pool of liquidity supplied by liquidity providers. In extreme conditions — a sharp gap, a cascade of liquidations — losses can exceed what the normal mechanics absorb. The **insurance fund** is the backstop for those moments.

> **It's a backstop, not a guarantee.** The insurance fund reduces the impact of extreme events. It does not promise to cover every loss, and it is not a guarantee on your position. Read [Risk disclosures](risk-disclosures.md).

## What the insurance fund is

0xMarkets runs a **per-market insurance fund** at the exchange layer. Each market has its own fund, so stress in one market is buffered without draining the protection of another.

The fund does two things:

1. **It collects** — a configurable slice of liquidation and position fees is directed into the fund over time, building a reserve.
2. **It backstops** — when a market's pool takes a realized drawdown that crosses a defined trigger, the fund can **inject capital back into that market's pool**, helping it stay solvent and keep honoring trades.

## How it's funded

Two streams feed the insurance fund:

- **Liquidation fees.** When a position is [liquidated](../trading/liquidations.md), **70% of the liquidation fee is directed to the insurance pool.** (The remaining 30% goes to an Alpha buyback. This distribution is set by the protocol and is planned to come under governance control in a future release.)
- **A configurable share of position fees.** A slice of the fees paid on opening and closing positions can also be routed into the fund.

Fund sizes, the exact fee share, and the drawdown trigger are parameters set by the protocol and tuned over time as each market grows.

## What it does and doesn't protect

- **It does:** give each market a reserve that can be injected into the pool to absorb extreme realized losses and reduce the chance the pool becomes unable to pay out.
- **It doesn't:** guarantee your individual position, cover unlimited losses, or remove the risk that — in a severe enough event — pool-solvency mechanics still bind.

When a winning side's open profit would exceed the pool's capacity, separate pool-solvency mechanics (a profit cap and auto-deleveraging) apply at the trading layer — see [PnL & profit settlement](../trading/pnl-and-settlement.md). The insurance fund works alongside those, as a reserve, not as a promise that every trade pays out in full.

## Next

- [Liquidations](../trading/liquidations.md)
- [Oracle security](oracle-security.md)
- [Risk disclosures](risk-disclosures.md)
