# Documentation Updates - Federated Miners Rebranding

## Summary
Updated all documentation to reflect the removal of "Regular LPs" and the rebranding of "Miner LPs" to "Federated Miners" across the cartha-lock-ui frontend.

**Major improvement:** Reorganized the wallet connection flow to make logical sense. Previously, step 8 asked users to "Connect your wallet" during the lock funds process, but users would have already connected their wallet when claiming USDC from the faucet. The wallet connection is now properly positioned at step 3 in the faucet section, with a simple reminder in the lock funds section.

## Files Modified

### 1. testnet/miner-guide.md
**Changes:**
- Removed reference to "Regular LPs and Miner LPs" two-option choice
- Updated to reflect new single-page design with Federated Miners
- **Reorganized wallet connection flow** - Moved wallet connection from Step 8 (Lock Funds section) to Step 3 (Faucet section)
  - Makes more sense since wallet must be connected to claim USDC from faucet
  - Added reminder note in Lock Funds section that wallet should already be connected
- Updated screenshot references to use new filenames:
  - `wallet-connect.png` - NEW screenshot for wallet connection (Step 3 in Faucet)
  - `paste-your-or-principal-miner-hotkey.png` (was: paste-your-or-a-principal-miner-hotkey.jpeg)
  - `select-available-pools.png` (was: choose-a-pool.jpeg)
  - `input-amount.png` (was: enter-amount.jpeg)
  - `input-lock-days.png` (was: enter-lock-days.jpeg)
  - `continue.png` (was: wait-5-sec-to-redirect-here-and-lock-deposit.jpeg)
- Updated step descriptions to match new UI flow
- Simplified Quick Start checklist to remove "Become a Miner LP" reference
- Renumbered steps in Lock Funds section (now 8-12 instead of 8-13)

**Key Line Changes:**
- Line 73-75: Added wallet connection as step 3 in Faucet section with new screenshot
- Line 77: Renumbered faucet claim to step 4
- Line 156: "You'll see the **Federated Miners** option with a lock flow form on the right"
- Line 160: Added note about wallet already being connected from faucet step
- Line 164-178: Updated all screenshot paths to new filenames
- Line 180: Changed section header from "Connect Wallet and Execute Transaction" to just "Execute Transaction"
- Line 182-204: Renumbered steps 8-12 (was 8-13)
- Line 400: Simplified to "Click 'Become an LP'" (removed "→ 'Become a Miner LP'")

## Screenshot Files Status

### New Screenshots (in .gitbook/assets/)
✅ wallet-connect.png - NEW: Wallet connection during faucet step
✅ paste-your-or-principal-miner-hotkey.png
✅ select-available-pools.png
✅ input-amount.png
✅ input-lock-days.png
✅ continue.png

### Existing Screenshots (still referenced)
✅ become-an-lp-navbar.png
✅ landing-page.jpeg
✅ faucet-navbar.jpeg
✅ claim-USDC.jpeg
✅ approve-USDC-limit.jpeg
✅ check-lock-position.jpeg
✅ wait-30s-5m-refresh-to-check-position.jpeg
✅ final-my-positions-page.png

### Screenshots No Longer Used
❌ connect-wallet.jpeg - Replaced by wallet-connect.png and moved to faucet section

## Verification

All references to "Regular LP" have been removed from:
- [x] testnet/miner-guide.md
- [x] No other files contained "Regular LP" references (verified via grep)

## Next Steps (if needed)

1. Ensure all new screenshot files are present in `.gitbook/assets/` folder
2. Verify screenshots are up-to-date with latest UI design
3. Update cartha-interface.md if the CLI-based flow documentation needs updates
4. Consider updating participants/README.md if any terminology needs alignment

## Related Frontend Changes

The frontend (cartha-lock-ui) has been updated to:
- Remove all Regular LP components and routes
- Rename "Miner LPs" to "Federated Miners" throughout
- Combine description and lock flow into single two-column page
- Add Important Information section to the main page

