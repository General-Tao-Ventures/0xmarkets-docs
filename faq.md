# FAQ

**What is 0xMarkets?**\
0xMarkets is a decentralized FX perpetual futures exchange (Perp DEX) where traders can access currencies, commodities, and other RWAs with leverage up to 500x. Liquidity is powered by the Cartha Subnet (SN35), built on Bittensor, where miners act as liquidity providers (LPs)

**What assets are supported?**\
Initially major FX and Crypto pairs and Gold, expanding to other commodities, crypto and more real-world assets (RWAs)

**What collateral is used?**\
Only **USDC** is accepted as collateral across all markets

**How much leverage can I use?**\
Up to **500x leverage** on supported markets

**Do I need permission to trade?**\
No. Onboarding is fully **permissionless**

**What fees will I pay?**\
A fixed trading fee, plus possible funding payments depending on long/short imbalances

**How do miners participate?**\
Miners deposit USDC into vaults specific to each market. Each vault is isolated, so risk stays within that market

**What are the minimum requirements?**\
Miners must maintain **$200k–$1M** USDC collateral over time and commit funds for epoch durations

**What is an epoch?**\
An epoch is a weekly reward period running from **Friday 00:00 UTC to Thursday 23:59 UTC**. Miner positions are frozen at the start of each epoch, and rewards are calculated based on this frozen snapshot. See [Weekly Epochs](how-it-works/weekly-epochs.md) for details.

**When should I lock my funds?**\
Lock by **Thursday 23:00 UTC** (or earlier) to ensure inclusion in the next epoch. The indexer needs up to 15 minutes to detect your position on Base chain, so give yourself buffer time. Positions locked after Friday 00:00 UTC won't earn rewards until the following week.

**When do miners start earning rewards?**\
After your first epoch freeze. When you lock funds, you're added to the "upcoming epoch." At the next Friday 00:00 UTC freeze, your position becomes "active" and starts earning rewards.

**What if I add more funds mid-epoch?**\
Top-ups during an epoch go into a pending state and don't count toward your current score. They'll be included in the next epoch's reward calculation.

**What rewards do miners earn?**

* **31% of ALPHA emissions**, based on deposit score (amount × lock duration × pool weight)
* **50% of trading fees** from the protocol

**What is the incentive pool?**

* **10% of ALPHA emissions** allocated to an incentive pool for airdrops and rewards
* Currently used for trader leaderboards and IB (Introducing Broker) rebates
* Can be used to incentivize any party in the ecosystem
* Track rewards at [cartha.finance/leaderboard](https://cartha.finance/leaderboard)

**What rewards do validators earn?**

* **41% of ALPHA emissions** for subnet maintenance and liquidation execution
* **20% of liquidation fees** (in USDC) for successful executions

**When do liquidations happen?**\
When a trader’s margin requirements are breached, their position is liquidated automatically

**How are liquidation fees distributed?**\
A **10% fee** is charged, split:

* 20% to validators
* 50% to the insurance pool
* 30% to ALPHA buyback & burn

**What is the insurance pool?**\
Funded via liquidation fees, it covers black-swan events and liquidity gaps. Deployment is governance-controlled

**How does governance work?**\
Lock ALPHA to receive **veALPHA**. veALPHA holders direct emissions and adjust key parameters

**What votes can veALPHA holders cast?**

* **Alpha Voting:** Decide which vaults receive emissions
* **Fees Voting:** Adjust fee splits and protocol parameters

**Do longer locks matter?**\
Yes. Longer ALPHA locks = more voting weight and a larger share of protocol fees

**What do validators do?**\
They cross-verify external price feeds from multiple oracle providers, prevent manipulation, and execute liquidations. They can be slashed if they miss liquidation duties

**How are trading fees distributed?**

* **50%** to miners (LPs) - liquidity providers
* **40%** to veALPHA stakers - pro-rata by ve balance
* **10%** to protocol treasury

**How are ALPHA emissions distributed?**

* **31%** to miners (LPs)
* **41%** to validators
* **10%** to incentive pool (airdrops and ecosystem rewards)
* **18%** owner emissions (protocol development)
