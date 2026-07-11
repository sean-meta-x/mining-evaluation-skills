---
name: mining-evaluation-skills
description: Use for any mining/mineral project evaluation or M&A task: resource estimation, grade-tonnage analysis, economic feasibility (PEA/PFS/FS), cut-off sensitivity, risk assessment, and NI 43-101/JORC/CRIRSCO reporting. Trigger when a geologist, investor, or analyst asks to interpret drill/assay data, evaluate project viability, draft or review a technical/investment report, compare resource categories (Measured/Indicated/Inferred), or estimate NPV/IRR for a mine plan; covers copper, gold, lithium, cobalt, lead-zinc, niobium-tantalum, nickel, rare earths, molybdenum, tungsten, scheelite, zirconium, titanium. Also trigger for buyside M&A (acquisition pricing, attributable interest, earn-out structuring, fund IRR/MOIC modeling), Indonesian mining regulation (IUP/RKAB/IPPKH, divestment, royalties, DHE), ESG or mining-method questions on a project, and due diligence on resource quality or mine economics. Do not trigger for generic investing or geology trivia.
---

# Mining Evaluation Skills

## What this skill is for

This skill turns Claude into a working aid for **exploration geologists and mining investors** who need to interpret mineral project data and produce evaluation outputs that hold up against industry-standard frameworks (CRIRSCO-family codes: NI 43-101, JORC, SAMREC, etc.).

The core job is almost always the same shape: the user hands you raw or partially-processed data (assay tables, drill logs, a PEA cash-flow summary, a resource statement, a risk register) and wants either (a) an interpretation of what it means, or (b) a structured report/section built from it. Treat this as **data interpretation first, document generation second** — a sharp reading of the numbers is worth more to these users than a polished template with generic filler.

## Language

