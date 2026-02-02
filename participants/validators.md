# Validators

Validators play a critical role in the Cartha subnet by scoring miners based on their USDC liquidity positions and publishing weights to the Bittensor network.

## Responsibilities

* Cross‑verify multi‑oracle price feeds; maintain reliable pricing with fallbacks.&#x20;
* Monitor markets; **execute liquidations**; slashing for missed events.&#x20;
* Score miners based on locked USDC amounts, lock duration, and pool weights
* Publish normalized weights to Bittensor every epoch
* Liquidation fee share: **20%** of the 10% liquidation fee.

## Minimum Compute Requirements

To run a Cartha validator, you need:

- **CPU**: 2 cores minimum
- **RAM**: 4 GB minimum
- **Disk**: 20 GB SSD
- **Network**: Stable internet connection with minimal downtime

## Getting Started

See the [Validator Guide](../testnet/validator-guide.md) for detailed setup instructions.
