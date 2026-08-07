# Alpha Token

Alpha is the native token of the **0xMarkets Liquidity Engine**, which runs as **Bittensor Subnet 35 (SN35)**. It is emitted by the network each epoch and distributed to the participants who keep 0xMarkets running — liquidity providers (miners) supplying USDC, validators supporting liquidations, and the protocol itself.

Alpha has two primary roles: it is a **reward-bearing asset** — holding it earns validator yield, and staking it earns a share of exchange trading fees — and it is the **unit of governance**, which veALPHA holders use to set how the protocol distributes its fee revenue. (veALPHA governance is rolling out progressively — see below.)

***

## How Alpha is earned

Alpha emissions are distributed across the network each epoch as follows:

| Recipient | Share | What it's for |
|---|---|---|
| **Validators** | 41% | The validator emission share — accrues to Alpha holders who stake (the native **validator yield** earned simply for holding and staking Alpha). |
| **Liquidity providers (miners)** | 31% | Allocated by **deposit score** (locked amount × time). The longer and larger the USDC deposit, the larger the Alpha allocation. |
| **Subnet owner** | 18% | Protocol development and operations. |
| **Incentive pool** | 10% | Flexible funding for ecosystem incentives (trading leaderboards, IB rebates, airdrops, community programs). |

The validator share is what makes simply **holding Alpha** productive: stake it and you earn that native yield, then stake on 0xMarkets to add a USDC share of trading fees on top. See [Staking & Governance (veALPHA)](vealpha.md).

***

## What you can do with Alpha

**Stake for veALPHA** — the primary use case. Staking Alpha on 0xMarkets earns you a share of trading fees (paid in USDC) and mints you veALPHA, which carries a vote on how the exchange distributes those fees (LP pool weights coming next). The larger and longer your stake, the larger your share and your vote. See [Staking & Governance (veALPHA)](vealpha.md).

**Hold** — accumulating Alpha early, through mining, builds a position before the platform scales, which translates into a larger share of future USDC fee rewards once you stake.

**Trade** — Alpha is liquid and tradeable. The veALPHA mechanism is designed to anchor Alpha's value to the USDC trading fees the platform generates, giving the token a fundamental, fee-based reference point.

***

## How value flows

The token economy has two distinct flows:

- **Alpha emissions** — minted by the 0xMarkets Liquidity Engine (SN35) each epoch and distributed **41% validators, 31% miners, 18% subnet owner, 10% incentive pool**.
- **Trading fees (USDC)** — paid by traders on the exchange and split **50% to the LP pool, 40% to the staking pool, 10% to treasury, 0% to Alpha buyback** (launch values, governance-adjustable within set floors).
- **Liquidation fees** — routed **70% to the insurance pool, 30% to Alpha buyback** (intent; planned to come under governance later).
- **Governance** — veALPHA holders set how trading fees are distributed across the LP pool, staking pool, and treasury (within floors), with LP pool weights as the next step.

See [Fees & rewards](../how-it-works/fees-and-rewards.md) for the protocol-level fee detail and [Fees](../trading/fees.md) for what a trade costs.

## Next

- [Governance (veALPHA)](vealpha.md)
- [Fees & rewards](../how-it-works/fees-and-rewards.md)
- [Weekly epochs](../how-it-works/weekly-epochs.md)
