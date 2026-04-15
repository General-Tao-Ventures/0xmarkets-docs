# ALPHA Token

ALPHA is the native token of the 0xMarkets Liquidity Provider, which runs on the Cartha Subnet (SN35) on Bittensor. It is emitted by the network each epoch and distributed to the participants who keep 0xMarkets running — miners providing liquidity, validators executing liquidations, and traders generating volume.

ALPHA has two primary uses: it is a **yield-bearing asset** when locked into veALPHA, and it is the **unit of governance** that determines how the protocol allocates resources across markets.

***

## How ALPHA is Earned

ALPHA emissions are distributed across the ecosystem each epoch:

| Recipient         | Share | Description                                                      |
| ----------------- | ----- | ---------------------------------------------------------------- |
| LP Miners         | 31%   | Allocated by vault deposit score (time × amount × pool weight)   |
| Validators        | 41%   | Rewards for liquidation execution and subnet maintenance         |
| Incentive Pool    | 10%   | Trading leaderboards, IB rebates, airdrops, community programs   |
| Owner / Protocol  | 18%   | Protocol development and operations                              |

Miners earn their share passively — the longer and larger the USDC deposit, the greater the deposit score, and therefore the larger the ALPHA allocation.

***

## What You Can Do With ALPHA

**Lock for veALPHA** — the primary use case. Locking ALPHA gives you veALPHA, which entitles you to 40% of all trading fees paid in USDC, plus a vote on how ALPHA emissions are directed across markets. The longer you lock, the larger your share. See [Governance (veALPHA)](vealpha.md).

**Hold** — early holders who accumulate ALPHA through mining receive a larger position before the platform scales, which translates directly into a larger share of future USDC fee rewards when they eventually lock.

**Sell** — ALPHA is liquid and tradeable. The veALPHA mechanism creates a stablecoin-denominated value floor based on the trading fees the platform generates, providing a fundamental pricing anchor.

***

## Token Flow

The diagram below shows how ALPHA emissions and trading fees flow through the system:

<figure><img src="../.gitbook/assets/0xM_Tokenomics.png" alt=""><figcaption><p>ALPHA emission and fee distribution across the 0xMarkets ecosystem</p></figcaption></figure>

Key flows:
* **0xMarkets Liquidity Provider → LP Miners / Validators / Incentive Pool** via ALPHA emissions each epoch
* **0xMarkets → LP Miners** 50% of trading fees in USDC
* **0xMarkets → veALPHA stakers** 40% of trading fees in USDC
* **0xMarkets → Insurance Pool** 5% liquidation fee
* **veALPHA → 0xMarkets** governance over parameters and market weights
