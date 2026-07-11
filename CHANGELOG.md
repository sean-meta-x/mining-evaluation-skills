# Changelog

All notable changes to `mining-evaluation-skills` are documented here.

## v1.4 — M&A buyside module and Indonesia regulatory reference

Field-tested additions from a live Indonesia dual-asset (gold + coal) acquisition engagement.

**Added — `references/ma-buyside.md`**: the deal-level layer between asset NPV and acquisition price — attributable-interest correction (registered vs deliverable stakes, minority leakage), decomposed risk factors with stated semantics (title × execution × geological delivery), the vintage-data trap (old-FS costs vs current prices), cash-at-close vs milestone/earn-out structuring (non-compliant resources priced by multiple, not DCF), fund IRR/MOIC dual-scenario modeling with production-based exit cross-checks (short-remaining-life EBITDA multiples, remaining-NAV × P/NAV), nominal-vs-economic consideration, and listed-buyer injection / market-reaction sequencing. Ends with a 10-point buyside checklist.

**Added — `references/indonesia-regulatory.md`**: Indonesia-specific screen — licensing reality (IUP/RKAB/IPPKH/AMDAL timelines), 49% divestment (listing is not an exemption; Vale precedent), the 2025 fiscal reset (PP 18/19 2025 royalties, gold doré export tax, proposed coal export duty), PP 8/2025 export-proceeds retention (100%/12-month cash trap) with IRR guidance, UU 2/2025 discretionary licensing, artisanal-mining and election-cycle risk, and standard mitigations (BIT/ICSID structuring, political-risk insurance). Includes a 10-item quick screen.

**Changed — `SKILL.md`**: Step 1 focus list now routes M&A/buyside pricing, earn-out structuring, and investor-return modeling to `references/ma-buyside.md`, and Indonesia-related tasks additionally to `references/indonesia-regulatory.md`. Frontmatter description extended with acquisition-pricing and Indonesia triggers.

Both references follow the existing house rules: no fabricated numbers, date-stamp every market/regulatory data point, and defer to QP/licensed-valuer sign-off for formal use.

## v1.3 — Optimized fork: trigger accuracy, price freshness, python-docx support

Community-optimized build based on upstream v1.2 (github.com/Hap-hub/mining-evaluation-skills).

**Fixed — description/content drift**: the frontmatter description only listed the original 10 metals, so queries about molybdenum, tungsten, scheelite, zirconium, or titanium (added in v1.1) could fail to trigger the skill. The description now lists all 13 metals, and additionally covers mining-company investment due diligence queries.

**Added — price and benchmark freshness rule** (SKILL.md Step 2): reference-file prices and cut-off benchmarks are static and can silently go stale; the skill now instructs verifying current metal prices via web search before any price-dependent economic conclusion, and always stating the price and its date in the output.

**Added — python-docx font guidance**: the Chinese-font-consistency fix from v1.2 was docx-js-only; environments that build Word files with python-docx (e.g. Claude Cowork sandboxes) got no guidance. Added an equivalent helper pattern setting `w:eastAsia` per run.

## v1.2 — Fixed inconsistent fonts in Chinese docx reports

**Fixed**: generated Word reports containing Chinese content sometimes showed inconsistent fonts within the same paragraph (e.g. bolded figures or table cells rendering in a different font than surrounding body text).

**Root cause**: the docx-generation step was only setting font on specific `TextRun`s (e.g. bolded figures), leaving other runs without an explicit font. Word falls back to its theme default font for unset runs, and that fallback doesn't necessarily match a font set explicitly elsewhere in the same paragraph, producing visibly mismatched fonts.

**Fix**: `SKILL.md` now instructs setting the font once at the document level (`styles.default.document.run.font`, with both `name` and `eastAsia` set to **Microsoft YaHei**) rather than per run. All runs — headings, body text, bold figures, table cells — inherit this single consistent font unless a run deliberately needs to look different. Verified in the sandbox that this produces a single `rFonts` declaration in `styles.xml` with no conflicting per-run overrides in `document.xml`.

## v1.1 — Metals expansion, regional standards, terminology fixes

**Added — 5 new metal reference files** (`references/metals/`):
- `molybdenum.md` — mostly a porphyry Cu-Mo by-product; standalone porphyry Mo deposits also covered.
- `tungsten.md` — wolframite-focused general tungsten reference (market/strategic context shared with scheelite).
- `scheelite.md` — kept separate from `tungsten.md` because scheelite's skarn setting and flotation-based processing route differ materially from wolframite's typical quartz-vein/gravity-circuit case.
- `zirconium.md` — heavy mineral sands context, co-produced with titanium minerals.
- `titanium.md` — mineral sands (ilmenite/rutile/leucoxene) vs. hard-rock sources, and the rutile/ilmenite value distinction.

**Added — regional reporting standards** (merged into `references/reporting-standards.md` rather than split into separate files):
- Brazil — notes on CRIRSCO-aligned disclosure practice and the absence of a single dedicated Brazilian code; points to whichever home-listing code actually applies.
- Russia — GKZ classification (A/B/C1/C2) described as a standalone, historically independent system. Deliberately does **not** include a GKZ-to-CRIRSCO equivalence table: the mapping is genuinely contested industry-wide, and publishing an approximate conversion risked implying a false equivalence. Any real cross-system reclassification is flagged as requiring actual Qualified/Competent Person review, not a lookup table.
- South Africa — SAMREC code, noted as a close CRIRSCO-family cousin of JORC/NI 43-101, with the practical differences (JSE listing, local Competent Person qualification) called out.

**Added** — `references/terminology-glossary-zh.md`: a Chinese/English terminology reference correcting common mistranslation issues, specifically:
- 边界品位 / 截止品位 / 最低工业品位 — three terms often used interchangeably in Chinese that have distinct technical meanings; the file specifies which one corresponds to the English "cut-off grade."
- 资源量 vs. 储量 (Resource vs. Reserve) — flagged as a legally material distinction, not a stylistic one.
- Standard Chinese terms for Measured/Indicated/Inferred (探明/控制/推断资源量) and Proved/Probable Reserve.
- PEA/PFS/FS naming — specifically flags that Chinese "预可行性" corresponds to PFS, not PEA, a common mistranslation.
- Grade-tonnage curve and sensitivity analysis terminology.

SKILL.md updated to point to the new metal files and to direct Claude to consult the terminology glossary before finalizing Chinese-language responses.

**Not included in this release** (deliberately deferred):
- No metal-specific cost/payability figures were added beyond qualitative ranges — consistent with the skill's existing approach of not asserting numbers the user hasn't supplied.
- No GKZ↔CRIRSCO conversion table — see above.
- No USGS/BGS or other external geological-data integration — out of scope for this release.

## v1.0 — Initial release

- Core evaluation domains: resource estimation, economic feasibility (PEA/PFS/FS), risk assessment, reporting standards (NI 43-101/JORC/CRIRSCO), ESG/sustainability.
- 8 metal reference files: copper, gold, lithium, cobalt, lead-zinc, niobium-tantalum, nickel, rare-earth.
- Scripts: grade-tonnage calculator, financial model (NPV/IRR/payback), resource classification checklist.
- Report templates: resource estimation report, PEA/PFS/FS summary, risk assessment matrix.
