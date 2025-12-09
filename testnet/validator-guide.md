# Validator Guide - Cartha Testnet

Complete guide for running validators on Cartha testnet.

**Repository**: [cartha-validator](https://github.com/General-Tao-Ventures/cartha-validator)

## Prerequisites

Before you begin, ensure you have:

- ✅ Python 3.11 installed
- ✅ [`uv`](https://github.com/astral-sh/uv) package manager (or `pip`)
- ✅ Bittensor wallet with registered validator hotkey
- ✅ Access to the testnet verifier URL

**Note**: On testnet, all validators are allowed - no whitelist is required. Whitelist restrictions only apply to mainnet.

## Step 1: Install Cartha Validator

```bash
# Clone the repository
git clone <repository-url>
cd cartha-subnet/cartha-validator

# Install using uv (recommended)
uv sync

# Or install using pip
pip install -e .
```

## Step 2: Configure Testnet Environment

Set the following environment variables:

```bash
# Required: Testnet verifier URL
export CARTHA_VERIFIER_URL="https://cartha-verifier-826542474079.us-central1.run.app"

# Required: Bittensor network configuration
export CARTHA_NETWORK="test"  # Use "test" for testnet
export CARTHA_NETUID=78       # Testnet subnet UID

# Optional: Validator-specific settings
export VALIDATOR_LOG_DIR="validator_logs"
export VALIDATOR_POLL_INTERVAL=300  # Seconds between runs
```

## Step 3: Validator Configuration

**Testnet Note**: On testnet, all validators are allowed to query verified miners - no whitelist is required. You can proceed directly to running your validator.

**Mainnet Note**: On mainnet, validators must be whitelisted by the subnet owner. The whitelist is managed by the verifier, not configured locally in the validator. Contact the subnet owner to get your validator hotkey added to the verifier's whitelist for mainnet.

## Step 4: Run Your Validator

Run your validator to start scoring miners and publishing weights:

```bash
uv run python -m cartha_validator.main \
  --verifier-url "${CARTHA_VERIFIER_URL}" \
  --netuid 78 \
  --subtensor.network test \
  --wallet-name <your-wallet-name> \
  --wallet-hotkey <your-hotkey-name> \
  --use-verified-amounts
```

This will:
- Fetch verified miners from the verifier
- Score miners using verifier-supplied amounts
- Calculate normalized weights based on miner scores
- Publish weights to the Bittensor subnet
- Show detailed debug logs including:
  - Per-miner scoring details
  - Full ranking with all miners
  - Position aggregation by pool

**Note**: Debug logging is enabled by default. Use `--logging.debug=False` to reduce verbosity.

**⚠️ Important**: You **must** use the `--use-verified-amounts` flag. This tells the validator to use verified miner data from the verifier instead of querying RPC endpoints directly.

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

### Command Line Arguments

```bash
uv run python -m cartha_validator.main --help
```

Key options:

- `--verifier-url`: Verifier endpoint URL (required)
- `--netuid`: Subnet UID (default: 35, use 78 for testnet)
- `--subtensor.network`: Bittensor network (use `test` for testnet, `finney` for mainnet)
- `--wallet-name`: Coldkey wallet name (required)
- `--wallet-hotkey`: Hotkey name (required)
- `--epoch`: Override epoch version (defaults to current Friday 00:00 UTC)
- `--timeout`: HTTP timeout for verifier calls (default: 15s)
- `--logging.debug`: Enable debug logging (enabled by default, use `--logging.debug=False` to disable)

### Configuration File

Edit `cartha_validator/config.py` to customize:

- Pool weights
- Max lock days
- Score temperature
- Epoch schedule

**Note**: 
- The verifier handles all on-chain validation and provides verified miner data. Validators only query the verifier and score miners - no RPC endpoints needed.
- Validator whitelist is managed by the verifier, not configured locally in the validator.

## Common Validator Commands

```bash
# View help
uv run python -m cartha_validator.main --help

# Run validator (testnet)
uv run python -m cartha_validator.main \
  --verifier-url "${CARTHA_VERIFIER_URL}" \
  --netuid 78 \
  --subtensor.network test \
  --wallet-name <name> \
  --wallet-hotkey <hotkey> \
  --use-verified-amounts

# Run validator with custom epoch
uv run python -m cartha_validator.main \
  --verifier-url "${CARTHA_VERIFIER_URL}" \
  --netuid 78 \
  --subtensor.network test \
  --wallet-name <name> \
  --wallet-hotkey <hotkey> \
  --epoch 2025-01-17T00:00:00Z \
  --use-verified-amounts
```

## Monitoring

### Logging

The validator uses Bittensor's logging system with **debug logging enabled by default** for detailed diagnostics.

**Logging Levels:**

- **Debug** (default): Detailed information including full rankings, per-miner scoring, and position aggregation
- **Info**: General progress and important events
- **Warning**: Non-critical issues
- **Error**: Critical errors

**Controlling Logging:**

```bash
# Disable debug logging
--logging.debug=False

# Set custom log directory
export VALIDATOR_LOG_DIR="validator_logs"
```

### Health Checks

Test verifier connectivity:

```bash
# Test verifier health
curl "${CARTHA_VERIFIER_URL}/health"

# Test verified miners endpoint
curl "${CARTHA_VERIFIER_URL}/v1/verified-miners?epoch=$(date -u +%Y-%m-%dT00:00:00Z)"
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

**Problem**: CLI can't connect to verifier

**Solution**:

- Verify `CARTHA_VERIFIER_URL` is set correctly
- Test connectivity: `curl "${CARTHA_VERIFIER_URL}/health"`
- Check network connectivity

### "Weights not publishing"

**Problem**: Weights are not being published to Bittensor

**Solution**:

- Check your wallet has sufficient testnet TAO
- Verify you're using the correct network (`test`) and netuid (`78`)
- Check validator logs for error messages
- Verify your validator hotkey is registered on the subnet

### "No verified miners found"

**Problem**: Validator can't fetch verified miners

**Solution**:

- **Testnet**: All validators are allowed, so whitelist is not the issue
- Check the verifier URL is correct
- Test the verified miners endpoint manually
- Check epoch version matches current epoch
- Verify you're using the correct network (`test`) and netuid (`78`)

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
