# Cartha Interface

**A modern web interface for managing your Cartha lock positions.** The Cartha Interface replaces the need to manually interact with smart contracts on BaseScan, providing a streamlined, user-friendly experience for liquidity providers.

**URL**: [https://cartha.finance](https://cartha.finance/)

## What is Cartha Interface?

The Cartha Interface is a web-based interface that simplifies the process of creating and managing lock positions on the Cartha subnet. Instead of manually copying transaction data and executing contracts on block explorers, the interface guides you through each step with clear instructions and automatic wallet integration.

### Key Benefits

* ✅ **No BaseScan Required** - Execute all transactions directly in the UI
* ✅ **Multi-Wallet Support** - Works with MetaMask, Coinbase Wallet, Talisman, and WalletConnect
* ✅ **Automatic Validation** - Ensures you're using the correct wallet address
* ✅ **Real-Time Status** - View transaction status and confirmations in real-time
* ✅ **Position Management** - View all your positions in one place
* ✅ **Modern Design** - Clean, intuitive interface with dark theme

## What Can You Do?

### 1. Create New Lock Positions

The primary use case for the Cartha Interface is creating new lock positions. The process is split into two phases:

#### Phase 1: Approve USDC

1. **Start from CLI**: Run `cartha vault lock` with your parameters
2. **Browser Opens Automatically**: The CLI opens the UI with all parameters pre-filled
3. **Connect Your Wallet**: Connect MetaMask, Coinbase Wallet, Talisman, or WalletConnect
4. **Wallet Validation**: The UI verifies your connected wallet matches the required owner address
5. **Approve Transaction**: Review the approval details and execute the transaction
6. **Automatic Detection**: The CLI automatically detects when approval completes

**What You'll See**:

* Required owner address vs your connected wallet address
* USDC contract address and spender (vault) address
* Amount to approve
* Copy buttons for easy reference
* Transaction status indicators

#### Phase 2: Lock Position

After Phase 1 completes, you'll automatically proceed to Phase 2:

1. **Review Lock Details**: See all lock parameters (pool ID, amount, lock days, hotkey, etc.)
2. **Confirm Transaction**: Review the lock details before executing
3. **Execute Lock**: Sign and submit the lock transaction
4. **Success Confirmation**: See confirmation with a link to view your positions

**What You'll See**:

* Pool ID and name
* Lock amount in USDC
* Lock duration in days
* Unlock date
* Hotkey address
* Required owner vs connected wallet comparison
* Transaction status with BaseScan link

### 2. View Your Positions

Navigate to **"My Positions"** (or visit `/manage`) to see all your active lock positions:

**Features**:

* **All Positions at a Glance**: See all your pools in one dashboard
* **Position Details**: For each position, view:
  * Pool name (e.g., BTCUSD, ETH/USD, EUR/USD)
  * Amount locked (USDC)
  * Lock duration (days)
  * Expiration date with countdown
  * Status (Active, In Next Epoch, etc.)
  * EVM address used for the lock
* **Status Indicators**: Color-coded status badges
* **Quick Actions**: Extend and Top Up buttons for each position
* **Refresh Button**: Manually refresh to see latest status

**Access Methods**:

* Click "My Positions" button on the landing page
* Navigate to `/manage` directly
* Click "View My Positions" after successfully creating a lock

### 3. Extend Lock Duration

Extend the duration of an existing lock position:

1. **Go to My Positions**: Navigate to the positions dashboard
2. **Click "Extend"**: Click the Extend button on the position you want to extend
3. **Select New Duration**: Choose how many additional days to add
4. **Review and Confirm**: Review the extension details
5. **Execute Transaction**: Sign and submit the extension transaction

**Note**: Extend Lock feature is currently in testing and may not work properly yet. If you encounter issues, contact support on Discord.

### 4. Top Up Existing Positions

Add more USDC to an existing lock position:

1. **Go to My Positions**: Navigate to the positions dashboard
2. **Click "Top Up"**: Click the Top Up button on the position you want to add funds to
3. **Enter Amount**: Specify how much additional USDC to add
4. **Approve if Needed**: If you haven't approved enough USDC, approve first
5. **Review and Confirm**: Review the top-up details
6. **Execute Transaction**: Sign and submit the top-up transaction

**Note**: Top Up feature is currently in testing and may not work properly yet. If you encounter issues, contact support on Discord.

### 5. Testnet Faucet

A built-in faucet for claiming testnet tokens:

* **Claim Testnet USDC**: Get 1,000,000 testnet USDC per claim
* **24-Hour Cooldown**: One claim per wallet address every 24 hours
* **Cooldown Management**: See when you can claim again
* **Balance Display**: View your current testnet token balances
* **ETH Faucet Links**: Quick access to external ETH faucets (Optimism and Alchemy)

**How to Use**:

1. Navigate to https://cartha.finance/faucet
2. Connect your wallet (must be on Base Sepolia network)
3. Click "Claim USDC" to receive 1,000,000 testnet USDC
4. Wait 24 hours before claiming again from the same wallet

**Note**: For testnet ETH, use the external faucet links provided on the faucet page (Optimism or Alchemy faucets).

## How It Works with the CLI

The Cartha Interface is designed to work seamlessly with the Cartha CLI:

### Starting from CLI

```bash
cartha vault lock \
  --coldkey my-coldkey \
  --hotkey my-hotkey \
  --network test \
  --pool-id BTCUSD \
  --amount 100.0 \
  --lock-days 30 \
  --owner-evm 0xYourEVMAddress

# Or using short aliases:
cartha v lock -w cold -wh hot -n test -p BTCUSD -a 100 -d 30 -e 0xYourEVM...
```

**What Happens**:

1. CLI authenticates with your Bittensor hotkey
2. CLI requests a signature from the verifier
3. CLI automatically opens the UI in your browser
4. UI is pre-filled with all transaction parameters
5. You complete the transactions in the UI
6. CLI monitors Phase 1 approval automatically
7. Verifier detects Phase 2 lock automatically

### Direct Access

You can also access the UI directly:

* **Landing Page**: https://cartha.finance
* **My Positions**: https://cartha.finance/manage
* **Faucet**: https://cartha.finance/faucet

When accessing directly, you'll need to:

* Connect your wallet manually
* Navigate to the feature you want to use
* Note: Creating new locks is best done through the CLI for proper signature generation

## Supported Wallets

The Cartha Interface supports multiple wallet types:

* **MetaMask** - Most popular Ethereum wallet
* **Coinbase Wallet** - Coinbase's official wallet
* **Talisman** - Recommended Bittensor/Polkadot wallet (browser extension)
* **WalletConnect** - Connect any WalletConnect-compatible wallet

**Network Requirement**: All wallets must be connected to **Base Sepolia** network (Chain ID: 84532) for testnet, or **Base Mainnet** (Chain ID: 8453) for mainnet.

## Security Features

### Wallet Address Validation

The UI includes automatic wallet validation to prevent common mistakes:

* **Required Owner Check**: Compares the connected wallet with the required owner address
* **Visual Warnings**: Clear indicators when addresses don't match
* **Disconnect/Reconnect**: Easy buttons to disconnect and reconnect the correct wallet
* **Error Prevention**: Prevents transactions with the wrong wallet

### Transaction Safety

* **Clear Parameter Display**: All transaction parameters are clearly displayed before execution
* **Copy Buttons**: Easy copy buttons for addresses and values
* **Transaction Status**: Real-time status updates with BaseScan links
* **Error Handling**: Clear error messages if transactions fail

## User Interface

### Design

* **Dark Theme**: Modern dark theme optimized for extended use
* **Responsive Layout**: Works on desktop, tablet, and mobile devices
* **Material Symbols**: Uses Material Symbols icons for consistent visual language
* **Inter Font**: Clean, readable Inter font family

### Navigation

* **Landing Page**: Home page with CLI command and quick access to positions
* **Sidebar**: Persistent sidebar on dashboard pages with logo and wallet status
* **Logo Navigation**: Click the Cartha logo to return to the landing page
* **Breadcrumbs**: Clear navigation paths between pages

## Troubleshooting

### "Wrong Network" Error

**Problem**: UI shows "Wrong Network" message

**Solution**:

1. Check your wallet is connected to Base Sepolia (Chain ID: 84532)
2. Switch networks in your wallet
3. Refresh the page

### "Wallet Address Mismatch" Warning

**Problem**: UI shows warning that connected wallet doesn't match required owner

**Solution**:

1. Click "Disconnect" button
2. Connect the correct wallet that matches the `--owner-evm` address
3. Verify the address matches before proceeding

### "Transaction Failed" Error

**Problem**: Transaction fails when trying to execute

**Solution**:

* **Check Network**: Ensure you're on Base Sepolia
* **Check Gas**: Ensure you have enough ETH for gas fees
* **Check Balance**: Ensure you have enough USDC
* **Check Approval**: For Phase 2, ensure Phase 1 approval completed successfully
* **Check Network Congestion**: Wait a moment and retry

### "Extend" or "Top Up" Not Working

**Problem**: Extend or Top Up buttons don't work

**Solution**:

* These features are currently in testing
* Contact support on Discord if you need to extend or top up
* Use the CLI or contact support for manual assistance

### Positions Not Showing

**Problem**: "My Positions" page shows no positions

**Solution**:

1. Ensure your wallet is connected
2. Verify you're using the correct wallet address
3. Click "Refresh" button to reload positions
4. Check that your locks were created successfully on-chain
5. Verify the verifier has detected your locks (check with `cartha miner status`)

## Best Practices

### Creating Locks

1. **Always Use CLI First**: Start with `cartha vault lock` to ensure proper signature generation
2. **Verify Wallet**: Double-check the wallet address matches before approving
3. **Check Network**: Always verify you're on Base Sepolia (testnet) or Base Mainnet (mainnet)
4. **Have Gas Ready**: Ensure you have enough ETH for both approval and lock transactions
5. **Wait for Confirmation**: Don't close the UI until transactions are confirmed

### Managing Positions

1. **Regular Checks**: Visit "My Positions" regularly to monitor expiration dates
2. **Plan Extensions**: Extend locks before they expire to avoid interruption
3. **Monitor Status**: Check that positions show "Active" or "In Next Epoch" status
4. **Use Refresh**: Click refresh if positions seem outdated

### Security

1. **Verify URLs**: Always use the official URL: https://cartha.finance
2. **Check Addresses**: Verify all addresses match before signing transactions
3. **Review Parameters**: Always review transaction parameters before executing
4. **Keep CLI Updated**: Ensure your CLI is up-to-date for best compatibility

## Future Features

The Cartha Interface is actively being developed. Upcoming features include:

* ✅ **Automated Faucet**: Self-service testnet token faucet (now available!)
* ✅ **Improved Extend/Top Up**: Full support for extending and topping up positions
* ✅ **Transaction History**: View history of all your lock transactions
* ✅ **Notifications**: Alerts for expiring positions
* ✅ **Multi-Chain Support**: Support for additional chains beyond Base
* ✅ **Advanced Analytics**: Detailed analytics and insights for your positions

## Getting Help

* **Documentation**: See the [Miner Guide](miner-guide.md) for detailed setup instructions
* **Discord**: Join our Discord for support: https://discord.gg/zGkW2kTsGM
* **CLI Help**: Run `cartha --help` or `cartha vault lock --help` for CLI assistance
* **GitHub**: Report issues on the [cartha-lock-ui repository](https://github.com/General-Tao-Ventures/cartha-lock-ui)

***

**Note**: The Cartha Interface is currently optimized for testnet use. Mainnet support will be available when the Cartha subnet launches on mainnet.
