# Changelog

## August 11, 2026 — Base mainnet launch

**Added**

* Trading is live on Base mainnet. Eight markets — EUR, GBP, JPY, GOLD, XAG, WBTC, WETH and TAO — all collateralized in USDC
* **Manage Liquidity** now links straight to the liquidity app from the interface
* Positions warn you when the mark price has crossed your liquidation price, and when displayed leverage has been capped
* A dismissible beta banner, so the notice stays out of your way once you've read it

**Changed**

* Available liquidity per side is now 25% of 0xMarkets LP TVL minus that side's open interest, so the number reflects what you can actually take
* Funding only accrues when there is open interest on both sides. A one-sided market no longer shows funding with no counterparty
* Pool and per-market TVL across **/pools**, **/stats** and the chart header now come from 0xMarkets LP
* Net rate is written as an unsigned magnitude — "pay 0.01%" rather than "pay -0.01%" — with a tooltip breaking out long, short and borrow components
* Effective leverage is capped in the display at each market's maximum (`>100x`, or `>200x` on forex), and net value no longer renders below $0
* Trade amounts fill to two decimals, extending to eight when rounding would move your size by more than 0.1%
* Markets list and the favorites bar redesigned — base symbols, per-market price decimals, and consistent token icons

**Fixed**

* The chart could crash on load when the TradingView library lost a race after unlock
* Order toasts now resolve correctly on fill and on cancel, including when events arrive out of order
* 24h volume showed a loading state indefinitely on quiet markets instead of zero
* Footer and social links now open in a new tab