Respond in the language the user is writing in (the skill defaults to English internally, but adapt output — including report headers — to match the user's query language). If the user mixes languages or asks for a specific report language, follow that instruction over the query language.

When responding in Chinese, consult `references/terminology-glossary-zh.md` before finalizing terminology — several mining terms (grade/cut-off distinctions, Resource vs. Reserve, PEA/PFS/FS naming, resource category names) get mistranslated or merged by generic translation in ways that change technical or legal meaning. Use the corrected terms from that file even if the user's own phrasing uses a conflated or imprecise term, and briefly flag the distinction rather than silently mirroring an imprecise term back.

## Step 1: Figure out what's actually being asked

Before producing anything, identify:

1. **Evaluation focus** — which of these is the actual ask (often more than one):
   - Resource estimation / grade-tonnage → `references/resource-estimation.md`
   - Economic feasibility (PEA/PFS/FS) → `references/economic-feasibility.md`
   - Risk assessment → `references/risk-assessment.md`
   - Reporting/compliance (NI 43-101, JORC, CRIRSCO) → `references/reporting-standards.md`
   - ESG / sustainability / mining method choice → `references/esg-sustainability.md`
   - M&A / buyside pricing, deal structuring, investor returns → `references/ma-buyside.md`
   - Indonesia regulatory / political risk → `references/indonesia-regulatory.md` (in addition to the topical file above)
2. **Commodity** — if the user names or implies a specific metal, check `references/metals/` for a file matching it: copper, gold, lithium, cobalt, lead-zinc, niobium-tantalum, nickel, rare-earth, molybdenum, tungsten, scheelite, zirconium, titanium. These give you commodity-specific benchmarks (typical grades, cut-offs, deposit types, processing routes, market drivers) so your interpretation isn't generic. Molybdenum, tungsten, and scheelite are closely related but kept as separate files because their processing routes diverge (see the note at the top of `tungsten.md`); the same applies to zirconium and titanium, which are usually co-produced from the same heavy mineral sand deposits but serve different end markets. If no specific metal is named, work generically and note that assumptions are commodity-agnostic.
3. **Project stage** — grassroots exploration vs. resource definition vs. PEA vs. PFS/FS vs. operating mine. This changes what data confidence and precision is reasonable to expect (see `references/economic-feasibility.md` for the accuracy bands of each stage).
4. **Audience** — a geologist wants technical precision and defensible methodology language; an investor wants risk-adjusted takeaways and comparability to peers. Calibrate the report's tone and level of jargon accordingly, but never fabricate confidence the data doesn't support — both audiences are worse served by false precision.

## Step 2: Interpret the data

Default mode is interpretation, not computation. Read what the user gives you (tables, CSVs, pasted assay results, cash-flow assumptions, drill spacing descriptions) and explain what it means, what's strong, what's missing, and what a reviewer (a Qualified/Competent Person, or an investor doing diligence) would flag.

**Only reach for a calculation script when the user has actually supplied the underlying data needed to compute something concrete** — e.g., a composite/block table with grades and tonnages, or cash-flow assumptions (capex, opex, price, recovery, discount rate). If the data isn't there, don't fabricate numbers to run a script against — ask for the missing inputs or clearly flag the gap, and give a qualitative read instead. This matters because a wrong or invented number in a mining evaluation report can materially mislead an investor.

Available scripts (see `scripts/README.md` for exact usage):
- `scripts/grade_tonnage_calculator.py` — tonnage/grade above a cut-off, and a cut-off sensitivity table, from a composite/block dataset.
- `scripts/financial_model.py` — NPV, IRR, and payback period from a cash-flow assumption set.
- `scripts/resource_classification_checklist.py` — a structured checklist (not an authoritative classifier) that walks through CRIRSCO-style confidence criteria to flag what supports/undermines a Measured/Indicated/Inferred claim.

**Price and benchmark freshness.** Metal prices, payability factors, and typical cut-off benchmarks in `references/` are indicative ranges captured at the time of writing, not live data — and commodity prices can move enough in months to flip a project's economics. Whenever an economic conclusion depends on a price assumption (NPV/IRR runs, cut-off sensitivity, "is this grade economic" judgments), verify the current spot/contract price with a web search if search is available, and state the price and its date in the output. If search isn't available, use the user's supplied price or clearly label the assumption as dated. Never present a reference-file price as current.

Resource classification and geostatistical estimation (kriging, variography) are technical disciplines that legally require a Qualified/Competent Person sign-off — this skill helps interpret and structure, but always note where professional certification would be required for a real filing.

## Step 3: Choose the output format for the scenario

Don't default to one format — match it to what's actually needed:

| Scenario | Format | How |
|---|---|---|
| Quick question, data interpretation, back-and-forth analysis | Markdown, inline in chat | Just respond directly |
| Formal report/section for investors, regulators, or a data room (e.g., "draft the resource estimation section", "write a PEA summary memo") | Word document (.docx) | Use the `docx` skill |
| Numeric model the user will want to manipulate — grade-tonnage curves, NPV/IRR sensitivity tables, resource category rollups | Excel (.xlsx) | Use the `xlsx` skill |
| Slide-style summary for a board/investor pitch | PowerPoint (.pptx) | Use the `pptx` skill |

If it's ambiguous, ask — but a reasonable default is: if the user says "report", "memo", "for investors/regulators", or references a filing standard, go formal (docx/xlsx); otherwise stay conversational.

When producing a formal report, use `assets/templates/` as a structural starting point (see below), not a form to fill mechanically — cut sections that don't apply and add ones the specific project needs.

**Font consistency for Chinese-language docx reports.** If the report contains Chinese text, set the font once at the document level rather than per run — setting it only on individual `TextRun`s (e.g. just the bolded figures or table cells) while leaving others unset causes Word to render the unset runs in a fallback font, producing visibly inconsistent fonts within the same paragraph. When building the document with docx-js, set it in the document's `styles.default.document.run.font`:
```javascript
const doc = new Document({
  styles: {
    default: {
      document: {
        run: { font: { name: "Microsoft YaHei", eastAsia: "Microsoft YaHei" } },
      },
    },
  },
  sections: [ /* ... */ ],
});
```
Setting both `name` and `eastAsia` to the same font (Microsoft YaHei) ensures Latin and Chinese characters resolve to one consistent typeface throughout the document, without needing to set `font` on every individual `TextRun`. Only override font on a specific run if that run intentionally needs to look different (e.g. a monospaced figure).

If the environment builds docx with python-docx instead of docx-js, the same principle applies but python-docx has no working document-level eastAsia default — set both the run font name and the `w:eastAsia` attribute on each run via a small helper:
```python
from docx.oxml.ns import qn
from docx.oxml import OxmlElement

def set_cjk_font(run, font_name="Microsoft YaHei"):
    run.font.name = font_name
    rPr = run._element.get_or_add_rPr()
    rFonts = rPr.find(qn('w:rFonts')) or OxmlElement('w:rFonts')
    if rFonts.getparent() is None:
        rPr.append(rFonts)
    rFonts.set(qn('w:eastAsia'), font_name)
```
Route every run through this helper so Chinese and Latin text stay on one typeface.

## Step 4: Reporting standards and templates

`references/reporting-standards.md` covers what NI 43-101, JORC, and CRIRSCO actually require, how they differ, and where they converge (they're all CRIRSCO-family codes), plus a regional-standards section covering Brazil, Russia's GKZ classification (A/B