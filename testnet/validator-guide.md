# Validator Guide - Cartha Testnet

Complete guide for running validators on Cartha testnet.

**Repository**: [cartha-validator](https://github.com/General-Tao-Ventures/cartha-validator)

## Prerequisites

Before you begin, ensure you have:

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

**Note**: On testnet, all validators are allowed - no whitelist is required. Whitelist restrictions only apply to mainnet.

The `run.sh` script will automatically:
- Install PM2 if not already installed
- Install all Python dependencies
- Configure your validator settings
- Set up process management

## Step 1: Install and Configure Validator

The validator installation is now fully automated with a single interactive script:

```bash
# Clone the repository
git clone https://github.com/General-Tao-Ventures/cartha-validator.git
cd cartha-validator

# Run the interactive installation script
./scripts/run.sh
```

The `run.sh` script will:

1. **Install PM2** (if not already installed) - Process manager for keeping validator running
2. **Check Python and uv** - Ensures required tools are available
3. **Install dependencies** - Automatically installs all Python dependencies
4. **Configure validator** - Prompts you for:
   - Wallet name (coldkey)
   - Hotkey name
   - Network selection (Mainnet netuid 35 or Testnet netuid 78)
   - Optional: Custom RPC URL override
   - Optional: Dry-run mode for testing
5. **Setup PM2** - Configures PM2 to manage both validator and auto-updater processes
6. **Start validator** - Optionally starts the validator immediately

**Testnet Note**: On testnet, all validators are allowed to query verified miners - no whitelist is required. You can proceed directly to running your validator.

**Mainnet Note**: On mainnet, validators must be whitelisted by the subnet owner. The whitelist is managed by the verifier, not configured locally in the validator. Contact the subnet owner to get your validator hotkey added to the verifier's whitelist for mainnet.

## Step 2: Validator is Running!

Once `run.sh` completes, your validator is automatically:

- ✅ Running via PM2 (survives SSH disconnect and system restarts)
- ✅ Auto-updating when new releases are published on GitHub
- ✅ Configured with your wallet, hotkey, and network settings
- ✅ Using `--use-verified-amounts` flag automatically (required)

### Auto-Updates

The validator manager automatically checks for new releases every hour. When a new version is detected:

1. The manager pulls the latest code from GitHub
2. Installs updated dependencies
3. Restarts the validator with the new version
4. All updates happen automatically - no manual intervention needed

You can monitor update activity in the validator manager logs:
```bash
pm2 logs cartha-validator-manager
```

The validator will:
- Fetch verified miners from the verifier
- Score miners using verifier-supplied amounts
- Calculate normalized weights based on miner scores
- Publish weights to the Bittensor subnet every Bittensor epoch
- Show detailed debug logs including:
  - Per-miner scoring details
  - Full ranking with all miners
  - Position aggregation by pool

**Note**: Debug logging is enabled by default. The validator manager handles all process management automatically.

**⚠️ Important**: The `--use-verified-amounts` flag is automatically included - this tells the validator to use verified miner data from the verifier instead of querying RPC endpoints directly.

## Validator Workflow

### Epoch Schedule

- **Weekly Epoch Start**: Friday 00:00 UTC
- **Weekly Epoch End**: Thursday 23:59 UTC (7 days total)
- **Epoch Version**: ISO8601 format (`YYYY-MM-DDT00:00:00Z`)
- **Weight Calculation**: Once per week at epoch start
- **Weight Publishing**: Every Bittensor epoch (tempo blocks) throughout the week
- **Daily Expiry Checks**: Performed daily during the week to filter expired pools

Validators should run continuously to catch epoch boundaries and perform daily checks.

### Scoring Logic

For each verified miner, the validator:

1. Fetches miner data from the verifier
2. Filters out expired pools (pools with `expires_at` in the past)
3. Calculates scores based on:
   - Locked amount (USDC)
   - Lock duration (lockDays)
   - Pool weights
   - Temperature curve
   - Expired pool filtering

### Weight Publishing

- Normalized weights are computed once per weekly epoch
- Weights are cached for the entire week
- Cached weights are published to Bittensor via `set_weights()` every Bittensor epoch (tempo blocks)
- Daily expiry checks update cached weights when pools expire

## Configuration Options

### Automatic Configuration

The `run.sh` script configures everything automatically. Configuration is stored in:

- **PM2 Ecosystem Config**: `scripts/ecosystem.config.js` - Contains validator arguments and environment variables
- **Auto-Updater Config**: `scripts/update_config.yaml` - Contains GitHub repo and update settings
- **Environment Variables**: `.env` file (if created) - Contains sensitive configuration

### Manual Configuration (Advanced)

If you need to modify configuration after installation:

**Edit PM2 Config** (`scripts/ecosystem.config.js`):
- Modify validator arguments in the `args` field
- Add environment variables in the `env` block
- Restart with: `pm2 restart cartha-validator --update-env`

**Command Line Arguments** (for manual runs):

```bash
uv run python -m cartha_validator.main --help
```

Key options:

- `--netuid`: Subnet UID (default: 35, use 78 for testnet)
- `--subtensor.network`: Bittensor network (use `test` for testnet, `finney` for mainnet)
- `--wallet-name`: Coldkey wallet name (required)
- `--wallet-hotkey`: Hotkey name (required)
- `--epoch`: Override epoch version (defaults to current Friday 00:00 UTC)
- `--timeout`: HTTP timeout for verifier calls (default: 15s)
- `--logging.debug`: Enable debug logging (enabled by default, use `--logging.debug=False` to disable)
- `--use-verified-amounts`: Always enabled automatically (required)

**Note**: 
- The verifier URL is automatically configured - no manual setup needed
- The verifier handles all on-chain validation and provides verified miner data. Validators only query the verifier and score miners - no RPC endpoints needed.
- Validator whitelist is managed by the verifier, not configured locally in the validator.

### Configuration File

Edit `cartha_validator/config.py` to customize:

- Pool weights
- Max lock days
- Score temperature
- Epoch schedule

## Managing Your Validator

After installation, use PM2 to manage your validator:

```bash
# Check validator status
pm2 status

# View validator logs
pm2 logs cartha-validator

# View validator manager logs (auto-updater)
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

If you need to run the validator manually for testing:

```bash
# View help
uv run python -m cartha_validator.main --help

# Run validator manually (testnet)
uv run python -m cartha_validator.main \
  --netuid 78 \
  --subtensor.network test \
  --wallet-name <name> \
  --wallet-hotkey <hotkey> \
  --use-verified-amounts

# Run validator with custom epoch
uv run python -m cartha_validator.main \
  --netuid 78 \
  --subtensor.network test \
  --wallet-name <name> \
  --wallet-hotkey <hotkey> \
  --epoch 2025-01-17T00:00:00Z \
  --use-verified-amounts
```

**Note**: When running via PM2 (recommended), the validator manager handles all configuration automatically. Manual runs are mainly for testing or debugging.

## Monitoring

### Logging

The validator uses Bittensor's logging system with **debug logging enabled by default** for detailed diagnostics.

**View Logs:**

```bash
# View validator logs (real-time)
pm2 logs cartha-validator

# View validator logs (last 100 lines)
pm2 logs cartha-validator --lines 100

# View error logs only
pm2 logs cartha-validator --err

# View validator manager logs (auto-updater)
pm2 logs cartha-validator-manager
```

**Logging Levels:**

- **Debug** (default): Detailed information including full rankings, per-miner scoring, and position aggregation
- **Info**: General progress and important events
- **Warning**: Non-critical issues
- **Error**: Critical errors

**Log Files:**

PM2 stores logs in `~/.pm2/logs/`:
- `cartha-validator-out.log` - Standard output
- `cartha-validator-error.log` - Error output
- `cartha-validator-manager-out.log` - Manager output
- `cartha-validator-manager-error.log` - Manager errors

### Health Checks

Test verifier connectivity:

```bash
# Test verifier health
curl "https://cartha-verifier-826542474079.us-central1.run.app/health"

# Test verified miners endpoint
curl "https://cartha-verifier-826542474079.us-central1.run.app/v1/verified-miners?epoch=$(date -u +%Y-%m-%dT00:00:00Z)"
```

## Troubleshooting

### "Validator not whitelisted" (Mainnet Only)

**Problem**: On mainnet, your validator hotkey is not whitelisted on the verifier

**Solution**:

- **Testnet**: This error should not occur on testnet as all validators are allowed
- **Mainnet**: Contact the subnet owner to get your validator hotkey added to the verifier's whitelist
- Provide your validator hotkey SS58 address
- The whitelist is managed by the verifier, not configured locally in the validator


### "Verifier URL not found"

**Problem**: Validator can't connect to verifier

**Solution**:

- The verifier URL is automatically configured by `run.sh`
- Test connectivity: `curl "https://cartha-verifier-826542474079.us-central1.run.app/health"`
- Check validator logs: `pm2 logs cartha-validator`
- Verify network connectivity
- If running manually, ensure you're using the correct verifier URL

### "Weights not publishing"

**Problem**: Weights are not being published to Bittensor

**Solution**:

- Check validator status: `pm2 status`
- View validator logs: `pm2 logs cartha-validator`
- Check your wallet has sufficient testnet TAO
- Verify you're using the correct network (`test`) and netuid (`78`) - configured during `run.sh`
- Verify your validator hotkey is registered on the subnet
- Ensure validator is running: `pm2 restart cartha-validator` if needed

### "No verified miners found"

**Problem**: Validator can't fetch verified miners

**Solution**:

- **Testnet**: All validators are allowed, so whitelist is not the issue
- Check validator logs: `pm2 logs cartha-validator`
- Test the verifier endpoint: `curl "https://cartha-verifier-826542474079.us-central1.run.app/v1/verified-miners?epoch=$(date -u +%Y-%m-%dT00:00:00Z)"`
- Check epoch version matches current epoch
- Verify you're using the correct network (`test`) and netuid (`78`) - configured during `run.sh`
- Restart validator: `pm2 restart cartha-validator`

## Additional Resources

- **[Testnet Overview](../testnet/README.md)** - Learn more about Cartha testnet
- **[Validator Testnet Setup Guide](https://github.com/General-Tao-Ventures/cartha-validator/blob/main/docs/TESTNET_SETUP.md)** - Detailed validator documentation
- **Discord**: https://discord.gg/7DXG57B6 - Join the Cartha community

## Next Steps

- Monitor your validator logs for scoring accuracy
- Test different scoring configurations
- Understand epoch cycles and weight publishing
- Join the validator community to share experiences

---

**Note**: Testnet is a testing environment. All tokens are testnet tokens with no real value. Use testnet to learn, test, and develop before deploying to mainnet.
