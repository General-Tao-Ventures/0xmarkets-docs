# Validator Guide

Complete guide for running validators on the 0xMarkets Liquidity Provider.

- **Repository**: [cartha-validator](https://github.com/General-Tao-Ventures/cartha-validator)
- **CLI Repository**: [cartha-cli](https://github.com/General-Tao-Ventures/cartha-cli)
- **PyPI Package**: [cartha-cli](https://pypi.org/project/cartha-cli/)

## Prerequisites

### Software Requirements

- ✅ Python 3.11 installed
- ✅ [`uv`](https://github.com/astral-sh/uv) package manager
- ✅ Node.js installed (for PM2 process manager)
- ✅ [btcli](https://docs.learnbittensor.org/btcli) installed (for wallet creation and subnet registration)
- ✅ Git (to clone the repository)
- ✅ TAO in your Bittensor wallet (for subnet registration)

### Minimum Compute Requirements

- ✅ **CPU**: 2 cores
- ✅ **RAM**: 4 GB
- ✅ **Disk**: 20 GB SSD
- ✅ **Network**: Stable internet connection with minimal downtime

> **Note**: On mainnet, validators must be whitelisted by the subnet owner. Contact the team via [Discord](https://0xmarkets.io/discord) with your validator SS58 hotkey address to request access.

---

## Step 1: Create Bittensor Wallet & Register to Subnet

Before running a validator, you need a Bittensor wallet and must register to the subnet.

### Create Wallet

If you don't have a Bittensor wallet, create one using btcli:

```bash
btcli wallet create
```

This will create both a coldkey and hotkey. Make sure to:
- **Save your mnemonic phrase** securely — you cannot recover your wallet without it
- **Fund your wallet with TAO** — required for subnet registration

For more details on wallet management, see the [Bittensor CLI documentation](https://docs.learnbittensor.org/btcli).

### Register to Subnet

You can register to subnet 35, which powers the 0xMarkets Liquidity Provider on mainnet, using either btcli or cartha-cli:

**Option 1: Register via the liquidity CLI**

```bash
pip install cartha-cli
cartha miner register
```

**Option 2: Register via btcli**

```bash
btcli subnets register --netuid 35
```

---

## Step 2: Install and Configure Validator

The `run.sh` script automates the full installation:

```bash
# Clone the repository
git clone https://github.com/General-Tao-Ventures/cartha-validator.git
cd cartha-validator

# Run the interactive installation script
./scripts/run.sh
```

The `run.sh` script will:

1. **Install PM2** (if not already installed) — process manager that keeps the validator running
2. **Check Python and uv** — ensures required tools are available
3. **Install dependencies** — automatically installs all Python packages
4. **Configure validator** — prompts you for:
   - Wallet name (coldkey)
   - Hotkey name
   - Network selection (Mainnet netuid 35 or Testnet netuid 78)
   - Optional: custom RPC URL override
   - Optional: dry-run mode for testing
5. **Setup PM2** — configures PM2 to manage both validator and auto-updater processes
6. **Start validator** — optionally starts the validator immediately

> **Warning**: On mainnet, validators must be whitelisted before they can query verified miners. The whitelist is managed by the verifier service — contact the subnet owner to have your hotkey added.

---

## Step 3: Validator is Running

Once `run.sh` completes, your validator is automatically:

- ✅ Running via PM2 (survives SSH disconnect and system restarts)
- ✅ Auto-updating when new releases are published on GitHub
- ✅ Configured with your wallet, hotkey, and network settings

### Auto-Updates

The validator manager automatically checks for new releases every hour. When a new version is detected:

1. The manager pulls the latest code from GitHub
2. Installs updated dependencies
3. Restarts the validator with the new version
4. All updates happen without manual intervention

Monitor update activity:
```bash
pm2 logs cartha-validator-manager
```

---

## How the Validator Works

### Epoch Schedule

The 0xMarkets Liquidity Provider uses a **weekly epoch cycle**:

| Event | Schedule |
| --- | --- |
| Weekly Epoch Start | Friday 00:00 UTC |
| Weekly Epoch End | Thursday 23:59 UTC |
| Epoch Version Format | ISO8601 (`YYYY-MM-DDT00:00:00Z`) |
| Weight Calculation | Once per week at epoch start |
| Weight Publishing | Every Bittensor epoch (~360 blocks) throughout the week |
| Daily Expiry Checks | Every 24 hours to filter newly expired positions |

### Scoring Logic

For each verified miner, the validator:

1. Fetches the epoch-frozen miner list from the verifier (snapshot taken at Friday 00:00 UTC)
2. Filters out expired pools (positions with `expires_at` in the past)
3. Filters out deregistered hotkeys (all their positions score 0)
4. Calculates per-position scores using the formula below
5. Sums position scores per miner
6. Applies minimum 100,000 USDC threshold (miners below this score 0)
7. Normalizes scores to Bittensor weights

### The Scoring Formula

Every liquidity position is scored individually:

```
position_score = pool_weight × amount_usdc × lock_boost

where:
  amount_usdc = frozen USDC at epoch start (original_amount_usdc)
  lock_boost  = min(lock_days, 365) / 365
  pool_weight = 1.0 for all pools (current pre-DEX equal-weight mode)
```

The miner's final raw score is the sum across all their active positions:

```
miner_score = Σ position_score_i
```

### Weight Normalization

```
remaining_weight = 1.0 − 0.243902 = 0.756098   (after 24.3902% incentive pool)
weight(miner_i)  = (miner_score_i / total_score) × 0.756098
```

The **Incentive Pool** always receives a fixed **24.3902%** of all subnet emissions regardless of miner activity.

---

## How Federated Miner Positions Affect Scores

The 0xMarkets Liquidity Provider is designed so every federated miner position makes a distinct, meaningful contribution to a principal miner's Bittensor weight.

### How It Works

When federated miners lock USDC into a principal miner's vault, those positions are included in the epoch snapshot. The validator scores each position individually — they are **not averaged or collapsed**. Each federated miner's position earns its own score based on its USDC amount and lock duration, then all scores are summed to produce the principal's final total.

**Example:**

| Position | USDC | Lock Days | Boost | Score |
| --- | --- | --- | --- | --- |
| Principal's own (365d) | 200,000 | 365 | 1.00 | 200,000 |
| Federated A (365d) | 50,000 | 365 | 1.00 | 50,000 |
| Federated B (182d) | 50,000 | 182 | 0.499 | 24,973 |
| Federated C (90d) | 50,000 | 90 | 0.247 | 12,329 |
| **Total** | **350,000** | — | — | **287,302** |

In this example, Federated A contributes more than twice the score of Federated C at the same USDC amount — because lock duration is rewarded proportionally. This creates a **fair, robust system** where every miner's commitment level directly drives their contribution to the principal's Bittensor weight.

### Why This Design Is Fair

- Every federated miner's position is evaluated independently — no averaging, no rounding
- Longer lock commitments translate directly to higher scores
- Mid-epoch top-ups are excluded (epoch freeze at Friday 00:00 UTC prevents late manipulation)
- The principal's Bittensor weight — and thus their subnet ALPHA emissions — reflects the true quality and commitment of their entire federated pool

### How Rewards Are Distributed to Federated Miners

After the Bittensor network allocates ALPHA emissions to the principal miner's hotkey, the principal uses the **`cartha-principal-rewards`** tool to distribute those earnings to their federated miners. The distribution uses the same per-position scoring formula:

```
# Each position scored identically to the validator:
position_score = pool_weight × scoring_amount × lock_boost

# Positions are split into two segments:
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

**Home positions** are the principal's own EVM wallet (commission-free). **Guest positions** are all other federated miners — they receive a proportional share of the guest pool after the principal's commission is deducted.

This two-layer design ensures:
1. The Bittensor network rewards principals whose vaults attract high-quality liquidity
2. Federated miners receive rewards that accurately reflect their individual lock commitments
3. The system is transparent and fully deterministic — both layers use the same scoring formula

---

## Configuration Options

### Automatic Configuration

The `run.sh` script configures everything automatically. Configuration is stored in:

- **PM2 Ecosystem Config**: `scripts/ecosystem.config.js` — validator arguments and environment variables
- **Auto-Updater Config**: `scripts/update_config.yaml` — GitHub repo and update settings

### Manual Configuration (Advanced)

**Edit PM2 Config** (`scripts/ecosystem.config.js`):
- Modify validator arguments in the `args` field
- Add environment variables in the `env` block
- Restart with: `pm2 restart cartha-validator --update-env`

**Command Line Arguments** (for manual runs):

```bash
uv run python -m cartha_validator.main --help
```

### Key Configuration Parameters

| Parameter | Default | Description |
| --- | --- | --- |
| `--netuid` | `35` | Subnet UID (mainnet) |
| `--subtensor.network` | `finney` | Bittensor network |
| `--wallet-name` | — | Coldkey wallet name (required) |
| `--wallet-hotkey` | — | Hotkey name (required) |
| `--epoch` | auto | Override epoch version (defaults to current Friday 00:00 UTC) |
| `--timeout` | `15.0` | HTTP timeout for verifier calls (seconds) |
| `--poll-interval` | `300` | Daemon polling interval (seconds) |
| `--log-dir` | `validator_logs` | Directory to save epoch weight logs |
| `--dry-run` | off | Print weights instead of publishing |
| `--run-once` | off | Exit after one run (instead of daemon mode) |

### Advanced Configuration (config.py)

Edit `cartha_validator/config.py` to customize:

| Setting | Default | Description |
| --- | --- | --- |
| `max_lock_days` | `365` | Maximum lock days for boost cap |
| `min_total_assets_usdc` | `100,000` | Minimum USDC threshold for any weight |
| `trader_rewards_pool_weight` | `0.243902` | Fixed incentive pool allocation (24.3902%) |
| `daily_alpha_emissions` | `2952.0` | Total ALPHA/day across all miners (display) |
| `pool_weights` | `{}` (equal) | Per-pool weight multipliers |

---

## Managing Your Validator

After installation, use PM2 to manage your validator:

```bash
# Check validator status
pm2 status

# View validator logs (real-time)
pm2 logs cartha-validator

# View last 100 lines
pm2 logs cartha-validator --lines 100

# View error logs only
pm2 logs cartha-validator --err

# View auto-updater logs
pm2 logs cartha-validator-manager

# Restart validator
pm2 restart cartha-validator

# Stop validator
pm2 stop cartha-validator

# Start validator
pm2 start cartha-validator

# View detailed process info
pm2 describe cartha-validator
```

### Manual Run (Advanced)

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

# Run with explicit epoch
uv run python -m cartha_validator.main \
  --netuid 35 \
  --subtensor.network finney \
  --wallet-name <name> \
  --wallet-hotkey <hotkey> \
  --epoch 2025-01-17T00:00:00Z
```

---

## Monitoring

### Log Files

PM2 stores logs in `~/.pm2/logs/`:
- `cartha-validator-out.log` — standard output
- `cartha-validator-error.log` — error output
- `cartha-validator-manager-out.log` — auto-updater output
- `cartha-validator-manager-error.log` — auto-updater errors

### What to Look For in Logs

A healthy validator will show:
- `[EPOCH] Weekly epoch detected` at the start of each Friday epoch
- Per-position scoring details: `[SCORE CALC] pool=... pool_weight=... × amount=... × boost=...`
- Per-miner weight assignments: `[WEIGHT] uid=... score=... → weight=...`
- `[TRADER POOL] Allocated fixed weight: 0.243902` every weight publication
- `Weights published successfully` after each `set_weights` call

### Health Checks

Test verifier connectivity:

```bash
# Test verifier health
curl "https://api.cartha.finance/health"

# Test verified miners endpoint for current epoch
curl "https://api.cartha.finance/v1/verified-miners?epoch=$(date -u +%Y-%m-%dT00:00:00Z)"
```

---

## Troubleshooting

### "Validator not whitelisted"

**Problem**: Your validator hotkey is not whitelisted on the verifier.

**Solution**:
- Contact the subnet owner via [Discord](https://0xmarkets.io/discord)
- Provide your validator hotkey SS58 address
- The whitelist is managed by the verifier service, not configured locally

### "Verifier URL not found"

**Problem**: Validator can't connect to verifier.

**Solution**:
- Test connectivity: `curl "https://api.cartha.finance/health"`
- Check validator logs: `pm2 logs cartha-validator`
- Verify network connectivity to `api.cartha.finance`

### "Weights not publishing"

**Problem**: Weights are computed but not published to Bittensor.

**Solution**:
- Check validator status: `pm2 status`
- View logs: `pm2 logs cartha-validator`
- Ensure your wallet has sufficient TAO
- Verify you're using network `finney` and netuid `35`
- Verify your hotkey is registered: `btcli subnets list --netuid 35`
- If cooldown is the issue, the validator will retry automatically on the next Bittensor epoch

### "No verified miners found"

**Problem**: Validator fetches an empty miner list.

**Solution**:
- Test the endpoint: `curl "https://api.cartha.finance/v1/verified-miners?epoch=$(date -u +%Y-%m-%dT00:00:00Z)"`
- Verify your epoch version matches the current epoch (should be the last Friday)
- Check network and netuid are correctly set to `finney` / `35`
- Restart validator: `pm2 restart cartha-validator`

### Score is 0 for a miner

**Problem**: A miner appears in the list but has score 0.

**Causes**:
- Total locked USDC across the principal miner's entire vault is below 100,000 USDC — all federated miners in that vault also receive no rewards for the epoch
- The hotkey was deregistered mid-epoch
- All of the miner's positions have expired (`expires_at` is in the past)

---

## Additional Resources

- **[Validation Overview](../validation/README.md)** — High-level role overview
- **[Cartha Architecture](https://github.com/General-Tao-Ventures/cartha-validator/blob/main/docs/ARCHITECTURE.md)** — Deep-dive into validator internals
- **[Rewards](../alpha-token/rewards/README.md)** — How emissions and fees flow through the subnet
- **[Weekly Epochs](../how-it-works/weekly-epochs.md)** — Epoch lifecycle and timing
- **Discord**: https://0xmarkets.io/discord — Join the 0xMarkets community for whitelist requests and support

---

> **Note**: Validators must be whitelisted by the subnet owner to participate on mainnet. Contact the team via Discord for whitelist requests.
