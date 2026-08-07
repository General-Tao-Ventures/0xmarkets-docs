# Litepaper

## Abstract

0xMarkets is a **multi-asset decentralized perpetual futures exchange** on **Base**, offering leveraged exposure to **FX, commodities, and crypto** in a permissionless way. All markets are **USDC-collateralized**.

The exchange is live in **Beta** — fully functional, but still maturing. Expect ongoing refinement of parameters and the occasional rough edge as the system hardens.

What makes 0xMarkets different is where its liquidity comes from. Instead of a single house treasury, liquidity is supplied by independent providers ("miners") on **Bittensor Subnet 35 (SN35)** — the **0xMarkets Liquidity Engine**. These providers commit USDC to per-market vaults and earn for doing so. Crucially, they supply **capital**, not prices: trades are priced by the **Pyth Pro** oracle plus on-chain price impact, never quoted by individual liquidity providers.

## Architecture at a glance

- **Collateral:** USDC on Base across every market.
- **Liquidity:** one vault per market, isolating risk between markets. Vaults are funded by LPs on SN35.
- **Pricing:** the **Pyth Pro** oracle provides the reference price; on-chain **price impact** adjusts execution based on how a trade shifts open-interest balance. Liquidity providers do **not** quote or price trades.
- **Leverage:** headline maximums of **FX up to 500x, commodities up to 200x, crypto up to 100x**, applied through a notional ladder (max leverage shrinks as position size grows). See [Leverage & margin](trading/leverage-and-margin.md).
- **Settlement:** all PnL is settled in USDC.

## The 0xMarkets Liquidity Engine (SN35)

The **0xMarkets Liquidity Engine** is the decentralized liquidity backbone for the exchange, running as **Bittensor Subnet 35**. It exists to deepen and decentralize the capital that traders trade against.

### Liquidity providers (miners)

- **Supply USDC** into per-market vaults, choosing which markets/vaults to back.
- **Commit for weekly epochs** — a 7-day cycle (Friday 00:00 UTC → Thursday 23:59 UTC). See [Weekly epochs](how-it-works/weekly-epochs.md).
- **Earn two ways:**
  - A share of **trading fees** (in USDC).
  - **Alpha emissions**, allocated by a deposit score (a function of locked amount and time).
- **Do not price trades.** Providers contribute capital only; pricing is handled by the oracle and on-chain impact.

### Validators

- Run on the subnet and **monitor markets for liquidation conditions**, helping execute liquidations and maintain the network.
- Earn **Alpha emissions** for this work.

### Insurance fund

- A **per-market insurance fund** sits at the exchange (DEX) layer as a backstop for extreme events.
- It is funded over time by a configurable share of fees, and can inject capital back into a market's pool under severe drawdown. See [Insurance fund](security/insurance-fund.md).

## The exchange (DEX)

### For traders

- Permissionless access to leveraged perps on FX, commodities, and crypto, all **USDC-collateralized**.
- A transparent fee structure — a trading fee on open and close, plus ongoing funding and borrowing. See [Fees](trading/fees.md).
- Liquidations are **maintenance-margin-driven**, not a flat percentage. See [Liquidations](trading/liquidations.md).

### Trading-fee distribution

Trading fees are split (these are launch values, adjustable by veALPHA governance within set floors):

| Destination | Share | Floor |
|---|---|---|
| LP pool (liquidity providers) | 50% | 30% |
| Staking pool (veALPHA) | 40% | 30% |
| Treasury | 10% | 10% |
| Alpha buyback | 0% (reserved) | — |

### Liquidation-fee distribution

Liquidation fees are directed (intent):

| Destination | Share |
|---|---|
| Insurance pool | 70% |
| Alpha buyback | 30% |

*This distribution is set by the protocol and is planned to come under governance control in a future release.*

## The Alpha token

**Alpha** is the network's native token, emitted each epoch by the subnet. Its primary uses are:

- **Staking & veALPHA** — staking Alpha (via Bittensor conviction) earns a share of USDC trading fees and mints veALPHA for governance over how those fees are distributed. Governance is rolling out progressively. See [Staking & Governance (veALPHA)](alpha-token/vealpha.md).
- **Incentives** — Alpha emissions reward the LPs and validators who keep the network running.

Emissions are split across network participants: **41% validators, 31% miners/LPs, 18% subnet owner, 10% incentive pool**.

See [Alpha Token](alpha-token/README.md) for detail.

## Next

- [How it works](how-it-works/README.md)
- [Weekly epochs](how-it-works/weekly-epochs.md)
- [Fees & rewards](how-it-works/fees-and-rewards.md)
- [Alpha Token](alpha-token/README.md)
