# Semantic Measure Standard — Improvement Backlog

## Purpose

This file records potential improvements identified during the post-design research sanity check of the Semantic Measure Standard and its Performance & Reward domain extensions.

It is **not an approved change list**.

The current standards remain authoritative until an item below is explicitly reviewed, decided, and incorporated into the relevant standard file.

Use this file as a handover/backlog for future work so another AI or maintainer can understand:

- what issue was identified;
- why it may matter;
- how it relates to the current design;
- what should be researched or decided next;
- which standard file would likely be affected.

## Current architecture

The standards currently use this structure:

- `semantic_measure_standard.md` — domain-agnostic measure naming, description, discoverability, grouping, formatting, governance, QA, and lifecycle rules.
- `business_glossary.md` — shared business vocabulary, synonyms, abbreviations, ambiguous/disallowed terms, and related terms.
- `domains/semantic_measure_standard_<domain>.md` — domain-specific extensions such as Workforce, Organisation, Performance, Fixed Reward, Variable Reward, Equity, and International Assignments.

Core design intent:

> Make the right measure easy to find and hard to misuse.

The current standard prioritises field-pane discoverability, concise names, strong descriptions, reusable measure families, hidden governed backend measures, and domain-specific semantic rules.

---

# Improvement candidates

## IMP-001 — AI-facing naming vs human field-pane discoverability

### Status

**Open — highest-priority design question.**

### Issue

The current standard deliberately optimises measure names for human discovery in the Power BI field pane. This includes:

- root-first measure families such as `Fixed Reward Average`;
- controlled context compression where table/folder context can carry part of the meaning, e.g. `Target %` inside a clearly named `Variable Reward` context.

Current Microsoft guidance increasingly treats semantic-model metadata as an input to Copilot/AI reasoning. AI systems rely heavily on object names, descriptions, relationships, and semantic metadata when selecting fields and measures.

This creates a potential tension:

- **Humans** may benefit from shorter names because the measure table and display folder provide visible context.
- **AI** may benefit from independently explicit names because it may reason over metadata without the same navigation cues a human sees.

### Example

Human-navigation-friendly:

```text
Reward Measures
└── Variable Reward
    ├── Target %
    ├── Award %
    └── Payout %
```

More independently explicit:

```text
Variable Reward Target %
Variable Reward Award %
Variable Reward Payout %
```

### Current standard position

- Root-first naming is intentional and should not be assumed to be a problem.
- Context compression is allowed only when folder/table context makes the shorter name unambiguous.
- Descriptions carry semantic detail.

### What needs deciding

Determine whether the standard should add a second discoverability test for AI-facing semantic models.

Possible rule to evaluate:

> A context-compressed measure may be acceptable for human authors only when the measure remains sufficiently identifiable to AI through its name, description, table/folder context, and AI schema exposure.

Alternative:

> Measures exposed to AI must remain independently semantically identifiable even if human-facing context compression would otherwise be allowed.

### Research / validation needed

- Test Copilot behaviour against models containing compressed vs fully explicit measure names.
- Determine how strongly AI Data Schemas, descriptions, and table names compensate for compressed measure names.
- Test realistic ambiguous P&R examples such as `Target %`, `Participation %`, `Value`, and `Eligible Employees` across multiple domains.

### Likely files affected

- `semantic_measure_standard.md`
- possibly `business_glossary.md`
- possibly a future AI/semantic-model standard rather than the measure standard itself.

---

## IMP-002 — AI Data Schema governance

### Status

**Open — TOP PRIORITY build item; likely separate modelling/governance standard.**

This item is now promoted from a research candidate to the **next build priority**. The next AI/maintainer should first design the AI semantic governance layer before returning to lower-priority backlog items. No existing standard has yet been changed to implement it.

### Issue

Power BI / Fabric now supports AI-focused semantic metadata patterns where a controlled set of tables, columns, measures, and relationships can be exposed to AI experiences.

The current standards already distinguish:

- business-facing measures;
- backend/hidden measures;
- shared technical measures.

However, **business-facing does not necessarily mean AI-facing**.

A model may contain measures useful to report builders that should not be included in the preferred AI reasoning surface.

### Potential architecture

```text
All semantic-model objects
        ↓
Business-facing semantic layer
        ↓
AI Data Schema / AI-approved surface
        ↓
Copilot / AI consumers
```

### What needs deciding

- Whether AI exposure is a separate governance property from visibility.
- Whether domains should define preferred AI-facing measures.
- Whether backend dependencies required by AI-generated DAX must also be included in AI schemas.
- Whether an AI schema should be managed centrally or per use case/persona.

### Recommendation direction

Do **not** automatically add AI-specific rules into every measure description.

