# Miners (LPs)

Miners provide USDC liquidity into the 0xMarkets liquidity vaults and earn trading fees and ALPHA emissions in return.

There are two types of miners — **principal miners** who hold registered Bittensor hotkeys and operate vaults directly, and **federated miners** who lock capital through a principal miner without running any Bittensor infrastructure.

---

## Principal Miners

Principal miners are registered Bittensor participants on the Cartha subnet (SN35), which powers the 0xMarkets Liquidity Provider. They lock USDC into market vaults, receive ALPHA emissions based on their vault's deposit score, and can optionally open their vault to external capital from federated miners.

**How scores and rewards are calculated:**

Every liquidity position is scored individually using the same formula:

```
position_score = pool_weight × amount_usdc × lock_boost
lock_boost     = min(lock_days, 365) / 365

miner_score    = Σ position_score   (sum across all active positions)
```

A principal miner's total score includes every position in their vault — their own capital and every federated miner's position. Each federated position is evaluated independently based on its own amount and lock duration. A federated miner locking for 365 days contributes twice the score of one locking for 182 days at the same USDC amount. This design ensures every participant's commitment level is fairly reflected in the principal miner's Bittensor weight and the ALPHA emissions they receive.

Principal miners with a total vault balance below **100,000 USDC** receive a score of 0. Since the principal miner's score drives all ALPHA emissions for their vault, federated miners inside that vault also receive no rewards for the epoch.

**Earning:**
- 50% of trading fees from their pools (proportional to deposit)
- ALPHA emissions proportional to their deposit score relative to all miners

→ [Learn more about Principal Miners](principal-miners.md) · [Principal Miner Guide](../cartha/principal-miner-guide.md)

---

## Federated Miners

Federated miners participate in the 0xMarkets Liquidity Provider without running a Bittensor node. They lock USDC through a principal miner's vault using only an EVM wallet, and earn a share of the principal miner's ALPHA emissions based on their individual position score.

**How rewards flow to federated miners:**

After the principal receives their ALPHA emissions, they distribute to federated miners using the same per-position scoring formula. Positions are split into two segments:

- **Home** (principal's own capital) — receives its proportional share with no commission
- **Guest** (all federated miners) — receives a proportional share after the principal's commission is deducted

```
each_reward = (guest_alpha_net) × (your_score / total_guest_score)
```

This means every federated miner's lock duration and amount directly determines their slice — no averaging, no pooling into a single rate.

**Key facts:**
- No Bittensor wallet or node required to lock
- Your USDC is held in a smart contract — the principal miner cannot access it
- Withdraw after your lock period expires, no approval needed
- ALPHA emissions flow to the principal miner first, then distributed per their terms

→ [Learn more about Federated Miners](federated-miners.md) · [Federated Miner Guide](../cartha/federated-miner-guide.md)

---

## Minimum Requirements

| | Principal Miner | Federated Miner |
| --- | --- | --- |
| Bittensor wallet | ✅ Required | ✅ Needed to claim ALPHA |
| EVM wallet | ✅ Required | ✅ Required |
| Subnet registration | ✅ Required (SN35) | ❌ Not required |
| Minimum locked USDC | 100,000 USDC | Depends on principal miner |

---

## Getting Started

- **Principal miners** — see the [Principal Miner Guide](../cartha/principal-miner-guide.md)
- **Federated miners** — see the [Federated Miner Guide](../cartha/federated-miner-guide.md)
- **Not sure which?** — If you have USDC but no Bittensor setup, start as a federated miner. Lock through [General Tensor](https://liquidity.0xmarkets.io/principal-miners) (the team-operated principal miner) to get started immediately.
