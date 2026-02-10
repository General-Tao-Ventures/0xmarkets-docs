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

---

# Documentation Updates - Incentive Pool Rebranding

## Summary
Updated all documentation to rebrand the "trader pool" / "trader emissions" to "incentive pool" to reflect that this 10% ALPHA allocation can be used to incentivize any party in the ecosystem, not just traders. This makes the allocation more flexible for airdrops, community programs, and other ecosystem initiatives.

## Conceptual Change
**Before:** 10% of ALPHA emissions was specifically for traders and IBs (Introducing Brokers)
**After:** 10% of ALPHA emissions goes to a flexible "incentive pool" that can be used for:
- Trading rewards (weekly leaderboards)
- IB rebates
- Airdrops to any party
- Community programs and ecosystem growth initiatives

## Files Modified

### 1. faq.md
**Changes:**
- Replaced FAQ question "What rewards do traders earn?" with "What is the incentive pool?"
- Updated answer to emphasize flexibility: "Can be used to incentivize any party in the ecosystem"
- Changed ALPHA emission distribution from "10% to traders & IBs" to "10% to incentive pool (airdrops and ecosystem rewards)"

**Key Updates:**
- Lines 44-49: New FAQ explaining the incentive pool concept
- Lines 91-94: Updated ALPHA emissions distribution list

### 2. cartha/README.md
**Changes:**
- Updated emissions distribution summary to use "incentive pool" instead of "traders"
- Modified "For Traders" section to say "Earn from incentive pool" instead of "Earn 10% of ALPHA emissions"

**Key Updates:**
- Line 15: "10% to incentive pool" instead of "10% to traders"
- Line 46: "Earn from incentive pool through weekly leaderboard rewards"

### 3. how-it-works/fees-and-rewards.md
**Changes:**
- Renamed section from "Trader Rewards" to "Incentive Pool Distribution"
- Completely rewrote to emphasize flexibility and multiple use cases
- Added bullet points for trading rewards, IB rebates, airdrops, and community programs

**Key Updates:**
- Line 15: "10% → Incentive Pool: Flexible allocation for ecosystem incentives"
- Lines 18-27: New comprehensive "Incentive Pool Distribution" section replacing trader-specific content

### 4. litepaper.md
**Changes:**
- Updated traders section to say "Earn from incentive pool" instead of "Earn 10% of ALPHA emissions"
- Changed ALPHA emission distribution to "incentive pool - flexible allocation for ecosystem incentives"

**Key Updates:**
- Line 84: "Earn from incentive pool via weekly leaderboards and IB rebates"
- Line 96: "10% to incentive pool - flexible allocation for ecosystem incentives (airdrops, trading rewards, IB rebates)"

### 5. participants/traders.md
**Changes:**
- Updated page header to say "Earn from incentive pool" instead of "Earn 10% of ALPHA emissions"
- Changed "Traders on 0xMarkets earn" to "Traders on 0xMarkets can earn from the incentive pool"
- Updated "trader allocation" to "incentive pool allocation"
- Changed "trader emission pool" to "incentive pool" (appears twice)
- Updated "Trader rewards" to "Rewards from the incentive pool"

**Key Updates:**
- Line 5: "Earn from incentive pool through weekly leaderboard rewards and IB rebates"
- Line 9: "can earn from the **incentive pool** (10% of total subnet ALPHA emissions)"
- Line 15: "ALPHA rewards from the incentive pool allocation"
- Line 22: "IB rebates come from the same 10% incentive pool"
- Lines 26-29: Updated reward flow description to use "incentive pool" terminology

## Verification

All references have been successfully updated:
- [x] "trader pool" → "incentive pool" ✓
- [x] "trader emission pool" → "incentive pool" ✓
- [x] "reward pool" → "incentive pool" ✓
- [x] "trader allocation" → "incentive pool allocation" ✓
- [x] "10% to traders" → "10% to incentive pool" ✓
- [x] No remaining references to trader-specific 10% allocation ✓

## Impact

This change allows the protocol to:
1. Use the 10% allocation more flexibly for ecosystem growth
2. Conduct airdrops to various parties (miners, validators, community members, etc.)
3. Launch new incentive programs without being constrained to traders only
4. Better communicate that this is a flexible incentive mechanism

## Related Files NOT Changed

The following files were checked but did not contain relevant references:
- glossary.md (no trader allocation references)
- changelog.md (empty file)
- roadmap.md (empty file)
- weekly-epochs.md (no trader allocation references)
- governance-vealpha.md (no trader allocation references)
- safety-and-liquidations.md (no trader allocation references)
- All testnet/ files (no trader allocation references)
- All diagrams/ files (image-only references)
