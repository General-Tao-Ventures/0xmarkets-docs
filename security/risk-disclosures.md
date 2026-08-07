# Risk disclosures

Using 0xMarkets — whether you trade, provide liquidity, or hold the assets involved — carries real risk. You can lose money, and on leveraged positions you can lose all of it. This page lays out the main risks across the whole system in plain language so you can decide whether this product is right for you. It is broad but **not exhaustive**, and **nothing here is financial advice.**

> **Only commit capital you can afford to lose.** If a full loss of the money you put in would materially hurt you, do not use leverage — and size the rest of your exposure accordingly.

## Two kinds of risk

It helps to separate the two risks people tend to lump together:

- **Counterparty risk** — the entity holding your money stops performing (it fails, freezes withdrawals, or runs off). This is the FTX / Celsius failure mode. 0xMarkets is **non-custodial**: your funds sit in on-chain smart contracts, not with a company that can lock you out. By design, this class of risk is largely removed — there is no central custodian to fail. *(That protection is only as strong as the contracts themselves — see Technology risk below.)*
- **Market risk** — the market moves and your position takes the loss. This one is **real and unavoidable**. It is the same risk every trader and liquidity provider has always faced, and it is the core risk you take here.

Most of what follows is a closer look at market risk and the technology, network, and legal risks that sit alongside it.

---

## Trading risks

**Leverage amplifies losses.** Leverage multiplies both gains and losses. A small move against a high-leverage position can wipe out your margin, and the higher the leverage, the smaller the adverse move it takes. See [Leverage & margin](../trading/leverage-and-margin.md).

**Liquidation means losing 100% of your margin.** If a position moves far enough against you it is **liquidated**, and a liquidation closes your entire margin — there is no partial refund, no margin call, and no warning. The only way to exit earlier and keep what's left is to close the position yourself or set a stop-loss. See [Liquidations](../trading/liquidations.md).

**Funding and borrowing erode held positions.** Perpetuals carry ongoing **funding** and **borrowing** costs that accrue for as long as a position is open. Over time these can meaningfully reduce — or eliminate — the value of a position, even one whose price has barely moved. See [Funding & borrowing](../trading/funding-and-borrowing.md).

**Volatility and price gaps.** Prices are volatile. FX and commodities also pause when their underlying markets close (overnight, weekends, holidays) and can **gap** sharply on reopen — a position held across a closed session can move against you while you cannot act, sometimes far enough to liquidate you. See [Market hours](../trading/market-hours.md).

## Pricing, oracle, and execution risks

**Oracle dependence.** Your trades are priced against an external oracle ([Pyth Pro](../trading/pricing-and-oracle.md)), not an order book. If the oracle is delayed, degrades, or is manipulated despite the on-chain guards, your fills or liquidations can be affected. A second independent feed (Chainlink Data Streams) is part of the design and is being enabled shortly after Beta to reduce single-source dependence. See [Oracle security](oracle-security.md).

**Slippage and price impact.** Large or imbalanced trades can move your execution price. Your fill can differ from the price you saw, bounded by the acceptable-price protection you set. See [Price impact & slippage](../trading/price-impact-and-slippage.md).

**Pool-solvency mechanics.** In extreme conditions, mechanisms that keep markets solvent — a cap on aggregate trader profit and auto-deleveraging — can affect how much profit is actually paid out on the most profitable positions. See [PnL & profit settlement](../trading/pnl-and-settlement.md).

## Liquidity-provider risks (if you provide liquidity)

Every trade has a counterparty: a pool of liquidity supplied by **liquidity providers (LPs)**. If you provide liquidity, you take the *other* side of the trader book, and a distinct set of market risks comes with that:

- **You are the counterparty to trader PnL.** When traders profit, the pool pays; when they lose, the pool collects. Being on the wrong side of trader profits at times is the model, not a malfunction.
- **Outlier moves, concentration, and adverse selection.** A sudden gap or cascade, a few large traders, or consistently skilled flow can move LP capital faster than fees and spread cushion it.
- **One-sided books and variance.** When traders crowd one direction, the pool holds the opposite directional exposure until it unwinds. Smaller, early trader populations carry wider short-run swings than mature ones.
- **Withdrawal and lockup.** Liquidity is committed to a market for the term you choose and becomes withdrawable once that term ends and it is free of open trades. It is not callable on demand.

The protocol cushions these (open-interest caps, per-position limits, leverage tiers, skew-based pricing, continuous borrow fees, an insurance fund, and auto-deleveraging) — but it does not remove them.

## Technology risks

**Smart-contract risk.** 0xMarkets runs as smart contracts on Base. Contracts can contain bugs or vulnerabilities; an audit reduces that risk but does not remove it. An initial audit by Hashlock (covering the liquidity-engine infrastructure) is complete, and a comprehensive end-to-end review with HackenProof is in progress — see [Audits](audits.md). Per-market vault isolation contains the blast radius of a problem, but an exploit, a faulty upgrade, or an integration failure could still result in loss of funds.

**Self-custody.** Non-custodial means you are responsible for your own wallet and keys. There is no password reset and no help desk that can recover funds for you. On-chain transactions are **irreversible** — a mistaken or malicious transaction you sign cannot be undone.

## Network and systemic risks

**Underlying networks.** 0xMarkets depends on two networks it does not control: **Base** for capital and execution, and **Bittensor Subnet 35** for the liquidity engine that coordinates and scores liquidity providers. Outages, congestion, reorgs, or failures on either are external risks on any user's register.

**Insurance fund is a backstop, not a guarantee.** The per-market insurance fund absorbs stress before it reaches liquidity, but it does **not** guarantee your position or promise to cover your losses. See [Insurance fund](insurance-fund.md).

## Asset and token risks

**Stablecoin risk.** Collateral is **USDC** on Base. A stablecoin can lose its peg or face issuer, regulatory, or bridging issues; the value of USDC is not guaranteed by 0xMarkets.

**Token and emissions risk.** Where rewards are paid in the Alpha token, their dollar value moves with the token's price — emissions can be worth materially less (or more) in dollar terms than when earned, independent of how the exchange performs.

## Governance and parameter risk

0xMarkets parameters — including the fee split (currently 50% LP / 40% veAlpha / 10% treasury / 0% buyback) and others — can be adjusted, in places through veAlpha governance where large holders can exert outsized influence. Parameters such as leverage tiers, fees, and limits may change over time, and changes can affect your positions or returns.

## Legal, regulatory, and tax risk

Your jurisdiction is your responsibility. 0xMarkets may not be available everywhere, and you should not use it where doing so is prohibited or restricted by applicable law, or where you are otherwise ineligible. The regulatory landscape for these products is still evolving, and tax treatment of any gains, fees, or rewards varies by country and by type. You are responsible for your own compliance and reporting — consider seeking independent legal and tax advice locally.

## Beta status

0xMarkets is in **Beta.** The exchange is live and fully functional, and is being actively refined. As with any newer platform, occasional issues can occur and some parameters will be tuned as it matures. 

## Not financial advice

Nothing in this documentation is financial, investment, legal, or tax advice — it is general information about how the product works. You are responsible for your own decisions and for understanding the risks before you act.

## Next

- [Liquidations](../trading/liquidations.md)
- [Audits](audits.md)
- [Oracle security](oracle-security.md)
- [Insurance fund](insurance-fund.md)
