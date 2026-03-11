# Market Hours

0xMarkets offers perpetual trading on FX, Metals, Commodities, and Crypto. FX, Metals, and Commodities follow traditional market hours, while Crypto markets are open 24/7.

## Trading Hours by Asset Class

| Asset Class | Opening Hours | Exceptions |
|-------------|--------------|------------|
| FX | Sunday 5PM ET to Friday 5PM ET | Trading continues during most US holidays |
| Metals | Sunday 6PM ET to Friday 5PM ET | Daily maintenance window from 5PM ET to 6PM ET, Monday to Thursday. Spot gold and silver trading also follow [CME holiday closures](https://www.cmegroup.com/tools-information/holiday-calendar.html) |
| Commodities | Sunday 6PM ET to Friday 5PM ET | Daily maintenance window from 5PM ET to 6PM ET. Follow [CME holiday closures](https://www.cmegroup.com/tools-information/holiday-calendar.html) |
| Crypto | 24/7 | N/A |

Market hours coincide with price feed availability from [Pyth](https://docs.pyth.network/price-feeds/core/market-hours).

## What Happens During Market Closures

The exchange does not accept orders and will not execute liquidations outside of market hours for the relevant asset classes.

If an order is submitted during a market closure, the order will appear to be processing but will ultimately be rejected by the exchange. The keeper receives no price data from the oracle during closures, which prevents any order execution or liquidation processing.

## Key Details

- **FX pairs** (EUR/USD, GBP/USD, USD/JPY): Closed from Friday 5PM ET to Sunday 5PM ET.
- **Metals** (GOLD/USD): Closed from Friday 5PM ET to Sunday 6PM ET, plus a daily maintenance window from 5PM to 6PM ET Monday through Thursday.
- **Commodities** (WTI/USD): Same schedule as Metals.
- **Crypto** (WBTC/USD, WETH/USD): Always open.
