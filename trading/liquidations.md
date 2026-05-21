# Liquidations

Liquidations protect the protocol — and the liquidity pool behind each market — from positions that can no longer cover their losses. This page covers liquidations from the **trader's** point of view. For the validator side, see [Validation](../validation/README.md). For LP exposure to liquidation risk, see [Risk Management](../cartha/risk-management.md).

## When a Position Is Liquidated

A position becomes liquidatable when its **margin falls below the maintenance margin requirement** for its market. This happens when:

* The mark price moves against the position
* Accrued **funding** or **borrowing** fees eat into collateral
* Realized **price impact** at close is large enough to drop margin below the threshold

Each market has its own maintenance margin factor, calibrated to the asset's volatility and the leverage tier you opened the position at.

## The Liquidation Lifecycle

1. **Margin breach detected** — validators monitor every open position against the live oracle price
2. **Liquidation submitted** — the first validator to detect the breach submits the liquidation on-chain
3. **Position closed** — remaining collateral covers losses and fees; any residual returns to the trader
4. **Liquidation fee applied** — a **10% fee** on the position's collateral at liquidation, split:
   * **20%** → validators (the actor who executed)
   * **50%** → insurance pool (backstops black-swan losses, governance-controlled)
   * **30%** → ALPHA buyback & burn

## Avoiding Liquidation

* **Watch margin ratio**, not just price — funding can erode collateral even on a flat position
* **Top up collateral** on an existing position before the maintenance margin is hit
* **Reduce leverage** as open interest grows — max leverage decreases as a market fills up (see [Order Types › Max Leverage](order-types.md#max-leverage))
* **Use stop-loss orders** to close out before the maintenance threshold; SL execution is not guaranteed in fast markets, but it's a better floor than nothing
* **Be aware of market closures** — FX, metals, and commodities pause overnight and weekends. Open positions stay open across closures, but you cannot manage them until the feed reopens

## The Insurance Pool

When a liquidation closes too late to cover losses in full — a "bad debt" event during extreme volatility — the **insurance pool** absorbs the shortfall before any LP capital is touched.

* Funded directly from the 50% liquidation-fee allocation
* Deployment is governance-controlled (veALPHA holders vote on backstop policy)
* Sized to handle expected tail events; black-swan scenarios beyond the pool are documented in [Legal & risk](../legal-and-risk.md)

## Trader Outcomes

| Scenario | What you keep |
|----------|---------------|
| Liquidation with collateral remaining | Residual collateral returns to your account after fees |
| Liquidation that fully exhausts collateral | Position closes; insurance pool covers any shortfall |
| Closed via stop-loss before liquidation | Standard close — only trading fees and accrued funding/borrowing apply |

> Liquidations are unrecoverable. If you regularly trade near max leverage, monitor your positions actively or use stop-losses.
