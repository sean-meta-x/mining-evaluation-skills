# Mining M&A — Buyside Valuation & Deal Structuring

Use this reference when the task is **pricing an acquisition** (not just valuing an asset): a fund or company buying into a mineral project, negotiating consideration, structuring earn-outs, or modeling investor returns. It extends the asset-level methods in `economic-feasibility.md` with the deal-level layer between "what the asset is worth" and "what the buyer should pay."

Core principle: **asset NPV is the ceiling of the analysis, not the answer.** The buyside price emerges from NPV after (1) attributable-interest correction, (2) risk-factor decomposition, (3) consideration structure, and it must be cross-checked against (4) market anchors and (5) investor-return arithmetic.

---

## 1. Perimeter and attributable interest (可归属权益)

Before any multiplication by a stake percentage, establish what the seller can actually deliver:

- **Registered holding ≠ free control.** Check for share pledges, repurchase ("sale-and-buyback") arrangements, debt-settlement transfers, and unexplained custodian/nominee blocks. A 62.87% registered stake with a third pledged is not a 62.87% deliverable stake.
- **Minority leakage.** If the target asset sits under a listed or partly-owned operating entity, headline asset NPV must be multiplied by the *effective attributable interest* before the deal-stake percentage is applied. Skipping this is the single most common buyside overvaluation (in one reviewed case it inflated the price benchmark by ~45%).
- **Market-cap anchors.** Where any entity in the holding chain is listed, its market capitalization is a live, dated anchor. A large gap between DCF and chain market caps is not an arbitrage flag by default — it prices restart risk, encumbrances, and control friction. Record the anchor with source and date.

## 2. From asset NPV to price: risk-factor decomposition

A single "risk factor" multiplier (e.g. ×0.35) drives the conclusion more than every DCF input combined, so it must be decomposed and documented, never asserted:

- Split into **named, independent factors** multiplied together, e.g. ① title/closing deliverability × ② execution (restart, permits, timeline) × ③ geological delivery (grade/tonnage reconciliation). Three factors of 0.8/0.72/0.65 ≈ 0.37 is arguable; a bare 0.37 is not.
- **State the semantics** — probability of success, or price-of-risk discount — and check for double counting against the discount rate and any price haircut already taken.
- **Scenario bands per factor**, not per conclusion: conservative/base/optimistic values for each factor, so scenario results can be attributed.
- **Reconciliation risk is a factor, not a footnote.** If actual plant feed grade materially underruns reserve grade (e.g. 1–2 g/t processed vs 7.7 g/t reserve), model a delivered-grade scenario explicitly; do not bury it in the multiplier.

## 3. The vintage-data trap (时代错配)

Old feasibility studies age asymmetrically: **prices get updated, costs quietly don't.**

- Inflate FS-era OPEX/CAPEX to valuation-date currency (2018→2026 mining cost inflation was roughly +30–40%). Using current metal prices against 8-year-old nominal costs overstates margin structurally.
- Rebuild CAPEX bottom-up: restart capex ≠ FS initial capex; add closure (industry order-of-magnitude, not the FS token number), working capital, and buyer-funded exploration.
- Old independent valuations are **evidence about risk, not about value**: a 2013 FMV of US$341M premised on 2014 production start and unencumbered title, in a project still not producing in 2026, is an argument *for* heavy execution discounting — cite it that way.

## 4. Consideration structure: cash-at-close vs milestones