Treat AI exposure as a semantic-model governance layer unless testing shows measure-level metadata is required.

### Likely files affected

Potentially a new file such as:

```text
semantic_ai_schema_standard.md
```

rather than changing the domain measure files directly.

---

## IMP-003 — Perspectives as a discoverability layer

### Status

**Open — architecture enhancement, not naming correction.**

### Issue

Display folders and domain measure tables are currently the main navigation mechanisms.

For very large semantic models, Power BI perspectives can expose a reduced subset of model objects for a particular audience or use case.

Potential discoverability stack:

```text
Domain measure tables
        ↓
Display folders
        ↓
Perspectives
```

### Why it matters

The current naming standard intentionally avoids overlong names and excessive folder nesting. Perspectives could reduce the pressure to encode extra context into names or create additional physical measure tables.

### What needs deciding

- When model size/complexity justifies perspectives.
- Whether perspectives should align to business domains, personas, report families, or analytical use cases.
- Whether perspectives are considered part of semantic governance or report authoring guidance.

### Likely files affected

Probably a future broader semantic-model architecture standard rather than `semantic_measure_standard.md`.

---

## IMP-004 — Report-level measure governance

### Status

**Open — important semantic-drift control.**

### Issue

Power BI permits report authors to create report-level/local measures against an existing semantic model.

The current standard governs measures in managed/shared semantic models but does not explicitly define when a report-level measure is acceptable.

Without a rule, report authors could accidentally recreate or redefine governed enterprise metrics.

### Example risk

Governed semantic model:

```text
Turnover %
```

Report author independently creates:

```text
Turnover % = Leavers / Headcount
```

with a different denominator/time methodology.

Both now appear semantically equivalent while producing different results.

### Candidate rule

> Reusable or business-defining calculations belong in the governed semantic model. Report-level measures are reserved for genuinely report-specific presentation or analysis that does not redefine a governed business metric.

Possible report-level uses:

- report-specific visual calculations;
- temporary exploratory analysis;
- presentation-only dynamic labels;
- calculations that have no reusable business meaning outside the report.

### What needs deciding

- Whether report-level measures must follow the same naming/description standard.
- Whether production reports may contain locally defined business metrics at all.
- Promotion process from report-level measure to governed semantic-model measure.

### Likely files affected

- `semantic_measure_standard.md`
- potentially a future report-authoring standard.

---

## IMP-005 — Storage-mode caveats for hierarchy / Organisation patterns

### Status

**Open — implementation guidance needed.**

### Issue

The Organisation domain correctly treats parent-child, cost-centre, reporting-line, ragged hierarchy, ancestor/descendant, and dynamic tree behaviour as legitimate measure-heavy patterns.

However, specific DAX implementation techniques are affected by storage mode.

Examples include:

- Import;
- DirectQuery;
- Direct Lake;
- composite models.

Parent-child functions such as `PATH`, `PATHITEM`, `PATHLENGTH`, and `PATHCONTAINS` have restrictions in some DirectQuery calculated-column/RLS scenarios. Direct Lake also has restrictions affecting calculated-column strategies.

### Important distinction

The domain standard currently describes **semantic patterns**. It should not accidentally imply one implementation pattern works for every storage mode.

### Candidate improvement

Add a small implementation caveat to the Organisation domain:

> Hierarchy semantics are storage-mode agnostic; implementation patterns are not. Validate parent-child/path, calculated-column, bridge-table, and security patterns against the model's storage mode before implementation.

Potentially document implementation variants separately:

```text
Parent-child semantic pattern
├── Import implementation
├── DirectQuery implementation
└── Direct Lake implementation
```

### Likely files affected

- `domains/semantic_measure_standard_organisation.md`
- possibly a future semantic modelling / hierarchy implementation standard.

---

## IMP-006 — Measure Data Category metadata

### Status

**Open — minor metadata completeness gap.**

### Issue

The current standard explicitly governs:

- name;
- description;
- display folder;
- visibility;
- format;
- synonyms;
- lifecycle.

Power BI measures can also use metadata such as **Data Category** where relevant, for example URL-oriented measures.

### What needs deciding

Whether the generic standard should define an extended metadata contract that includes optional properties such as:

```text
Data Category
```

when materially relevant.

### Recommendation direction

Do not make Data Category mandatory. Add it only as an optional governed metadata property where applicable.

### Likely files affected

- `semantic_measure_standard.md`

---

## IMP-007 — Machine-testable governance using INFO.VIEW / model metadata

### Status

**Open — high-value future automation.**

### Issue

Modern DAX INFO/INFO.VIEW metadata functions expose semantic-model metadata including properties such as:

- measure name;
- description;
- expression;
- format string;
- hidden status;
- display folder;
- state;
- home table and related model metadata.

