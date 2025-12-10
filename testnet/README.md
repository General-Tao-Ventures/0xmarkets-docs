# Cartha Testnet

**Cartha Testnet** is a public testing environment for the Cartha Subnet (SN35) that powers 0xMarkets DEX. The testnet allows miners, validators, and developers to test the full functionality of the Cartha subnet before deploying to mainnet.

**Repositories:**
- **Miner CLI**: [cartha-cli](https://github.com/General-Tao-Ventures/cartha-cli)
- **Validator**: [cartha-validator](https://github.com/General-Tao-Ventures/cartha-validator)

## What is Cartha Testnet?

Cartha Testnet is a fully functional replica of the Cartha subnet running on Bittensor's testnet network. It provides:

- **Real vault contracts** deployed on Base Sepolia testnet
- **Testnet TAO** for subnet registration (no real cost)
- **Testnet USDC** for liquidity provision testing
- **Full miner and validator functionality** identical to mainnet
- **Safe testing environment** without financial risk

## What Can You Do on Cartha Testnet?

### For Miners (Liquidity Providers)

- **Test liquidity provision** without risking real funds
- **Practice registration** and hotkey management
- **Experiment with different pools** (BTC/USD, ETH/USD, EUR/USD)
- **Use the Cartha Lock UI** for a streamlined lock/unlock experience (no BaseScan needed!)
- **View and manage positions** through the web interface
- **Extend locks and top up** existing positions (currently in testing)
- **Understand reward mechanisms** and epoch cycles
- **Test multi-pool strategies** with testnet USDC

### For Validators

- **Test validator scoring logic** and weight distribution
- **Practice liquidation execution** (when available)
- **Test validator infrastructure** and monitoring
- **Understand epoch cycles** and weight publishing
- **Validate verifier integration** and API endpoints

### For Developers

- **Test smart contract interactions** with real vault contracts
- **Use the Cartha Lock UI** for testing the frontend lock flow
- **Develop integration tools** and automation scripts
- **Test API endpoints** and verifier functionality
- **Build monitoring dashboards** and analytics tools
- **Experiment with different strategies** safely

## Testnet Configuration

### Network Details

- **Bittensor Network**: `test` (Bittensor testnet)
- **Subnet UID**: `78` (Cartha testnet subnet)
- **EVM Chain**: Base Sepolia (Chain ID: `84532`)
- **Verifier URL**: `https://cartha-verifier-826542474079.us-central1.run.app`
- **Lock UI URL**: `https://cartha.finance` (for managing locks and positions)

### Testnet Tokens

- **Testnet TAO**: Required for subnet registration
  - Faucet: https://app.minersunion.ai/testnet-faucet
- **Testnet ETH**: Required for gas fees on Base Sepolia
  - Faucet: https://console.optimism.io/faucet (select Base Sepolia)
  - Alternative: https://www.alchemy.com/faucets/base-sepolia
- **Testnet USDC**: Required for liquidity provision
  - **Faucet**: https://cartha.finance/faucet
  - **Claim Amount**: 1,000,000 USDC per claim
  - **Cooldown**: 24 hours between claims (per wallet address)


## Getting Started

Choose your path:

- **[Miner Guide](miner-guide.md)** - Learn how to run miners on Cartha testnet
- **[Validator Guide](validator-guide.md)** - Learn how to run validators on Cartha testnet
- **[Cartha Lock UI](cartha-lock-ui.md)** - Learn about the web interface for managing lock positions

## Testnet vs Mainnet

### Key Differences

| Feature | Testnet | Mainnet |
|---------|---------|---------|
| **Network** | Bittensor testnet | Bittensor finney |
| **Subnet UID** | 78 | 35 |
| **EVM Chain** | Base Sepolia | Base Mainnet |
| **Tokens** | Testnet tokens (no value) | Real tokens (real value) |
| **Cost** | Free (testnet TAO) | Requires real TAO |
| **Purpose** | Testing & development | Production use |

### When to Use Testnet

- ✅ Testing new features before mainnet deployment
- ✅ Learning how the system works
- ✅ Developing integration tools
- ✅ Testing validator logic and scoring
- ✅ Experimenting with different strategies

### When to Use Mainnet

- ✅ Ready for production deployment
- ✅ Want to earn real rewards
- ✅ Confident in your setup and understanding
- ✅ Have sufficient capital for minimum requirements

## Getting Help

### Resources

- **CLI Documentation**: [Cartha CLI Testnet Guide](https://github.com/General-Tao-Ventures/cartha-cli/tree/main/testnet)
- **Validator Documentation**: [Cartha Validator Testnet Setup](https://github.com/General-Tao-Ventures/cartha-validator/blob/main/docs/TESTNET_SETUP.md)
- **Discord**: https://discord.gg/7DXG57B6
Contact Cartha team for testnet USDC and support 

### Common Issues

- **Need testnet USDC**: Visit https://cartha.finance/faucet to claim 1,000,000 USDC (24-hour cooldown between claims)
- **Validator not whitelisted**: Contact subnet owner
- **Transaction failures**: Check network (Base Sepolia), gas (testnet ETH), and balances
- **Registration issues**: Verify testnet TAO balance and network settings
- **Wallet address mismatch**: Ensure the wallet connected in the Cartha Lock UI matches the `--owner-evm` address specified in the CLI
- **Extend/Top Up not working**: These features are currently in testing - contact support if you encounter issues

## Next Steps

1. **For Miners**: See the [Miner Guide](miner-guide.md) to get started
2. **For Validators**: See the [Validator Guide](validator-guide.md) to get started
3. **For Developers**: Explore the API endpoints and build integration tools
4. **Join the Community**: Connect with other testnet participants on Discord/Telegram

---

**Note**: Testnet is a testing environment. All tokens are testnet tokens with no real value. Use testnet to learn, test, and develop before deploying to mainnet.
