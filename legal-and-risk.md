# Legal & risk

### Regulatory Status

0xMarkets is a decentralized protocol. It is **not licensed or registered** as a financial services provider in any jurisdiction. Users are responsible for determining whether participation is legal in their country of residence. Access may be restricted in certain regions due to local regulations.

### Trading Risks

* **Leverage risk:** Perpetual futures allow up to **500x leverage**. This magnifies both profits and losses. Even small price moves can liquidate positions and cause **total loss of margin**.
* **Market risk:** FX, commodities, and other RWAs are volatile. Prices may move sharply, especially in low-liquidity conditions.
* **Funding payments:** Traders may be required to pay recurring funding if holding imbalanced positions.

### Liquidity Provider Risks (Miners)

* **Capital at risk:** Miners deposit USDC into vaults. Losses can occur from bad debt, failed liquidations, or black-swan market moves.
* **Collateral requirements:** Maintaining $200k–$1M over time is required. Failure to do so may reduce rewards or disqualify participation.
* **Epoch lock-ups:** Deposits are committed for epochs; liquidity cannot always be withdrawn instantly.

### Validator Risks

* **Operational responsibility:** Validators must cross-verify oracles and execute liquidations. Missed or failed liquidations can result in **slashing of posted ALPHA collateral**.
* **Reputation and penalties:** Misbehavior or inactivity may reduce validator rewards or cause exclusion from the subnet.

### Liquidation & Insurance Risks

* **Liquidation exposure:** When margin is breached, a **10% liquidation fee** is applied. Traders may lose more than expected if markets gap suddenly.
* **Insurance pool limitations:** Although the pool is funded by liquidation fees and designed to cover black-swans or liquidity gaps, coverage is not guaranteed. In extreme cases, losses may exceed the pool’s capacity.

### Protocol & Smart Contract Risks

* **Smart contract vulnerabilities:** All DeFi protocols face risks of bugs, hacks, or exploits. Despite audits, no guarantee of absolute security exists.
* **Oracle risk:** Price feeds rely on multiple providers and validator checks. Manipulation or outages may still occur.
* **Systemic dependencies:** The Cartha Subnet (SN35) and Bittensor network are underlying dependencies; disruptions may impact 0xMarkets.

### Governance Risks

* **Concentration:** veALPHA governance is weighted by lock duration and token size. Large holders may exert outsized influence.
* **Parameter changes:** Governance may alter fee splits, vault emissions, or risk parameters. This may affect miner and trader incentives unpredictably.

### Treasury & Token Risks

* **Fee revenue variability:** Treasury income depends on trading volume, which may fluctuate significantly.
* **Token economics:** ALPHA price is market-driven and volatile. Rewards denominated in ALPHA may vary in real-world value.

### User Responsibility

Participation in 0xMarkets involves **high risk**. Users must:

* Understand leveraged trading and DeFi risks before engaging.
* Comply with applicable laws in their jurisdiction.
* Only risk capital they can afford to lose.

> Nothing in these documents constitutes financial advice. 0xMarkets, Cartha Subnet, or affiliated contributors bear **no liability** for user losses.
