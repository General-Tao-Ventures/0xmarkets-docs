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

**What rewards do miners earn?**

* **60% of trading fees** from the protocol
* **ALPHA emissions**, based on a time-weighted deposit score (amount × duration)

**What do validators do?**\
They cross-verify external price feeds from multiple oracle providers, prevent manipulation, and act as executors for liquidations

**How are validators incentivized?**\
Validators earn **20% of liquidation fees** and may post ALPHA collateral to participate. They can also be slashed if they miss liquidation duties

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

**What funds the treasury?**

* **10% of trading fees**
* Optional share of funding payments

**What is the treasury used for?**\
Treasury allocations are governance-controlled and may fund development, growth, or ecosystem initiatives