The current standard contains many rules that could be automatically tested rather than manually reviewed.

### Candidate automated checks

```text
Business-facing measure has description
Business-facing measure has intentional format
Measure name <= approved length
No prohibited prefixes on business measures
QA measures begin with "QA -"
CF measures begin with "CF -"
UI measures begin with "UI -" where applicable
Hidden/backend measure naming remains readable
Display folder depth within target
Deprecated measures are hidden
No implicit business metrics
Fact tables have row-count measures
```

More advanced checks could inspect:

- dependency graphs;
- duplicate/similar measure names;
- domain ownership;
- missing descriptions;
- context-compressed names that become ambiguous across the whole model.

### What needs deciding

- Preferred implementation technology: DAX INFO.VIEW queries, TMDL parsing, Tabular Editor Best Practice Analyzer, TOM/XMLA tooling, Fabric APIs, or combination.
- Which rules should be hard failures vs warnings.
- How domain-specific standards plug into linting.

### Likely files affected

Potential new files:

```text
semantic_measure_validation_standard.md
semantic_measure_lint_rules.md
```

The existing standards should remain human-readable source-of-truth documents, with automated checks derived from them.

---

## IMP-008 — Context-compression validation test

### Status

**Open — closely related to IMP-001 but testable independently.**

### Issue

The standard permits short names when measure-table and display-folder context carries the omitted business root.

This improves side-panel readability but may produce duplicate or ambiguous names across domains:

```text
Performance Measures > Eligibility > Eligible Employees
Variable Reward Measures > Eligibility > Eligible Employees
Equity Measures > Eligibility > Eligible Employees
```

Global uniqueness is currently desirable but not mandatory.

### Improvement to evaluate

Create a formal ambiguity test:

> A context-compressed name is acceptable only if a user searching the model can distinguish the intended measure quickly using the visible table/folder/description context.

Potential stronger version for AI-facing models:

> A context-compressed measure must remain uniquely interpretable from model metadata available to the consuming AI experience.

### What needs testing

Use real models with repeated concepts such as:

- `Eligible Employees`;
- `Participants`;
- `Participation %`;
- `Target %`;
- `Value`;
- `Average`.

### Likely files affected

- `semantic_measure_standard.md`

---

## IMP-009 — Synonyms should be positioned for semantic/AI reuse, not legacy Q&A

### Status

**Open — wording/governance refinement.**

### Issue

The current `business_glossary.md` correctly separates business vocabulary from measure implementation.

Power BI's older natural-language Q&A experience is being superseded by Copilot/AI experiences. Therefore the glossary should not be framed primarily as a Q&A configuration artefact.

### Recommended conceptual framing

> The glossary is the canonical enterprise semantic vocabulary used by humans, semantic models, documentation, search, Copilot/AI, and other analytical tooling.

### Current architecture assessment

No structural change is required. The separate glossary is the correct architecture.

### What needs deciding

- Whether synonyms should be stored only in the glossary or also mapped into model metadata automatically.
- How approved synonyms propagate into AI schemas or semantic-model metadata.
- Whether ambiguous synonyms should be domain-scoped.

### Likely files affected

- `business_glossary.md`

---

## IMP-010 — Formal semantic metadata contract

### Status

**Open — medium priority.**

### Issue

The current standard governs metadata throughout multiple sections, but does not present one single consolidated measure-object contract.

A future standard might formally describe a governed measure as:

```text
Measure
├── Name
├── Domain / semantic owner
├── Measure class
├── Visibility
├── Display folder
├── Description
├── Format / dynamic format behaviour
├── Synonyms
├── Data Category (where relevant)
├── Lifecycle status
└── AI exposure / schema status (if adopted)
```

Technical/generated metadata could include:

```text
DAX expression
Dependencies
Referenced objects
Model state
```

### Why it may help

- clearer onboarding;
- easier machine validation;
- clearer separation of manually governed vs generated metadata;
- easier integration with TMDL/Tabular Editor tooling.

### Risk

Do not over-formalise the standard if the contract merely duplicates content already easy to navigate.

Navigation remains the #1 design objective.

### Likely files affected

- `semantic_measure_standard.md`

---

## IMP-011 — Explicit promotion path from prototype to governed measure

### Status

**Open — lifecycle enhancement.**

### Issue

The current standard distinguishes:

- enterprise/certified;
- team/shared;
- prototype/local models;
- experimental measures;
- deprecated measures.

What is not yet defined is the promotion process from exploratory measure to approved business measure.

### Questions to resolve

Before a measure becomes governed/business-facing, should it require:

