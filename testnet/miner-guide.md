# Miner Guide - Cartha Testnet

Complete guide for running miners (liquidity providers) on Cartha testnet.

**Repository**: [cartha-cli](https://github.com/General-Tao-Ventures/cartha-cli)

## Prerequisites

Before you begin, ensure you have:

- ✅ Python 3.11 installed
- ✅ [`uv`](https://github.com/astral-sh/uv) package manager (or `pip`)
- ✅ Bittensor wallet set up
- ✅ MetaMask (or other EVM wallet) installed
- ✅ Base Sepolia network added to MetaMask
- ✅ Testnet ETH in your wallet (for gas fees)
- ✅ Testnet USDC in your wallet (contact team if needed)
- ✅ Testnet TAO in your Bittensor wallet (for registration)

## Step 1: Install Cartha CLI

```bash
# Clone the repository
git clone <repository-url>
cd cartha-subnet/cartha-cli

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
```

## Step 3: Set Up Your EVM Wallet

### Add Base Sepolia Network to MetaMask

1. Open MetaMask and click the network dropdown
2. Click "Add Network" or "Add a network manually"
3. Enter the following details:

   ```
   Network Name: Base Sepolia
   RPC URL: https://base-sepolia.g.alchemy.com/v2/tmVGLC0DvW956sjrIjXuf
   Chain ID: 84532
   Currency Symbol: ETH
   Block Explorer URL: https://sepolia.basescan.org
   ```

4. Click "Save" and switch to Base Sepolia network

**Note**: We're using Alchemy's paid tier RPC endpoint for better performance and reliability. The free public endpoint (`https://sepolia.base.org`) is rate-limited and may experience delays.

**Quick Add (MetaMask):**

You can also use the [Chainlist](https://chainlist.org/) website:
1. Visit https://chainlist.org/
2. Search for "Base Sepolia"
3. Click "Connect Wallet" and approve the connection
4. Click "Add to MetaMask" and confirm

### Get Testnet Tokens

**Testnet ETH** (for gas fees):
- Visit: https://console.optimism.io/faucet
- Select "Base Sepolia" network
- Connect wallet and request tokens
- Wait a few minutes for the transaction to complete

**Testnet USDC** (for liquidity):
- Contact Cartha team via Discord/Telegram
- Provide your Base Sepolia wallet address
- Request testnet USDC for testing
- Wait for the team to send you testnet USDC

**Testnet TAO** (for registration):
- Visit: https://app.minersunion.ai/testnet-faucet
- Request testnet TAO to your wallet

## Step 4: Register Your Hotkey

Register your hotkey to the testnet subnet:

```bash
uv run cartha miner register \
  --network test \
  --netuid 78
```

This will:
- Register your hotkey to subnet 78 (testnet)
- Fetch your slot UID
- Display your registration details

**Save the output** - you'll need your slot UID for future commands.

## Step 5: Lock Funds

Use the interactive lock flow to create a lock position:

```bash
uv run cartha vault lock
```

**Note**: Chain ID and vault address are automatically detected from the pool ID - no need to specify them manually!

This command will:
1. Check your registration on the subnet
2. Authenticate with your Bittensor hotkey
3. Request a signed LockRequest from the verifier
4. Display transaction data for execution in MetaMask
5. Poll for lock status until verified

**Important**: Make sure you're connected to **Base Sepolia** network in MetaMask before executing transactions.

**Transaction Flow**:
1. **Approve USDC**: First transaction approves the vault to spend your USDC
2. **Lock Position**: Second transaction locks your USDC in the vault
3. Both transactions require gas fees (paid in testnet ETH)

## Step 6: Check Your Miner Status

Verify your miner status (no authentication required):

```bash
uv run cartha miner status \
  --wallet-name <your-wallet-name> \
  --wallet-hotkey <your-hotkey-name>
```

This shows:
- Miner state and pool information
- All active pools with amounts and expiration dates
- Days remaining countdown (with warnings for expiring pools)
- Password issuance status

## Available Testnet Pools

| Pool Name | Pool ID (hex) | Vault Address |
|-----------|---------------|---------------|
| BTC/USD | `0xee62665949c883f9e0f6f002eac32e00bd59dfe6c34e92a91c37d6a8322d6489` | `0x471D86764B7F99b894ee38FcD3cEFF6EAB321b69` |
| ETH/USD | `0x0b43555ace6b39aae1b894097d0a9fc17f504c62fea598fa206cc6f5088e6e45` | `0xdB74B44957A71c95406C316f8d3c5571FA588248` |
| EUR/USD | `0xa9226449042e36bf6865099eec57482aa55e3ad026c315a0e4a692b776c318ca` | `0x3C4dAfAC827140B8a031d994b7e06A25B9f27BAD` |

**Note**: When using `cartha vault lock`, you can simply specify `--pool-id BTC/USD` and the CLI will automatically:
- Match the correct vault address for that pool
- Match the correct chain ID (Base Sepolia: 84532)

You don't need to manually specify `--vault-address` or `--chain-id` unless you want to override them.

## Common Miner Commands

```bash
# View available pools
uv run cartha vault pools

# Check miner status
uv run cartha miner status --wallet-name <name> --wallet-hotkey <hotkey>

# View help
uv run cartha --help
uv run cartha miner register --help
uv run cartha vault lock --help
```

## Troubleshooting

### "Verifier URL not found"

**Problem**: CLI can't connect to verifier

**Solution**:

```bash
# Verify environment variable is set
echo $CARTHA_VERIFIER_URL

# Test verifier connectivity
curl "${CARTHA_VERIFIER_URL}/health"

# If using a different URL, update it
export CARTHA_VERIFIER_URL="https://cartha-verifier-826542474079.us-central1.run.app"
```

### "Hotkey not registered"

**Problem**: Hotkey is not registered on the subnet

**Solution**:

- Register your hotkey first using `cartha miner register`
- Verify you're using the correct network (`test`) and netuid (`78`)
- Check that you have testnet TAO in your wallet

### "Transaction failed"

**Problem**: MetaMask transaction failed

**Solution**:

- **Check Network**: Make sure you're on **Base Sepolia** network (not Mainnet or other networks)
- **Check Gas**: Ensure you have enough testnet ETH for gas fees
- **Check USDC**: Ensure you have enough testnet USDC in your wallet
- **Check Approval**: Make sure you've approved the vault to spend USDC (first transaction)
- **Verify Transaction Data**: Check that the transaction data matches what the CLI displayed
- **Check Network Congestion**: Base Sepolia may be slower than mainnet - wait a bit and retry

### "Insufficient funds" or "Not enough ETH"

**Problem**: Don't have enough testnet ETH for gas

**Solution**:

- Visit https://console.optimism.io/faucet
- Select "Base Sepolia" network
- Request testnet ETH to your wallet address
- Wait a few minutes for the transaction to complete
- Retry your transaction

### "USDC balance is zero" or "No USDC found"

**Problem**: Don't have testnet USDC tokens

**Solution**:

- Contact the Cartha team on Discord/Telegram
- Provide your Base Sepolia wallet address
- Request testnet USDC for testing
- Wait for the team to send you testnet USDC
- Verify receipt on [BaseScan Sepolia](https://sepolia.basescan.org/)

### "Write as Proxy" tab not showing on BaseScan

**Problem**: When trying to lock funds, you can't find the "Write as Proxy" tab on BaseScan

**Solution**:

The Cartha vault contracts are UUPS upgradeable proxy contracts. BaseScan needs to verify the proxy relationship before showing the "Write as Proxy" tab. Follow these steps:

1. **Navigate to the vault contract** on BaseScan:
   - Go to: `https://sepolia.basescan.org/address/{VAULT_ADDRESS}`
   - Replace `{VAULT_ADDRESS}` with your vault address

2. **Click the "Contract" tab** (if not already selected)

3. **Click the "Code" sub-tab** (under Contract)

4. **Find "More Options"** on the right side of the page

5. **Click "Is this a proxy?"** from the More Options menu

6. **Click "Verify"** to link the proxy to its implementation contract

7. **Wait for verification** - BaseScan will automatically detect and link the implementation contract

8. **Refresh the page** - After verification completes, you should now see "Write as Proxy" tab

**Note**: This verification is a one-time process per contract. Once verified, the "Write as Proxy" tab will remain available for that contract address.

## Testing Your Setup

### Complete Testnet Checklist

Before starting, make sure you have:

- [ ] Python 3.11 installed
- [ ] `uv` package manager installed
- [ ] Bittensor wallet set up
- [ ] MetaMask (or other EVM wallet) installed
- [ ] Base Sepolia network added to MetaMask
- [ ] Testnet ETH in your wallet (from faucet)
- [ ] Testnet USDC in your wallet (from team)
- [ ] Testnet TAO in your Bittensor wallet (for registration)

### Quick Test

```bash
# 1. Register your hotkey
uv run cartha miner register --wallet-name test --wallet-hotkey test --network test --netuid 78

# 2. Check miner status (no authentication needed)
uv run cartha miner status --wallet-name test --wallet-hotkey test

# 3. Lock funds (interactive flow)
# Note: Make sure you're on Base Sepolia network in MetaMask!
uv run cartha vault lock \
  --coldkey test \
  --hotkey test \
  --pool-id BTC/USD \
  --amount 100.0 \
  --lock-days 30 \
  --owner-evm 0xYourEVMAddress
```

**Important**: 
- Chain ID (84532 for Base Sepolia) and vault address are **automatically detected** from the pool ID
- You only need to specify `--pool-id BTC/USD` (or `ETH/USD`, `EUR/USD`)
- The CLI will show you the auto-matched values before proceeding

## Additional Resources

- **[Testnet Overview](../testnet/README.md)** - Learn more about Cartha testnet
- **[CLI Testnet Guide](https://github.com/General-Tao-Ventures/cartha-cli/tree/main/testnet)** - Detailed CLI documentation
- **Discord**: https://discord.gg/7DXG57B6
Contact Cartha team for testnet USDC and support 

## Next Steps

- Experiment with different pools and lock durations
- Test multi-pool strategies
- Monitor your miner status regularly
- Join the community to share experiences and get help

---

**Note**: Testnet is a testing environment. All tokens are testnet tokens with no real value. Use testnet to learn, test, and develop before deploying to mainnet.
