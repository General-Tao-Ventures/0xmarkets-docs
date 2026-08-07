# FAQ

Common questions, grouped by topic. Each answer links to the page with the full story.

- [Getting started](#getting-started)
- [Trading](#trading)
- [Fees & costs](#fees-and-costs)
- [Providing liquidity](#providing-liquidity)
- [Epochs & rewards](#epochs-and-rewards)
- [Validators](#validators)
- [Token & governance](#token-and-governance)
- [Security & trust](#security-and-trust)

## Getting started

**What is 0xMarkets?**\
A decentralized, multi-asset perpetual futures exchange on Base. You trade FX, commodities, and crypto with leverage, using USDC as collateral, straight from your own wallet. Liquidity is supplied by liquidity providers (LPs) on the 0xMarkets Liquidity Engine (Bittensor Subnet 35). See [What is 0xMarkets](../getting-started/what-is-0xmarkets.md).

**What network is it on?**\
**Base** (Ethereum L2). You trade directly from your own wallet on Base.

**Do I need to sign up or pass KYC?**\
No. 0xMarkets is **non-custodial** — no account, no sign-up, no KYC. You connect your wallet and trade, and your funds stay in your control.

**What do I use as collateral?**\
**USDC**, on Base. All positions are backed by USDC and all profit and loss settle in USDC.

**What can I trade?**\
At Beta launch, nine markets across three asset classes: **FX** (EUR/USD, GBP/USD, USD/JPY), **commodities** (gold, silver, oil), and **crypto** (BTC, ETH, TAO) — all USD-quoted. The list expands as liquidity grows. See [Markets](markets.md).

## Trading

**How much leverage can I use?**\
Headline ceilings are **up to 500x on FX, 200x on commodities, 100x on crypto**. The leverage you actually get depends on your position size — a leverage ladder steps the cap down as positions grow. See [Leverage & margin](../trading/leverage-and-margin.md).

**How are prices determined?**\
From a real-time price **oracle**, not an order book. At Beta launch the primary feed is **Pyth Pro**, with **Chainlink Data Streams** as a secondary feed enabled shortly after. Your fill is the oracle price adjusted for the price impact of your trade size. See [Pricing & the oracle](../trading/pricing-and-oracle.md).

**When am I liquidated?**\
When your equity (collateral ± unrealized PnL, minus fees) falls to your **maintenance margin**. The higher your leverage, the higher that margin and the closer your liquidation price sits to your entry. See [Liquidations](../trading/liquidations.md).

**If I'm liquidated, do I lose everything?**\
Yes — a liquidation closes **100% of your margin**, with no partial refund. To exit earlier and keep what's left, use a [stop-loss](../trading/order-types.md). Full detail in [Liquidations](../trading/liquidations.md).

**Can I trade FX and commodities on weekends?**\
Generally no. **Crypto trades 24/7**, but **FX and commodities follow their real-world sessions** and pause on weekends, overnight breaks, and holidays. Positions you already hold stay open across closes; new orders won't execute until the session resumes. See [Market hours](../trading/market-hours.md).

## Fees & costs

**What fees will I pay as a trader?**\
A **trading fee** when you open and close (0.015%–0.040% of size, depending on asset class and trade direction), plus ongoing **funding** and **borrowing** while a position is open. See the [Fee schedule](fee-schedule.md).

**Is there a keeper or execution fee?**\
No separate one. You pay normal Base network gas (in ETH) on your own transactions; the keepers that execute your trades are subsidised by the protocol.

**How are trading fees distributed?**\
50% to the LP pool, 40% to veAlpha rewards, 10% to the treasury, 0% to Alpha buyback. These are the launch values and are adjustable by governance. See [Fees & rewards](../how-it-works/fees-and-rewards.md).

## Providing liquidity

**How do liquidity providers participate?**\
LPs (also called miners) deposit **USDC** into a vault for a specific market. Each vault is **isolated**, so the risk of one market stays contained to that market's vault. See [Providing Liquidity](../liquidity/README.md).

**Do LPs set or quote prices?**\
No. LPs supply **capital**; prices come from the oracle (Pyth Pro) and the on-chain price-impact model. LPs are the counterparty to trader PnL, not a pricing engine.

**What's the minimum to provide liquidity?**\
The minimum lock is **100,000 USDC** per position, committed for the lock term you choose (up to 365 days), with a 7-day cooldown on withdrawal. See [Become a Liquidity Provider](../liquidity/miner-guide.md).

**How do LPs earn?**\
Two independent streams: **trading-fee yield** (the LP pool's share of fees, realized as your vault share value rises) and **ALPHA emissions** (based on your deposit score — amount × lock duration). See [Fees & rewards](../how-it-works/fees-and-rewards.md).

**What are the risks of providing liquidity?**\
You take the other side of trader PnL, so you can lose when traders win, alongside outlier moves, concentration, and adverse selection. See [Risk disclosures](../security/risk-disclosures.md).

## Epochs & rewards

**What is an epoch?**\
A weekly reward period running **Friday 00:00 UTC to Thursday 23:59 UTC**. LP positions are frozen at the start of each epoch, and rewards are calculated from that snapshot. See [Weekly Epochs](../how-it-works/weekly-epochs.md).

**When should I lock my funds?**\
Lock by **Thursday 23:00 UTC** (or earlier) to be included in the next epoch. The indexer needs up to ~15 minutes to detect your position on Base, so give yourself buffer. Positions locked after Friday 00:00 UTC won't earn until the following week.

**When do I start earning rewards?**\
After your first epoch freeze. When you lock, you're added to the upcoming epoch; at the next Friday 00:00 UTC freeze your position becomes active and starts earning.

**What if I add more funds mid-epoch?**\
Top-ups during an epoch go into a pending state and don't count toward your current score — they're included in the next epoch's calculation. See [Top Up & Extend Lock](../liquidity/how-to-top-up-and-extend.md).

**What share of ALPHA emissions do LPs receive?**\
LPs (miners) receive **31% of ALPHA emissions**, distributed pro-rata by deposit score.

## Validators

**What do validators do?**\
Validators help secure the 0xMarkets Liquidity Engine: they score LPs each epoch (by locked USDC × lock duration), set Bittensor weights that direct emissions, and support liquidation execution. See [Validator Guide](../liquidity/validator-guide.md).

**What do validators earn?**\
The validator share of ALPHA emissions — **41% of total emissions** — which flows to the Alpha staked to the validator as the native validator yield holders earn by staking.

## Token & governance

**How will governance work?**\
Governance is rolling out progressively. You stake Alpha to mint **veALPHA**, which votes on how the exchange distributes its trading fees — the split between the LP pool, staking pool, and treasury, within set floors. LP pool weights are the next step. See [Staking & Governance (veALPHA)](../alpha-token/vealpha.md).

**What is ALPHA?**\
The token of the 0xMarkets Liquidity Engine, used for emissions to LPs and validators, for staking rewards (a share of trading fees), and for veALPHA governance. See [Alpha Token](../alpha-token/README.md).

**How are ALPHA emissions distributed across the network?**\
**41% to validators, 31% to miners/LPs, 18% to the subnet owner, and 10% to the incentive pool.**

## Security & trust

**Is 0xMarkets audited?**\
An initial audit by **Hashlock** (covering the liquidity-engine infrastructure) is complete, and a comprehensive **end-to-end** review with **HackenProof** is in progress. See [Audits](../security/audits.md).

**What is the insurance fund?**\
A per-market backstop at the exchange layer, funded partly by liquidation fees (70% of each liquidation fee is directed to it). It absorbs stress events but is **not a guarantee** on your position. See [Insurance fund](../security/insurance-fund.md).

**How are liquidations and their fees handled?**\
Liquidations are triggered by your maintenance margin (not a flat fee) and the resulting liquidation fee is directed **70% to the insurance pool / 30% to Alpha buyback**. See [Liquidations](../trading/liquidations.md).

**What does "Beta" mean here?**\
0xMarkets is live and fully functional, and actively being refined as it matures. As with any newer platform, occasional issues can occur and some parameters are tuned over time. Treat the live interface as the source of truth for current values.

**Is there a referral program?**\
A referral program for introducing brokers and affiliates is **coming soon** — a share of referred traders' fees goes to their referrer. See [Referrals](../referrals.md).

## Next

- [Markets](markets.md)
- [Fee schedule](fee-schedule.md)
- [Glossary](glossary.md)
- [Providing Liquidity](../liquidity/README.md)