- **Cap cash-at-close at what the conservative case supports.** Value above the conservative case rides on unverified premises (drilling, permits, restart) — pay for it only when the premise verifies: earn-out/milestone tranches tied to *verifiable, third-party events* (infill drilling confirming grade; tailings facility approval; JORC conversion; production permits like Indonesia's RKAB).
- **Non-compliant resources cannot carry DCF weight at close.** For non-JORC/NI 43-101 resources (especially majority-Inferred), price cash-at-close on a resource multiple (US$/t or US$/oz in-ground, market-calibrated) and demote the DCF to a scenario reference; the DCF value becomes the milestone tranche.
- **Net debt and contingent liabilities** reduce consideration at close, dollar-for-dollar; state explicitly whether the valuation is enterprise or equity.

## 5. Fund-return modeling (基金回报测算)

Price the entry with the investor's arithmetic, not only the asset's:

- **Dual-scenario tree** (delivered / not-delivered) with explicit probability, not a single expected NPV. Report IRR and MOIC per branch and probability-weighted, across 2–3 candidate entry prices. The negotiation insight is usually that returns are more sensitive to entry price than to asset performance.
- **Structure restart funding as debt**, not equity top-up: interest-bearing shareholder loans recovered at exit protect the downside branch and are a genuine term-sheet lever.
- **Exit value needs two independent methods.** A scenario-NAV exit should be cross-checked with production-based pricing at the exit date: run-rate EBITDA × a *short-remaining-life* multiple (2.0–3.5× for <5 years of reserves — never the 4–7× quoted for long-life producers), and remaining-NAV × P/NAV (0.8–1.0 for a producing single-asset miner). Keep market variables (metal price, multiple) separate from execution variables (delivered vs not) so the tree doesn't smuggle a bull-market assumption into the "success" branch.
- **Timing risk is quantifiable**: one year of exit delay typically costs 2–3 points of expected IRR at these structures; jurisdictions with capital controls (see regional references) make delay the base case, not the tail.

## 6. Nominal vs economic consideration (名义对价 vs 经济对价)

When the seller must reinvest proceeds into the buyer's shares (lock-ups, escrow, loop structures) or bears heavy transfer taxes, the seller's *economic* consideration can be ~0.6–0.8× the nominal price. Two consequences:

- A rational seller inflates the nominal ask to compensate — benchmark "seller's ask vs fair value" on the economic number, not the headline.
- Negotiating room lives in the structure (lock-up length, cash ratio, tax gross-ups), often more cheaply than in the headline price.
- **Compliance first**: reinvestment loops, undisclosed side letters ("drawer agreements"), and dispersed nominee subscriptions are, in most listing regimes, round-tripping / disclosure / acting-in-concert violations. Flag them as deal-breakers requiring restructuring, not as terms to model.

## 7. Listed-buyer injection and market reaction

If stage two is injection into a listed vehicle:

- **Valuation-basis gap**: the market prices coal (historic median EV/EBITDA ≈ 4×, ESG-constrained capital) very differently from gold (P/NAV in a strong gold tape). Sequencing injections by market receptivity (crowd-pleasing asset first; unverified asset after JORC/permits) can matter more than the assets themselves.
- **Diluted per-share value as the pricing benchmark**: post-injection market value ÷ post-placement share count is the reference price for placements and seller reinvestment. Pricing new shares at the *pre-deal* price instead transfers measurable value to subscribers — compute it and put it on the negotiation ledger.
- **Micro-cap amplification**: for small listed buyers, announcement-day reactions of ±20–30% are normal; the driver distribution is disclosure quality and narrative (independent technical report, restart milestones, related-party clarity), not asset quality.

---

## Buyside checklist

1. Attributable interest established from a share register + encumbrance search, not the seller's deck?
2. Risk multiplier decomposed, semantics stated, double counting checked?
3. FS costs inflated to valuation-date money; closure/working capital/exploration added?
4. Cash-at-close ≤ conservative case; milestones tied to third-party-verifiable events?
5. Non-compliant resources priced by multiple, not DCF?
6. Fund IRR/MOIC computed per entry price with a probability tree; exit cross-checked by production-based methods?
7. Economic (not nominal) consideration benchmarked; structure risks flagged to counsel?
8. Net debt / contingent liabilities to be deducted at close?
9. All prices, market caps and FX carry a source and date?
10. Stated plainly that this supports negotiation and does not replace a QP/licensed valuer?
