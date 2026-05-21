# Pricing

0xMarkets is oracle-priced. Every market quote, fill, liquidation, and trigger-order execution references the **oracle mark price**, not an internal order book.

## Pyth Network as the Primary Oracle

Prices stream from [Pyth Network](https://pyth.network/), which aggregates first-party data from over 100 exchanges and market makers. Each market is mapped to a Pyth feed maintained for that asset.

* **Sub-second updates** — prices update continuously while the underlying market is open
* **Confidence intervals** — Pyth publishes a price *and* an uncertainty band; 0xMarkets uses both to gate execution
* **First-party publishers** — data comes directly from the exchanges and market makers producing it, not scraped second-hand

Market hours track Pyth feed availability — see [Market Hours](market-hours.md).

## Mark Price vs Trade Price

* **Market orders** fill at the current oracle price when a keeper picks the order up
* **Limit, stop-market, TP/SL, and TWAP orders** trigger when the oracle price crosses your specified level — these are *not* passive order-book orders (see [Order Types](order-types.md))
* **Funding and borrowing** accrue against the mark price
* **Liquidations** trigger when the mark price moves margin below the maintenance threshold

## Validator Cross-Verification

Cartha validators independently cross-verify oracle prices and are the actors responsible for executing liquidations. This second layer protects against feed manipulation: a single anomalous price tick should not move a market or trigger spurious liquidations.

* Validators consume the same Pyth feeds and confirm price consistency before acting
* Fallback oracle paths exist for reliability when a primary feed degrades
* Slashing penalties apply to validators that miss or mis-execute liquidations — see [Risk Management](../cartha/risk-management.md)

## Price Impact

Price impact is *not* baked into the fill price for order entry. Instead, it accrues as a position attribute and settles when the position decreases or closes. This means market orders execute at the clean oracle price, with impact tracked separately. See [Trading Fees › Price Impact](fees.md#price-impact) for the full mechanics.

## When the Oracle Goes Quiet

During scheduled market closures (e.g. FX weekend, metals maintenance window), feeds pause. The exchange does not accept fills or execute liquidations during these windows — see [Market Hours](market-hours.md) for details.
