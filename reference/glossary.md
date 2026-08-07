# Glossary

Plain-language definitions of the terms used across these docs. Where a term has its own page, the link takes you to the full explanation.

**Acceptable price** — The worst execution price you'll accept on an order. Because orders execute a moment after you submit them, you set a limit; if the fill would be worse than your acceptable price, the order reverts instead of filling. See [Price impact & slippage](../trading/price-impact-and-slippage.md).

**ADL (auto-deleveraging)** — A pool-protection backstop. If the winning side's total open profit grows large enough to threaten pool solvency, the most profitable positions on that side can be partially closed to keep the system solvent. See [PnL & profit settlement](../trading/pnl-and-settlement.md).

**Borrowing fee** — A cost that accrues on your position size over time for holding a leveraged position. The smaller open-interest side of a market pays no borrowing fee. See [Funding & borrowing](../trading/funding-and-borrowing.md).

**Collateral** — The USDC you post to back a position. Your collateral plus or minus unrealized PnL is your equity; if it falls to the maintenance margin, you're liquidated.

**Dual-oracle** — 0xMarkets' pricing design. Pyth Pro is the primary feed at Beta launch, with Chainlink Data Streams as a secondary feed enabled shortly after. See [Pricing & the oracle](../trading/pricing-and-oracle.md).

**Funding fee** — A periodic payment between traders. The side with larger open interest pays the side with smaller open interest, at a rate that scales with the imbalance. It can be a cost or a credit to you depending on which side you're on. See [Funding & borrowing](../trading/funding-and-borrowing.md).

**Keeper** — An automated executor that completes the second step of every order: it picks up your submitted order and executes it against a fresh signed oracle price. Keepers also trigger liquidations and stop/limit orders.

**Leverage** — The multiple by which your position size exceeds your collateral. At 20x, $1,000 of collateral controls a $20,000 position. Higher leverage magnifies both gains and losses. See [Leverage & margin](../trading/leverage-and-margin.md).

**Leverage ladder** — The rule that caps maximum leverage by position size: the cap steps down as your position notional grows, so large positions are limited to lower leverage than small ones. See [Leverage & margin](../trading/leverage-and-margin.md).

**Liquidation** — The automatic closing of your position when your equity falls to the maintenance margin. You forfeit 100% of your margin; there is no partial refund. See [Liquidations](../trading/liquidations.md).

**Liquidation fee** — The cost taken when a position is liquidated, equal in effect to your maintenance margin (collateral × MMR). See [Liquidations](../trading/liquidations.md).

**Long** — A position that profits when the market price rises and loses when it falls.

**Maintenance margin (MMR)** — The minimum equity a position must hold to stay open, expressed as a rate. 0xMarkets uses a dynamic MMR that rises with your leverage — up to a 20% ceiling, down to a 1% floor: `MMR = clamp((Your Leverage ÷ Market's Max Leverage) × 20%, 1%, 20%)`. See [Liquidations](../trading/liquidations.md).

**Mark price** — The oracle-derived price used to value your open position, calculate PnL, and decide liquidations. It comes from the live price feed, not an order book.

**Notional** — Your total position size in USD (collateral × leverage). The leverage ladder tiers are based on notional, not on your collateral.

**Open interest (OI)** — The total size of all open positions in a market, split into long and short. The balance between the two drives funding, price impact, and which fee rate a trade pays.

**Oracle** — The external price source that feeds 0xMarkets real-time prices. See [Pricing & the oracle](../trading/pricing-and-oracle.md).

**Perpetual future** — A leveraged contract that tracks an asset's price with no expiry date. You hold it as long as you like, paying or receiving funding along the way, until you close it or it's liquidated.

**Position** — Your open trade in a single market: a direction (long or short), a size, the collateral backing it, and an entry price.

**Price impact** — The adjustment to your fill price caused by how your trade affects the market's balance. Trades that worsen the long/short balance pay impact; trades that improve it get price improvement. Capped at ±0.5%. See [Price impact & slippage](../trading/price-impact-and-slippage.md).

**Profit cap** — A pool-solvency backstop (not a per-trade cap). It only engages if the entire winning side's open profit would exceed a set fraction of the LP pool, scaling those profits down proportionally. See [PnL & profit settlement](../trading/pnl-and-settlement.md).

**Pyth Pro** — The primary low-latency oracle feed used at Beta launch, delivering signed real-time prices that keepers execute against. See [Pricing & the oracle](../trading/pricing-and-oracle.md).

**Short** — A position that profits when the market price falls and loses when it rises.

**Slippage** — The difference between the price you expected and the price you actually got. You cap your slippage with an acceptable price. See [Price impact & slippage](../trading/price-impact-and-slippage.md).

**Spread** — The gap between the buy-side and sell-side price, embedded in the oracle's signed min/max prices rather than charged as a separate fee.

**Stop-loss** — A trigger order that closes your position once the market reaches a level you set, capping your loss. It closes as a normal trade, so you keep your remaining margin — unlike a liquidation. See [Order types](../trading/order-types.md).

**Take-profit** — A trigger order that closes your position once it reaches a target profit level. See [Order types](../trading/order-types.md).

**TWAP** — Time-weighted average price: an order type that splits a large order into smaller pieces executed over time to reduce price impact. See [Order types](../trading/order-types.md).

**Two-step execution** — How every order works: you submit it, then a keeper executes it against a fresh signed oracle price. Because the execution price can differ from the submission-time price, you protect yourself with an acceptable price.

**USDC** — The stablecoin used as collateral and for settlement on 0xMarkets, on Base. All PnL is paid in USDC.

**veAlpha** — Alpha locked for voting-escrow, which directs a share of protocol fees and governs adjustable parameters. (Out of scope for trading; mentioned here only because some fee distributions reference it.)

## Next

- [FAQ](faq.md)
- [Markets](markets.md)
- [Fee schedule](fee-schedule.md)
