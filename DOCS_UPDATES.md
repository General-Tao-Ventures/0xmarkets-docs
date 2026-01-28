# Documentation Updates - Federated Miners Rebranding

## Summary
Updated all documentation to reflect the removal of "Regular LPs" and the rebranding of "Miner LPs" to "Federated Miners" across the cartha-lock-ui frontend.

## Files Modified

### 1. testnet/miner-guide.md
**Changes:**
- Removed reference to "Regular LPs and Miner LPs" two-option choice
- Updated to reflect new single-page design with Federated Miners
- Updated screenshot references to use new filenames:
  - `paste-your-or-principal-miner-hotkey.png` (was: paste-your-or-a-principal-miner-hotkey.jpeg)
  - `select-available-pools.png` (was: choose-a-pool.jpeg)
  - `input-amount.png` (was: enter-amount.jpeg)
  - `input-lock-days.png` (was: enter-lock-days.jpeg)
  - `continue.png` (was: wait-5-sec-to-redirect-here-and-lock-deposit.jpeg)
- Updated step descriptions to match new UI flow
- Simplified Quick Start checklist to remove "Become a Miner LP" reference

**Line Changes:**
- Line 152: "You'll see the **Federated Miners** option with a lock flow form on the right"
- Line 158: Updated screenshot path
- Line 164-172: Updated all screenshot paths to new filenames
- Line 182: Updated continue button screenshot
- Line 400: Simplified to "Click 'Become an LP'" (removed "→ 'Become a Miner LP'")

## Screenshot Files Status

### New Screenshots (in .gitbook/assets/)
✅ paste-your-or-principal-miner-hotkey.png
✅ select-available-pools.png
✅ input-amount.png
✅ input-lock-days.png
✅ continue.png

### Existing Screenshots (still referenced)
✅ become-an-lp-navbar.png
✅ connect-wallet.jpeg
✅ approve-USDC-limit.jpeg
✅ check-lock-position.jpeg
✅ wait-30s-5m-refresh-to-check-position.jpeg
✅ final-my-positions-page.png

## Verification

All references to "Regular LP" have been removed from:
- [x] testnet/miner-guide.md
- [x] No other files contained "Regular LP" references (verified via grep)

## Next Steps (if needed)

1. Ensure all new screenshot files are present in `.gitbook/assets/` folder
2. Verify screenshots are up-to-date with latest UI design
3. Update cartha-lock-ui.md if the CLI-based flow documentation needs updates
4. Consider updating participants/README.md if any terminology needs alignment

## Related Frontend Changes

The frontend (cartha-lock-ui) has been updated to:
- Remove all Regular LP components and routes
- Rename "Miner LPs" to "Federated Miners" throughout
- Combine description and lock flow into single two-column page
- Add Important Information section to the main page