- canonical name review;
- description completeness;
- population/grain validation;
- format assignment;
- domain owner assignment;
- QA/reconciliation evidence;
- glossary check;
- duplicate/redundancy check;
- AI exposure decision;
- dependency validation?

### Why it matters

This turns the naming standard into an operational governance workflow rather than a static style guide.

### Likely files affected

Probably a new governance/workflow file rather than bloating `semantic_measure_standard.md`.

---

## IMP-012 — Standardise how domain defaults are inherited into descriptions

### Status

**Open — minor consistency issue.**

### Issue

Domain standards may define defaults such as:

```text
Fixed Reward reporting currency = AUD
Fixed Reward basis = annualised
Performance basis = selected cycle/final outcome
```

The current measure standard also says descriptions should remain independently useful when misunderstanding is material.

This creates a repetition trade-off.

### Question to resolve

When may a measure rely on a domain default without repeating it in every description?

Potential rule:

> Repeat a domain default in a measure description when omission could materially change interpretation; otherwise allow inheritance from the domain standard.

Examples:

- `Fixed Reward` may explicitly state `Currency: AUD` because currency is material.
- A low-risk helper measure may rely on the domain default without repeating it.

### Likely files affected

- `semantic_measure_standard.md`
- domain standards as needed.

---

# Research conclusions that do NOT currently require changes

The following current decisions were sanity-checked and remain strong:

## Keep root-first measure families

Examples:

```text
Fixed Reward
Fixed Reward Average
Fixed Reward Median
Fixed Reward Change
Fixed Reward Change %
```

This is an intentional discoverability convention. It is not a Microsoft-mandated grammar, but it does not conflict with Power BI and provides strong field-pane clustering.

## Keep descriptions as the semantic contract

Descriptions should continue to explain:

- definition;
- calculation;
- population;
- time semantics;
- unusual context behaviour;
- units/currency;
- exclusions;
- material edge cases.

They should not merely repeat DAX.

## Keep business-facing vs backend distinction

Hidden/backend measures are legitimate governed semantic objects, especially in hierarchy-heavy Organisation models.

Do not make hidden measures cryptic.

## Keep navigation-first display-folder philosophy

Folders reduce search cost. They should not reproduce implementation architecture for its own sake.

## Keep domain-specific extension architecture

The split between:

```text
semantic_measure_standard.md
business_glossary.md
domains/semantic_measure_standard_<domain>.md
```

is a strong architecture and should not be collapsed back into one large standard.

## Keep fact-table row-count convention

A mandatory fact row-count measure is an internal governance/QA convention rather than a Microsoft requirement, but it remains useful for validation, grain checking, reconciliation, and effective-dated models.

## Keep semantic ownership rule

The primary business concept owns the measure. Denominators, dependencies, and slicing dimensions do not normally change ownership.

## Keep calculation-grain vs report-context distinction

A measure description documents intrinsic calculation grain only when the calculation itself imposes one. Ordinary visual grouping/filter context does not belong in the measure name or description.

---

# Suggested future review order

If this backlog is resumed, work in this order:

1. **TOP PRIORITY — build the AI semantic governance layer**
   - Design `semantic_ai_standard.md` as a separate standard layered over the governed semantic model.
   - Define AI Data Schema governance, AI eligibility vs human visibility, AI instructions, verified answers, preferred metrics, glossary integration, and an AI regression/evaluation test set.
   - Resolve IMP-001 and IMP-002 together inside this work rather than treating them as isolated naming tweaks.
   - Preserve the current measure standard as the foundation; do not merge AI-specific governance into measure naming unless testing proves a rule belongs there.
2. **IMP-008 — context-compression ambiguity testing**
3. **IMP-004 — report-level measure governance**
4. **IMP-007 — automated linting / machine validation**
5. **IMP-005 — Organisation storage-mode implementation caveats**
6. **IMP-003 — perspectives**
7. Remaining metadata/governance refinements

Do not implement several items at once without deciding whether they belong in:

- the core measure standard;
- a domain extension;
- the business glossary;
- or a separate semantic-model / AI / validation standard.

The current architecture intentionally keeps these concerns separated.

---

# Handover instruction for future AI

When resuming this backlog:

1. Read `semantic_measure_standard.md` first.
2. Read the domain file relevant to the issue being considered.
3. Read `business_glossary.md` if terminology/synonyms are involved.
4. Treat this backlog as **research candidates, not approved rules**.
5. Verify current Power BI / Fabric behaviour using up-to-date primary Microsoft documentation before proposing a change.
6. Preserve the core objective: **make the right measure easy to find and hard to misuse**.
7. Do not add complexity unless it measurably improves navigation, semantic correctness, maintainability, governance, or AI reliability.
8. Discuss and lock the design decision before modifying any canonical standard file.
