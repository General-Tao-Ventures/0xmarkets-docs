# Managing positions

Once a position is open, you can adjust it without closing it. This page covers the four things you can do: change collateral, change size, set exit triggers, and read your position's live numbers.

## Add or remove collateral

You can deposit more USDC into an open position or withdraw some of it:

- **Adding collateral** lowers your effective leverage and moves your liquidation price further away — it makes the position safer.
- **Removing collateral** raises your effective leverage and moves your liquidation price closer — it frees up USDC but increases risk.

You cannot withdraw so much that the position would breach its maintenance margin; the interface enforces the limit.

## Increase or partially close

- **Increase** — add to your position size. The new size is filled at the current market price, so your average entry price moves toward the new fill.
- **Partial close** — close part of your position and realize that share of your PnL, leaving the rest open. Useful for taking some profit off the table or reducing risk while staying in the trade.

## Set stop-loss and take-profit

Attach exit triggers to an open position:

- **Take-profit (TP)** — automatically closes the position when the price reaches a level in your favor.
- **Stop-loss (SL)** — automatically closes the position when the price reaches a level against you, capping your loss.

TP and SL are executed by keepers when the trigger price is reached. They are the main tool for managing risk when you're not watching the market. See [Order types](order-types.md) for how triggers behave.

> A stop-loss is not a guarantee of an exact exit price. In a fast or gapping market the fill can be worse than the trigger level. It limits your exposure; it does not freeze your loss at the exact number.

## Read your position

Each open position shows live:

- **Size** and **direction** (long/short)
- **Collateral** and **effective leverage**
- **Entry price**, **mark price**, and **liquidation price**
- **Unrealized PnL** — what you'd make or lose if you closed now
- **Accrued borrowing fee** and **accrued funding** — ongoing costs (or credits) since you opened. See [Funding & borrowing](funding-and-borrowing.md).

Your unrealized PnL is shown net of fees accrued so far, so it reflects what you would actually receive on close.

## Next

- [Closing a trade](closing-a-trade.md)
- [Leverage & margin](leverage-and-margin.md)
- [Liquidations](liquidations.md)
