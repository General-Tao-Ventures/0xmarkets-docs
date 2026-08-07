# Audits

Smart-contract security comes from two things: the design the contracts are built on, and independent review of the specific code that's deployed. This page is honest about where each stands at Beta.

> **0xMarkets launches in Beta.** The exchange is live, but still maturing. A clean audit reduces risk — it does not remove it. No audit can guarantee that software is free of bugs. Trade accordingly, and read [Risk disclosures](risk-disclosures.md).

## The contract architecture

0xMarkets is built on a **GMX v2-style perpetuals architecture** — a widely-used, battle-tested design for on-chain perps. This matters for security:

- The core mechanics (pool-based liquidity, oracle-priced execution, two-step keeper settlement, dynamic maintenance margin, funding and borrowing) follow patterns that have been deployed, reviewed, and run at scale across the industry.
- Using a proven design means the highest-risk parts of the system are not novel experiments — they are established patterns, adapted for a multi-asset (FX, commodities, crypto) exchange.

A proven base lowers risk. It does not replace an audit of *this* deployment: 0xMarkets adapts the architecture for its own markets, oracle setup, and parameters, and that adapted code is what needs independent review.

## Third-party audit status

0xMarkets has been through two independent security reviews:

- **Hashlock — completed.** An initial audit by Hashlock covering the liquidity-engine infrastructure has been completed. Report: [hashlock.com/audits/cartha](https://hashlock.com/audits/cartha).
- **HackenProof — in progress.** A comprehensive, **end-to-end** security review of the full exchange is currently underway with HackenProof: [hackenproof.com/companies/0xmarkets](https://hackenproof.com/companies/0xmarkets). Results will be published here once complete.

Because the end-to-end review is still in progress, the exchange launches as **Beta** — see below.

## What an audit does and doesn't do

- **It does:** surface known classes of vulnerability, logic errors, and economic edge cases before they reach production.
- **It doesn't:** guarantee the absence of bugs, cover code changed after the review, or remove market, oracle, or liquidation risk.

This is part of why the launch is branded **Beta** — and why you should never trade more than you can afford to lose. See [Risk disclosures](risk-disclosures.md).

## Next

- [Oracle security](oracle-security.md)
- [Insurance fund](insurance-fund.md)
- [Risk disclosures](risk-disclosures.md)
