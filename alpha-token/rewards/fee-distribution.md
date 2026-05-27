# Fee Distribution

Fees on 0xMarkets are paid in **USDC** and split across the participants that make the protocol work. There are two fee streams: **trading fees** from normal trading activity, and **liquidation fees** from margin breaches.

## Trading Fees

Every market charges open and close fees, plus funding and borrowing where applicable. The collected USDC is split:

| Share | Recipient | Rationale |
|-------|-----------|-----------|
| **50%** | Miners (LPs) | Compensation for providing liquidity backing the market |
| **40%** | veALPHA stakers | Pro-rata by ve balance — long-term aligned holders |
| **10%** | Protocol treasury | Operations, security, ecosystem reserves |

LP shares are paid into the **market vault** the LP backs — so cvBTC LPs earn from BTC/USD volume, cvEUR LPs earn from EUR/USD volume, etc. This means LP yield tracks the volume of the specific markets you've chosen.

## Funding & Borrowing Fees

* **Funding** — the side with larger open interest pays the side with smaller open interest, incentivizing market balance. Funding does not accrue to LPs; it transfers between traders.
* **Borrowing** — only the side with larger open interest pays. Of collected borrowing fees, **63% goes to LPs** and **37% goes to the protocol**. Borrowing rates scale with utilization, so deep but heavily-used vaults compound yield.

The protocol may also allocate a share of funding payments — current settings are governance-controlled via veALPHA fees voting.

## Swap Fees

A fee applies when swapping tokens. The rate depends on the token pair and the current pool balance. Swap fees follow the same trading-fee split (50% LPs / 40% veALPHA / 10% protocol).

## Liquidation Fees

When a trader's margin is breached, a **10% fee** on the position's collateral is charged at liquidation, split:

| Share | Recipient | Purpose |
|-------|-----------|---------|
| **20%** | Validators | Compensation for executing the liquidation |
| **50%** | Insurance pool | Backstops bad debt and black-swan losses |
| **30%** | ALPHA buyback & burn | Deflationary pressure on ALPHA supply |

The insurance-pool share is the most important LP-side protection: it's a continuously-funded reserve sized to absorb shortfalls before any vault capital is touched. See [Liquidations](../../trading/liquidations.md) and [Risk Management](../../cartha/risk-management.md) for the full picture.

## Price-Impact Rebates

When negative price impact exceeds a market's cap, the excess accrues to the trader as a **claimable rebate** — not a fee anywhere in the distribution table. Rebates become claimable after ~5 days under the **Claims** tab.

## Distribution Cadence

* **Trading fees to LPs** — accrue continuously into the vault NAV; you realize them on unlock
* **Trading fees to veALPHA** — paid pro-rata per epoch, claimable from the governance interface
* **Trading fees to treasury** — accrue to the protocol multisig
* **Liquidation fees** — settled on each liquidation event
* **ALPHA buyback & burn** — funded continuously from the 30% liquidation-fee allocation

## Claiming

* **LPs**: USDC fees compound into your vault position; settle at withdrawal
* **veALPHA stakers**: claim fee share per epoch from the governance UI
* **Validators**: liquidation fees pay on each successful execution
* **Traders (price-impact rebates)**: claim from the **Claims** tab after the ~5-day settlement window

See the [FAQ](../../faq.md) for additional fee questions and [Trading Fees](../../trading/fees.md) for the trader-side fee mechanics.
