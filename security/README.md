# Security

Security at 0xMarkets is a continuous program — formal audits, ongoing monitoring, validator-enforced execution integrity, and a maintained disclosure channel.

## Sections

* [Audits](../cartha/security-audit.md) — completed audits, scope, and reports

## Audit Status

| Component | Auditor | Date | Rating |
|-----------|---------|------|--------|
| Cartha smart contracts | [Hashlock](https://hashlock.com/audits/cartha) | January 2026 | **Secure** |

Full audit report: [PDF on hashlock.com](https://hashlock.com/wp-content/uploads/2026/02/Cartha-Smart-Contract-Audit-Report-Final-Report-v5.pdf).

## Defense in Depth

Security on 0xMarkets is not just smart-contract audits. The protocol relies on multiple independent layers:

| Layer | What it protects against |
|-------|--------------------------|
| **Smart-contract audits** | Logic flaws and edge-case vulnerabilities in vault and core contracts |
| **Oracle redundancy** | Single-feed failures or anomalous ticks (multiple Pyth publishers + fallback paths) |
| **Validator cross-verification** | Manipulated or stale oracle data being acted on |
| **Validator slashing** | Validators going offline or skipping duty (they post ALPHA collateral) |
| **Insurance pool** | Bad-debt events that exceed position collateral |
| **Vault isolation** | One market's losses contaminating other markets |
| **Lock + cooldown** | Short-term gaming of epoch rewards |

See [Pricing](../trading/pricing.md), [Liquidations](../trading/liquidations.md), and [Risk Management](../cartha/risk-management.md) for how these layers compose.

## User-Side Best Practices

* **Verify contract addresses** before interacting (canonical list in [Cartha overview](../cartha/README.md#smart-contracts))
* **Keep private keys secure** — hardware wallets recommended for large positions
* **Start small** when trying new features or markets
* **Monitor positions regularly** at [liquidity.0xmarkets.io/positions](https://liquidity.0xmarkets.io/positions)
* **Use trusted operators** when delegated-mining — General Tensor or any miner on the Cartha Rewards System (see [Delegated Miner](../cartha/delegated-miner.md))

## Reporting a Vulnerability

If you discover a potential security issue:

* **Email**: security@0xmarkets.io (or use the address listed on the [Contact page](../contact.md))
* **Do not** disclose publicly before the team has a chance to respond
* **Provide** reproduction details, severity assessment, and any PoC code

Responsible disclosures may be eligible for a bounty depending on severity and impact.

> All DeFi protocols carry inherent risks. See [Legal & risk](../legal-and-risk.md) before participating.
