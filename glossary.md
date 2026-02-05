# Glossary

**Epoch:** A fixed time period for calculating miner rewards. Cartha uses weekly epochs running Friday 00:00 UTC → Thursday 23:59 UTC. See [Weekly Epochs](how-it-works/weekly-epochs.md).

**Epoch Freeze:** The moment (Friday 00:00 UTC) when the miner list is frozen for reward calculation. Positions must be verified before the freeze to earn rewards that week.

**Frozen Epoch:** The current epoch where rewards are being earned. Miner positions are locked and weights are calculated based on the frozen snapshot.

**Upcoming Epoch:** The next epoch being prepared. New miners are added here and will start earning after the next freeze.

**Perpetual Future (Perp):** A futures contract with no expiry; funding keeps prices anchored.

**Funding Payments:** Periodic payments between longs/shorts to align perp price with index; the treasury may take an optional share.&#x20;

**Liquidation:** Automatic position close when margin is insufficient; a **10% fee** is applied and split among validators, insurance, and buyback.&#x20;

**veALPHA:** Vote‑escrowed ALPHA; longer lock → higher voting weight and fee share.&#x20;
