# Order Types

## Market Orders

Market orders execute immediately at the current oracle price.

* A keeper picks up and executes the order on-chain after submission
* Best for entering or exiting positions quickly when price precision is less important than speed

## Limit Orders

Limit orders trigger when the oracle price reaches your specified trigger price.

* **Long limits** trigger when the oracle price falls to or below the trigger price
* **Short limits** trigger when the oracle price rises to or above the trigger price
* Unlike traditional exchange limit orders, these are not passive orderbook orders — keepers execute them when the oracle price matches the trigger condition
* Fast price movements can cause the oracle to skip past your trigger price, preventing execution

## Take-Profit and Stop-Loss Orders

Take-profit (TP) and stop-loss (SL) orders automatically close positions at specified oracle price levels.

* **Take-Profit Long** — triggers when the oracle price rises to or above the trigger price
* **Take-Profit Short** — triggers when the oracle price falls to or below the trigger price
* **Stop-Loss Long** — triggers when the oracle price falls to or below the trigger price
* **Stop-Loss Short** — triggers when the oracle price rises to or above the trigger price

## Auto-Cancel TP/SL

When enabled, TP/SL orders automatically cancel when their associated position is fully closed.

* Prevents orphaned orders from triggering unexpectedly after a position has been closed by other means
* Only applies to newly created TP/SL orders after the setting is enabled — existing orders are not affected
* There is a limit on the number of active auto-cancelable orders per position

## Stop-Market Orders

Stop-market orders increase or open positions when the oracle price reaches a trigger level.

* **Long positions** — trigger when the oracle price rises above the stop price
* **Short positions** — trigger when the oracle price falls below the stop price
* Used to enter positions on breakouts or momentum moves

## TWAP Orders

TWAP (Time-Weighted Average Price) orders split large orders into multiple smaller parts distributed over time.

* Minimizes price impact for large position changes
* Configure the duration and number of parts (2-30) — the system calculates the frequency and size per part
* Recommended for orders exceeding $1,000,000 with negative price impact above 0.2%
* Implemented at the application layer by grouping standard limit orders with time-gated activation

## Max Leverage

Each market has a maximum allowed leverage that decreases as total open interest increases.

* This mechanism protects against price impact gaming via high-leverage positions
* The interface warns when max leverage would be exceeded
* **Position increases** — orders may be rejected if max leverage is exceeded
* **Position decreases** — orders can still execute, but collateral within the position may not be reduced

## Execution Guarantees

Limit, Stop-Market, TWAP, and TP/SL orders do not have guaranteed execution.

> Orders may fail if the oracle price never reaches the trigger, there is insufficient liquidity, max leverage is exceeded, or the position becomes liquidatable before execution.
