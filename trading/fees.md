# Fees

## Open and Close Fees

A percentage fee is charged when opening or closing a position.

* Fee rates vary by market and are displayed in the trade confirmation before you submit the order
* Both opening and closing a position incur this fee

## Price Impact

Price impact is applied when closing or decreasing positions, not at entry.

* Impact is calculated based on changes to the open interest imbalance in the market
* **Positive impact** (favorable to the trader) — occurs when the trade improves market balance by reducing the imbalance between long and short open interest
* **Negative impact** (unfavorable to the trader) — occurs when the trade worsens market balance by increasing the imbalance
* Each market has caps on both positive and negative price impact
* For position increases, there is no price impact — orders fill at the mark price. The impact is stored internally and settled when the position is decreased or closed.

## Price Impact Rebates

When negative price impact exceeds the market cap, the excess becomes a claimable rebate.

* Rebates become claimable after approximately five days
* Accrued rebates can be viewed and claimed under the **Claims** tab
* Price impact rebates for closing trades are also claimable under the Claims tab

## Execution Fee

The execution fee (also called the network fee) covers the gas cost for keepers to execute your order on-chain.

* The displayed max network fee overestimates the likely cost
* After execution, any excess fee is automatically refunded to your account
* This is a blockchain gas cost, not a fee specific to 0xMarkets, and does not reduce your position collateral

## Network Fee Buffer

An adjustable buffer added to the max network fee, configurable in **Settings**.

* Guards against gas price spikes between order submission and execution
* Higher buffer means more reliable execution but a larger upfront cost (excess is refunded)
* Default buffer is 30%

## Funding Fees

Funding rates adjust based on the long/short open interest imbalance in each market.

* The side with larger open interest pays the side with smaller open interest, incentivizing market balance
* Rates adjust adaptively: increasing when the imbalance is high, holding steady when moderate, and decreasing when low
* Funding accrues continuously and settles when positions are modified or closed

## Borrowing Fees

Only the side with larger open interest pays borrowing fees.

* Rates increase with utilization — higher open interest relative to pool size means higher fees
* Of collected borrowing fees, 63% goes to liquidity providers and 37% goes to the protocol

## Swap Fees

A fee is charged when swapping tokens.

* The fee rate depends on the token pair and the current pool balance
