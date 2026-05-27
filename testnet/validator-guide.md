# Validator Guide - 0xMarkets Liquidity Provider Testnet

Complete guide for running validators on the 0xMarkets Liquidity Provider testnet.

- **Repository**: [cartha-validator](https://github.com/General-Tao-Ventures/cartha-validator)

## Prerequisites

### Software Requirements

- ✅ Python 3.11 installed
- ✅ [`uv`](https://github.com/astral-sh/uv) package manager
- ✅ Node.js installed (for PM2 process manager)
- ✅ Bittensor wallet with registered validator hotkey
- ✅ Git (to clone the repository)

### Minimum Compute Requirements

- ✅ **CPU**: 2 cores
- ✅ **RAM**: 4 GB
- ✅ **Disk**: 20 GB SSD
- ✅ **Network**: Stable internet connection with minimal downtime

> **Note**: On testnet, all validators are allowed — no whitelist is required. Whitelist restrictions only apply to mainnet.

---

## Step 1: Install and Configure Validator

```bash
# Clone the repository
git clone https://github.com/General-Tao-Ventures/cartha-validator.git
cd cartha-validator

# Run the interactive installation script
./scripts/run.sh
```

The `run.sh` script will:

1. **Install PM2** — process manager for keeping validator running
2. **Check Python and uv** — ensures required tools are available
3. **Install dependencies** — automatically installs all Python packages
4. **Configure validator** — prompts you for:
   - Wallet name (coldkey)
   - Hotkey name
   - Network selection — select **Testnet (netuid 78)**
   - Optional: dry-run mode for testing
5. **Setup PM2** — configures PM2 to manage both validator and auto-updater
6. **Start validator** — optionally starts the validator immediately

---

## Step 2: Validator is Running

Once `run.sh` completes, your validator is automatically:

- ✅ Running via PM2 (survives SSH disconnect and system restarts)
- ✅ Auto-updating when new releases are published on GitHub
- ✅ Configured with your wallet, hotkey, and network settings

---

## How the Validator Works

### Epoch Schedule

| Event | Schedule |
| --- | --- |
| Weekly Epoch Start | Friday 00:00 UTC |
| Weekly Epoch End | Thursday 23:59 UTC |
| Weight Calculation | Once per week at epoch start |
| Weight Publishing | Every Bittensor epoch (~360 blocks) throughout the week |
| Daily Expiry Checks | Every 24 hours to filter newly expired positions |

### Scoring Logic

For each verified miner, the validator:

1. Fetches the epoch-frozen miner list from the verifier (snapshot taken at Friday 00:00 UTC)
2. Filters out expired pools (`expires_at` in the past)
3. Filters out deregistered hotkeys (all their positions score 0)
4. Calculates per-position scores using the formula below
5. Sums position scores per miner
6. Applies 100,000 USDC minimum threshold (miners below this score 0)
7. Normalizes scores to Bittensor weights

### The Scoring Formula

Every liquidity position is scored individually:

```
position_score = pool_weight × amount_usdc × lock_boost

where:
  amount_usdc = frozen USDC at epoch start (original_amount_usdc)
  lock_boost  = min(lock_days, 365) / 365
  pool_weight = 1.0 for all pools (pre-DEX equal-weight mode)
```

The miner's total score is the sum across all active positions:

```
miner_score = Σ position_score_i
```

### Weight Normalization

```
remaining_weight = 1.0 − 0.243902 = 0.756098   (after 24.3902% incentive pool)
weight(miner_i)  = (miner_score_i / total_score) × 0.756098
```

---

## Configuration

### Testnet-Specific Settings

- **Network**: `test`
- **Netuid**: `78`
- **Verifier URL**: `https://cartha-verifier-826542474079.us-central1.run.app`

### Manual Run (Testnet)

```bash
# Dry run — print weights without publishing
uv run python -m cartha_validator.main \
  --netuid 78 \
  --subtensor.network test \
  --wallet-name <name> \
  --wallet-hotkey <hotkey> \
  --dry-run

# Production testnet run
uv run python -m cartha_validator.main \
  --netuid 78 \
  --subtensor.network test \
  --wallet-name <name> \
  --wallet-hotkey <hotkey>
```

---

## Managing Your Validator

```bash
pm2 status
pm2 logs cartha-validator
pm2 logs cartha-validator --lines 100
pm2 logs cartha-validator --err
pm2 logs cartha-validator-manager
pm2 restart cartha-validator
pm2 stop cartha-validator
pm2 start cartha-validator
pm2 describe cartha-validator
```

---

## Health Checks

```bash
# Test testnet verifier health
curl "https://cartha-verifier-826542474079.us-central1.run.app/health"

# Test verified miners endpoint
curl "https://cartha-verifier-826542474079.us-central1.run.app/v1/verified-miners?epoch=$(date -u +%Y-%m-%dT00:00:00Z)"
```

---

## Troubleshooting

### "Verifier URL not found"

**Problem**: Validator can't connect to the testnet verifier.

**Solution**:
- Test connectivity: `curl "https://cartha-verifier-826542474079.us-central1.run.app/health"`
- Check logs: `pm2 logs cartha-validator`

### "Weights not publishing"

**Problem**: Weights computed but not publishing.

**Solution**:
- Check you're using network `test` and netuid `78`
- Ensure wallet has testnet TAO
- Verify hotkey is registered on the subnet
- Restart if needed: `pm2 restart cartha-validator`

### "Validator not whitelisted"

This error only applies to mainnet (netuid 35). On testnet (netuid 78) all validators are allowed — if you see this, verify you have the correct netuid configured.

---

## Additional Resources

- **[Mainnet Validator Guide](../cartha/validator-guide.md)** — Full guide with scoring details and federated miner reward calculation
- **[Testnet Overview](../testnet/README.md)** — Learn more about the 0xMarkets Liquidity Provider testnet
- **[Validator Architecture](https://github.com/General-Tao-Ventures/cartha-validator/blob/main/docs/ARCHITECTURE.md)** — Deep-dive into validator internals

---

> **Warning**: Testnet is a testing environment. All tokens are testnet tokens with no real value. Use testnet to learn, test, and develop before deploying to mainnet.
