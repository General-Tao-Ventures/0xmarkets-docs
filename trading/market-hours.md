# Market hours

Different asset classes trade on different schedules, mirroring the real-world markets that price them. This affects when you can open and close positions on 0xMarkets.

## Crypto — 24/7

Crypto markets (BTC, ETH, TAO) trade **around the clock, every day**. Prices stream continuously, so you can open, manage, and close these positions at any time.

## FX — 24/5

FX markets (EUR, GBP, JPY) follow the global foreign-exchange week:

- **Open:** Sunday **5:00 PM New York time (ET)**
- **Close:** Friday **5:00 PM ET**
- Trades continuously through the week, with no daily break.

In UTC that's roughly **Sunday 22:00 → Friday 22:00**, shifting about an hour earlier (21:00) during US daylight-saving months.

## Commodities — global session with a daily break

Commodity markets (gold, silver, oil) follow the global metals and energy session:

- **Open:** Sunday **6:00 PM ET**
- **Close:** Friday **5:00 PM ET**
- **Daily break:** a 60-minute pause each day from **5:00 PM to 6:00 PM ET** (Monday–Thursday).

In UTC that's roughly **Sunday 23:00 → Friday 22:00**, again shifting about an hour with US daylight saving.

## How hours are enforced

0xMarkets does **not** hard-code a trading calendar in its contracts. Instead, market availability **follows the oracle**: when an underlying real-world market is closed (overnight breaks, weekends, holidays), its [oracle price](pricing-and-oracle.md) stops updating, and the exchange rejects stale prices. In practice this means:

- You can trade FX and commodities during their normal sessions, when fresh prices are flowing.
- During a weekend close, a daily break, or a market holiday, new orders on those markets will not execute until the session resumes and the oracle updates again.
- Positions you already hold remain open across these closes.

> The hours above are the standard sessions of the underlying markets. Because availability is driven by the live data feed rather than a fixed calendar, the exact moments trading pauses and resumes track the oracle, not a hard-coded schedule.

## Toward 24/7 markets

Over time, 0xMarkets intends to extend more markets toward **24/7 availability** — including FX and commodities — as the quality and reliability of the underlying data sources allow. Round-the-clock trading on a market will be enabled only where the data feed can be trusted to deliver continuous, accurate prices outside traditional sessions. Until then, these markets follow the standard hours above.

## Price gaps

Markets that close can **gap** — reopen at a price meaningfully different from where they closed, if news broke while they were shut. This matters for two reasons:

- A **stop-loss** set inside the gap may fill at the reopening price, which can be worse than your trigger level. Stops limit exposure; they don't guarantee an exact exit.
- A position held over a weekend or break can move sharply at the reopen before you can react.

If you hold leveraged FX or commodity positions over a market close, size them with gap risk in mind.

## Next

- [Pricing & the oracle](pricing-and-oracle.md)
- [Order types](order-types.md)
- [Liquidations](liquidations.md)
