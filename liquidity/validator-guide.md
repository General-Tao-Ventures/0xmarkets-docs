# Validator Guide

Complete guide to running a validator on **Bittensor Subnet 35 (SN35)** — the network behind the **0xMarkets Liquidity Engine**. Validators score liquidity providers (miners) by the USDC they have locked and how long they have locked it for, then publish normalized weights to Bittensor so emissions flow to the miners who committed the most capital for the longest.

- **Repository:** [cartha-validator](https://github.com/General-Tao-Ventures/cartha-validator)
- **CLI:** [cartha-cli](https://github.com/General-Tao-Ventures/cartha-cli) · [PyPI](https://pypi.org/project/cartha-cli/)

> **Beta.** The liquidity engine is live and functional but still maturing. Some parameters will be tuned as it matures.

---

## What a validator does

A validator does **not** price trades or assess miner "performance" in any trading sense — pricing is handled by the protocol's [Pyth Pro](../trading/pricing-and-oracle.md) oracle and an on-chain impact model, and miners are pure capital providers. The validator's only job is to measure committed liquidity and turn it into Bittensor weights:

- Score every miner position as `locked USDC × lock-duration boost × pool weight`.
- Sum positions per hotkey and apply the **100,000 USDC** minimum threshold.
- Normalize scores into Bittensor weights and publish them each epoch.
- Filter out expired and deregistered positions throughout the week.

---

## Prerequisites

### Software

- Python 3.11
- [`uv`](https://github.com/astral-sh/uv) package manager
- Node.js (for the PM2 process manager)
- [btcli](https://docs.learnbittensor.org/btcli) (wallet creation and subnet registration)
- Git (to clone the repository)
- TAO in your Bittensor wallet (for subnet registration)

### Minimum compute

- **CPU:** 2 cores
- **RAM:** 4 GB
- **Disk:** 20 GB SSD
- **Network:** stable connection with minimal downtime

> **Note:** On mainnet, validators must be whitelisted by the subnet owner. Contact the team via [Discord](https://0xmarkets.io/discord) with your validator SS58 hotkey address to request access.

---

## Step 1: Create a Bittensor wallet & register to the subnet

### Create the wallet

If you don't already have a Bittensor wallet, create one with btcli:

```bash
btcli wallet create
```

This creates both a coldkey and hotkey. Make sure to:

- **Save your mnemonic phrase** securely — you cannot recover the wallet without it.
- **Fund the wallet with TAO** — required for subnet registration.

For more on wallet management, see the [Bittensor CLI docs](https://docs.learnbittensor.org/btcli).

### Register to the subnet

Register your hotkey to **Subnet 35 (SN35)** using either the liquidity CLI or btcli:

**Option 1: liquidity CLI**

```bash
pip install cartha-cli
cartha miner register
```

**Option 2: btcli**

```bash
btcli subnets register --netuid 35
```

---

## Step 2: Install and configure the validator

The `run.sh` script automates the full installation:

```bash
# Clone the repository
git clone https://github.com/General-Tao-Ventures/cartha-validator.git
cd cartha-validator

# Run the interactive installation script
./scripts/run.sh
```

The script will:

1. **Install PM2** (if needed) — the process manager that keeps the validator running.
2. **Check Python and uv** — ensure required tools are available.
3. **Install dependencies** — all Python packages.
4. **Configure the validator** — prompts you for the wallet name (coldkey), hotkey name, network (mainnet netuid 35), an optional custom RPC URL, and an optional dry-run mode.
5. **Set up PM2** — configures PM2 to manage both the validator and the auto-updater.
6. **Start the validator** — optionally starts it immediately.

> **Important:** On mainnet, validators must be whitelisted before they can query verified miners. The whitelist is managed by the verifier service — contact the subnet owner to have your hotkey added.

---

## Step 3: Validator is running

Once `run.sh` completes, your validator is automatically:

- Running via PM2 (survives SSH disconnect and reboots)
- Auto-updating when new releases are published on GitHub
- Configured with your wallet, hotkey, and network settings

### Auto-updates

The validator manager checks for new releases every hour. When a new version is detected it pulls the latest code, installs updated dependencies, and restarts the validator — no manual intervention. Monitor update activity:

```bash
pm2 logs cartha-validator-manager
```

---

## How the validator works

### Epoch schedule

The subnet runs on a **weekly (7-day) epoch cycle**:

| Event | Schedule |
| --- | --- |
| Epoch start | Friday 00:00 UTC |
| Epoch end | Thursday 23:59 UTC |
| Epoch version format | ISO8601 (`YYYY-MM-DDT00:00:00Z`) |
| Weight calculation | Once per week at epoch start |
| Weight publishing | Every Bittensor epoch (~360 blocks) throughout the week |
| Daily expiry checks | Every 24 hours, to filter newly expired positions |

### Scoring logic

For each verified miner, the validator:

1. Fetches the epoch-frozen miner list from the verifier (snapshot taken at Friday 00:00 UTC).
2. Filters out expired positions (`expires_at` in the past).
3. Filters out deregistered hotkeys (all their positions score 0).
4. Calculates per-position scores using the formula below.
5. Sums position scores per miner.
6. Applies the **100,000 USDC** minimum threshold (hotkeys below it score 0).
7. Normalizes scores into Bittensor weights.

### The scoring formula

Every liquidity position is scored individually:

```
position_score = pool_weight × amount_usdc × lock_boost

where:
  amount_usdc = USDC frozen at epoch start (original_amount_usdc)
  lock_boost  = min(lock_days, 365) / 365
  pool_weight = 1.0 for all pools (current equal-weight mode)
```

A hotkey's raw score is the sum across all its active positions:

```
miner_score = Σ position_score_i
```

### Weight normalization

Validators normalize raw scores into Bittensor weights. A fixed portion of subnet emissions is reserved for the incentive pool before the remainder is split across qualified miners in proportion to their score:

```
remaining_weight = 1.0 − incentive_pool_fraction
weight(miner_i)  = (miner_score_i / total_score) × remaining_weight
```

> The emissions split is **41% validators, 31% miners, 18% subnet owner, 10% incentive pool.** The `incentive_pool_fraction` above is the **10%** incentive-pool allocation; the remaining weight is distributed across miners by score. See [Fees & rewards](../how-it-works/fees-and-rewards.md).

---

## How federated miner positions affect scores

The liquidity engine is designed so every federated-miner position makes a distinct, meaningful contribution to a principal miner's Bittensor weight.

When federated miners lock USDC under a principal miner's hotkey, those positions are included in the epoch snapshot. The validator scores each position **individually** — they are not averaged or collapsed. Each federated position earns its own score from its USDC amount and lock duration, and all scores are summed into the principal's total.

**Example:**

| Position | USDC | Lock days | Boost | Score |
| --- | --- | --- | --- | --- |
| Principal's own (365d) | 200,000 | 365 | 1.00 | 200,000 |
| Federated A (365d) | 50,000 | 365 | 1.00 | 50,000 |
| Federated B (182d) | 50,000 | 182 | 0.499 | 24,973 |
| Federated C (90d) | 50,000 | 90 | 0.247 | 12,329 |
| **Total** | **350,000** | — | — | **287,302** |

Federated A contributes more than twice the score of Federated C at the same USDC amount, because lock duration is rewarded proportionally. Every commitment level maps directly and transparently to weight.

### Why this design is robust

- Every federated position is evaluated independently — no averaging, no rounding.
- Longer lock commitments translate directly into higher scores.
- Mid-epoch top-ups are excluded (the Friday 00:00 UTC freeze prevents late manipulation).
- The principal's weight — and thus their ALPHA emissions — reflects the true commitment of the entire set of positions under their hotkey.

### How rewards reach federated miners

This is an **off-chain rewards-aggregation step run by the principal miner**, not an on-chain transfer the validator performs. After Bittensor allocates ALPHA to the principal's hotkey, the principal's rewards service (`cartha-principal-rewards`) splits it out using the same per-position scoring formula. Federated miners' USDC never moves — only the ALPHA they earned is distributed.

```
# Each position scored identically to the validator:
position_score = pool_weight × scoring_amount × lock_boost

# Positions split into two segments:
home_share  = home_total_score / total_score      # Principal's own positions
guest_share = guest_total_score / total_score     # All federated miners

# ALPHA distribution:
home_alpha  = total_alpha × home_share             # No commission
guest_gross = total_alpha × guest_share
commission  = guest_gross × commission_rate
guest_net   = guest_gross − commission             # Distributed to federated miners

# Each federated miner receives:
reward_i = guest_net × (score_i / guest_total_score)
```

**Home positions** are the principal's own EVM wallet (commission-free). **Guest positions** are all federated miners — they receive a proportional share of the guest pool after the principal's commission. Both layers use the same deterministic scoring formula, so the entire chain from lock to reward is transparent.

---

## Configuration options

### Automatic configuration

The `run.sh` script configures everything. Configuration lives in:

- **PM2 ecosystem config:** `scripts/ecosystem.config.js` — validator arguments and environment variables.
- **Auto-updater config:** `scripts/update_config.yaml` — GitHub repo and update settings.

### Manual configuration (advanced)

**Edit the PM2 config** (`scripts/ecosystem.config.js`):

- Modify validator arguments in the `args` field.
- Add environment variables in the `env` block.
- Restart with `pm2 restart cartha-validator --update-env`.

**Command-line arguments** (for manual runs):

```bash
uv run python -m cartha_validator.main --help
```

### Key parameters

| Parameter | Default | Description |
| --- | --- | --- |
| `--netuid` | `35` | Subnet UID (mainnet) |
| `--subtensor.network` | `finney` | Bittensor network |
| `--wallet-name` | — | Coldkey wallet name (required) |
| `--wallet-hotkey` | — | Hotkey name (required) |
| `--epoch` | auto | Override epoch version (defaults to the current Friday 00:00 UTC) |
| `--timeout` | `15.0` | HTTP timeout for verifier calls (seconds) |
| `--poll-interval` | `300` | Daemon polling interval (seconds) |
| `--log-dir` | `validator_logs` | Directory for epoch weight logs |
| `--dry-run` | off | Print weights instead of publishing |
| `--run-once` | off | Exit after one run instead of daemon mode |

### Advanced configuration (`config.py`)

Edit `cartha_validator/config.py` to customize:

| Setting | Default | Description |
| --- | --- | --- |
| `max_lock_days` | `365` | Maximum lock days for the boost cap |
| `min_total_assets_usdc` | `100,000` | Minimum USDC threshold for any weight |
| `trader_rewards_pool_weight` | see config | Incentive-pool allocation — **10%** of daily emissions (of the 41/31/18/10 validator/miner/owner/incentive split) |
| `daily_alpha_emissions` | see config | Total ALPHA/day across all miners (display only) |
| `pool_weights` | `{}` (equal) | Per-pool weight multipliers |

---

## Managing your validator

Use PM2 to manage the validator:

```bash
pm2 status                              # Check status
pm2 logs cartha-validator               # Live logs
pm2 logs cartha-validator --lines 100   # Last 100 lines
pm2 logs cartha-validator --err         # Errors only
pm2 logs cartha-validator-manager       # Auto-updater logs
pm2 restart cartha-validator            # Restart
pm2 stop cartha-validator               # Stop
pm2 start cartha-validator              # Start
pm2 describe cartha-validator           # Detailed process info
```

### Manual run (advanced)

```bash
# Dry run — print weights without publishing
uv run python -m cartha_validator.main \
  --netuid 35 \
  --subtensor.network finney \
  --wallet-name <name> \
  --wallet-hotkey <hotkey> \
  --dry-run

# Production run
uv run python -m cartha_validator.main \
  --netuid 35 \
  --subtensor.network finney \
  --wallet-name <name> \
  --wallet-hotkey <hotkey>

# Run with an explicit epoch
uv run python -m cartha_validator.main \
  --netuid 35 \
  --subtensor.network finney \
  --wallet-name <name> \
  --wallet-hotkey <hotkey> \
  --epoch 2025-01-17T00:00:00Z
```

---

## Monitoring

### Log files

PM2 stores logs in `~/.pm2/logs/`:

- `cartha-validator-out.log` — standard output
- `cartha-validator-error.log` — error output
- `cartha-validator-manager-out.log` — auto-updater output
- `cartha-validator-manager-error.log` — auto-updater errors

### What a healthy validator shows

- `[EPOCH] Weekly epoch detected` at the start of each Friday epoch
- Per-position scoring: `[SCORE CALC] pool=... pool_weight=... × amount=... × boost=...`
- Per-miner weights: `[WEIGHT] uid=... score=... → weight=...`
- The fixed incentive-pool allocation logged on every weight publication
- `Weights published successfully` after each `set_weights` call

### Health checks

```bash
# Verifier health
curl "https://api.cartha.finance/health"

# Verified miners for the current epoch
curl "https://api.cartha.finance/v1/verified-miners?epoch=$(date -u +%Y-%m-%dT00:00:00Z)"
```

---

## Troubleshooting

### "Validator not whitelisted"

- Contact the subnet owner via [Discord](https://0xmarkets.io/discord).
- Provide your validator hotkey SS58 address.
- The whitelist is managed by the verifier service, not configured locally.

### "Verifier URL not found"

- Test connectivity: `curl "https://api.cartha.finance/health"`.
- Check validator logs: `pm2 logs cartha-validator`.
- Verify network connectivity to `api.cartha.finance`.

### "Weights not publishing"

- Check status: `pm2 status`.
- View logs: `pm2 logs cartha-validator`.
- Ensure your wallet has sufficient TAO.
- Verify you are on network `finney`, netuid `35`.
- Verify your hotkey is registered: `btcli subnets list --netuid 35`.
- If a cooldown is the issue, the validator retries automatically on the next Bittensor epoch.

### "No verified miners found"

- Test the endpoint: `curl "https://api.cartha.finance/v1/verified-miners?epoch=$(date -u +%Y-%m-%dT00:00:00Z)"`.
- Verify your epoch version matches the current epoch (the last Friday).
- Check network and netuid are set to `finney` / `35`.
- Restart: `pm2 restart cartha-validator`.

### Score is 0 for a miner

- Total locked USDC under that hotkey is below **100,000 USDC** — every federated miner under it also earns nothing for the epoch.
- The hotkey was deregistered mid-epoch.
- All of the hotkey's positions have expired (`expires_at` in the past).

---

## Next

- [Principal Miner Guide](principal-miner-guide.md) — the operator side of scoring
- [Become a Liquidity Provider](miner-guide.md) — the LP basics
- [Weekly Epochs](../how-it-works/weekly-epochs.md) — epoch lifecycle and timing
- [Fees & rewards](../how-it-works/fees-and-rewards.md) — how emissions flow through the subnet
- [Risk disclosures](../security/risk-disclosures.md) — network and systemic risks
- [FAQ](../reference/faq.md) · [Glossary](../reference/glossary.md)
- **Discord:** [0xmarkets.io/discord](https://0xmarkets.io/discord) — whitelist requests and support

---

> **Note:** Validators must be whitelisted by the subnet owner to participate on mainnet. Contact the team via Discord for whitelist requests.
