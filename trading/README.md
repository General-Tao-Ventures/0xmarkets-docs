# Trading

0xMarkets is a multi-asset perpetual futures exchange on Base. You trade FX, commodities, and crypto with leverage, using USDC as collateral, directly from your own wallet — no account, no KYC, no custody.

This section explains how trading works, end to end:

| Page | What it covers |
|---|---|
| [Opening a trade](opening-a-trade.md) | Long or short, size, leverage, collateral, and how your order is filled |
| [Managing positions](managing-positions.md) | Add or remove collateral, partial close, set stop-loss / take-profit |
| [Closing a trade](closing-a-trade.md) | Market close, triggers, and how PnL settles |
| [Order types](order-types.md) | Market, Limit, TP/SL, Stop Market, TWAP |
| [Leverage & margin](leverage-and-margin.md) | Max leverage per asset, the leverage ladder, and maintenance margin |
| [Liquidations](liquidations.md) | When a position is liquidated and what it costs |
| [Fees](fees.md) | Opening and closing fees by asset class |
| [Funding & borrowing](funding-and-borrowing.md) | The ongoing costs of holding a position |
| [Price impact & slippage](price-impact-and-slippage.md) | How your size affects your fill, and how to cap slippage |
| [Pricing & the oracle](pricing-and-oracle.md) | Where prices come from and how trades are priced |
| [Market hours](market-hours.md) | When each market trades |
| [PnL & profit settlement](pnl-and-settlement.md) | How profit and loss are calculated and paid |

## How it works in one paragraph

When you open a position, you are trading against a pool of liquidity supplied by **liquidity providers (LPs)** — the other side of every trade. The same person can be both a trader and an LP. Prices come from a real-time oracle, not an order book, so you always trade at the market price adjusted for the size of your trade. Your position stays open until you close it, it hits a stop, or it gets liquidated. Profit and loss settle in USDC.

> Nothing here is financial advice. Perpetual futures with leverage carry a high risk of loss. See [Risk disclosures](../security/risk-disclosures.md).
