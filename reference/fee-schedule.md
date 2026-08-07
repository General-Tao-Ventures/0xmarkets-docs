# Fee schedule

Every cost of trading on 0xMarkets, in one place. This page is a lookup — each row links to the Trading page that explains the mechanism in full.

## Trading fee

Charged on your **position size**, both when you open and when you close. The rate depends on the asset class and on whether your trade improves or worsens the market's balance — the lower rate is for trades that bring open interest back toward balance, the higher rate for trades that push it further out.

| Asset class | Balancing trade | Imbalancing trade |
|---|---|---|
| **FX** | 0.015% | 0.025% |
| **Crypto** | 0.030% | 0.040% |
| **Commodities** | 0.020% | 0.030% |

Full explanation: [Fees](../trading/fees.md).

## Ongoing and per-order costs

| Cost | What it is | Page |
|---|---|---|
| **Funding fee** | Periodic payment between traders: the larger open-interest side pays the smaller side, with the rate scaling to the imbalance. Can be positive or negative for you. | [Funding & borrowing](../trading/funding-and-borrowing.md) |
| **Borrowing fee** | A per-position charge that accrues on your position size over time; the smaller open-interest side pays none. | [Funding & borrowing](../trading/funding-and-borrowing.md) |
| **Price impact** | Large trades that worsen the book's balance pay an impact cost; trades that improve it get price improvement. Capped at **±0.5%**. | [Price impact & slippage](../trading/price-impact-and-slippage.md) |
| **Network gas** | Normal Base network gas (in ETH) on the transactions you sign. Keeper execution gas is subsidised by the protocol — there's no separate keeper/execution fee charged to you. | [Fees](../trading/fees.md) |

## Where trading fees go

The trading fee is split across the protocol. These are the launch values and are adjustable by veAlpha governance:

| Destination | Share |
|---|---|
| **LP pool** | 50% |
| **veAlpha rewards** | 40% |
| **Treasury** | 10% |
| **Alpha buyback** | 0% |

Full detail: [Fees → Where trading fees go](../trading/fees.md).

## Where liquidation fees go

Liquidation fees are distributed separately from trading fees. This split is planned to come under governance control in a future release:

| Destination | Share |
|---|---|
| **Insurance pool** | 70% |
| **Alpha buyback** | 30% |

What a liquidation costs and how the fee is calculated: [Liquidations](../trading/liquidations.md).

## Next

- [Fees](../trading/fees.md)
- [Liquidations](../trading/liquidations.md)
- [Markets](markets.md)
