# Semantic Measure Standard

## 1. Purpose

This standard defines how DAX measures are named, described, grouped, formatted, governed, and exposed in Power BI semantic models.

Primary objective: **make the right measure easy to find and hard to misuse**.

The standard is domain-agnostic. Domain files extend it with business-specific concepts, assumptions, examples, and edge cases.

## 2. Scope

Applies to governed semantic models and shared analytical models.

Model classes:

- **Enterprise / certified** — full standard mandatory.
- **Team / shared** — core naming, description, visibility, folder, and formatting rules mandatory.
- **Prototype / local** — relaxed during development; must conform before production use.

## 3. Design principles

1. **Discoverability first.** Naming and folders exist to reduce search cost.
2. **Descriptions carry semantic detail.** Names stay readable and concise.
3. **Explicit measures for governed metrics.** Do not rely on implicit aggregations for business reporting.
4. **Business-facing and backend measures are intentionally separated.**
5. **Reuse measures for shared business logic.** Avoid repeating the same population or calculation logic inline.
6. **Folder structure follows navigation need, not implementation architecture.**
7. **The semantic subject owns the measure.** Dependencies and slicing dimensions do not normally change ownership.
8. **Do not create a new measure merely because an existing measure is sliced by another dimension.**
9. **Stable row/entity attributes belong in columns or model structures; context-dependent calculations and presentation logic belong in measures.**
10. **Backend measures are first-class governed objects. Hidden does not mean cryptic.**

## 4. Measure classes

Supported classes:

1. Business measures
2. Base measures
3. Derived measures
4. KPI measures
5. Helper measures
6. Validation / QA measures
7. Text / dynamic label measures
8. Conditional formatting measures
9. Selector / parameter measures
10. Security / context diagnostic measures
11. Deprecated measures

A measure may be technically foundational without being backend-only. Classification follows intended use, not dependency depth.

## 5. Business-facing vs backend measures

### Business-facing

- Visible to report authors.
- Named for business discoverability.
- Description mandatory.
- Intentional format mandatory.
- Must represent a valid business concept.

### Backend

- Hidden by default.
- Used to support calculations, traversal, context, QA, UI, or formatting.
- Must still have readable names.
- Group under `_Technical` when that improves navigation.
- Do not create excessive subfolders unless measure volume warrants them.

## 6. Naming grammar

### 6.1 Root-first measure families

Use the business concept first so related measures cluster in search.

Preferred:

- `Fixed Reward`
- `Fixed Reward Average`
- `Fixed Reward Median`
- `Fixed Reward Change`
- `Fixed Reward Change %`

Avoid natural-language variants that scatter related measures alphabetically when discoverability suffers.

### 6.2 Context variants

Use ` - ` for deliberate contextual or categorical variants.

Examples:

- `Fixed Reward - Local`
- `Fixed Reward - Previous Cycle`
- `Vested Value - Current`

Standard calculation-family transformations do not require a hyphen.

### 6.3 Prefixes

Technical prefixes may classify purpose where useful:

- `QA -` validation/failure measures
- `CF -` conditional-formatting measures
- `UI -` presentation-only text/navigation measures

Do not prefix ordinary business measures with technical tags such as `M_`, `Calc_`, `KPI_`, or `Helper_`.

### 6.4 Suffixes

Use controlled suffixes for meaningful semantic variants:

- `%`
- `Change`
- `Change %`
- `Variance`
- `Variance %`
- `Average`
- `Median`
- `Minimum`
- `Maximum`
- `YTD`
- `FYTD`
- `Prior Year`
- `Previous Cycle`
- approved units/currencies where a user must distinguish variants

### 6.5 Percentage convention

Use `%` as a terminal suffix with a preceding space.

Preferred:

- `Participation %`
- `Fixed Reward Change %`

Use `pp` for percentage-point change where approved by the business glossary.

- `Participation Change pp`
- `Participation Change %`

### 6.6 Change vs variance

- **Change** = same metric across time/state.
- **Variance** = actual/current metric against a benchmark, target, reference, or expectation.

Default arithmetic direction:

- Change = Current - Prior
- Change % = (Current - Prior) / Prior
- Variance = Actual - Reference
- Variance % = (Actual - Reference) / Reference

Exceptions must be documented.

### 6.7 Entity counts

Prefer established business metric names or plural entities over generic `Count` when unambiguous.

Examples:

- `Headcount`
- `Employees`
- `Equity Grants`
- `International Assignments`

Use `Count` where the plural noun is ambiguous, e.g. `Performance Outcome Count`.

### 6.8 Case and punctuation

Business measures use Title Case.

Allowed punctuation where meaningful:

- spaces
- `%`
- `-`
- `/`
- `&` only where part of an established term or materially needed for brevity

Prefer `and` over `&` in normal business-facing names.

Avoid underscores and implementation syntax in visible business measures.

### 6.9 Character limits

- Target: **30 characters or fewer**
- Soft maximum: **40 characters**
- Hard maximum: **50 characters**

Over 40 characters requires a clear discoverability reason. Over 50 is prohibited unless an approved exception exists.

### 6.10 Context compression

A measure name may omit a business root already supplied by its measure table/display folder when:

1. the shortened name remains unambiguous in that location;
2. readability materially improves;
3. table/folder context is reliably visible to the intended author.

Use sparingly. Do not create generic names such as `Value`, `Total`, or `Average` where multiple concepts coexist.

## 7. Measure tables and display folders

### 7.1 Domain-based measure tables

Prefer logical business domains, for example:

- `Workforce Measures`
- `Organisation Measures`
- `Performance Measures`
- `Fixed Reward Measures`
- `Variable Reward Measures`
- `Equity Measures`
- `International Assignment Measures`

Physical table count may vary by model size. Small models may combine related logical domains under a broader table such as `Reward Measures`.

### 7.2 Display folders

Folders represent business concepts first.

Preferred:

- `Fixed Reward`
- `Variable Reward`
- `Eligibility`
- `Outcomes`
- `Reporting Lines`

Avoid primary organisation by aggregation type such as `Sums`, `Averages`, `Percentages`.

### 7.3 Folder depth

Target no more than two business folder levels.

Technical folders may go deeper only when volume creates a real navigation problem.

### 7.4 `_Technical`

Use `_Technical` when hidden support measures would otherwise pollute business navigation.

Keep it flat by default. Split further only when volume warrants it.

## 8. Description contract

Every business-facing measure must have a description.

Use this section order, including only sections that are materially relevant:

1. **Definition**
2. **Calculation**
3. **Population**
4. **Time**
5. **Context**
6. **Unit / Currency**
7. **Exclusions**
8. **Notes**

Descriptions must explain business semantics, not merely restate the DAX expression.

### 8.1 Calculation style

Prefer formula-style business logic first.

Example:

`Calculation: [Fixed Reward] ÷ [Employees with Fixed Reward].`

Add prose only when needed to clarify edge cases.

### 8.2 Filter/context behaviour

If a measure intentionally removes, overrides, or replaces normal filter context, the description must say so.

Examples:

- `Ignores Performance Outcome filters.`
- `Always evaluates against the selected review-cycle population.`

### 8.3 Calculation grain

Document **intrinsic calculation grain** only where the DAX explicitly evaluates at, or restricts evaluation to, a particular business grain.

Do not document ordinary visual grouping/filter context as measure grain.

Example:

`Calculated at Employee level, then aggregated across the current filter context.`

### 8.4 Time averaging

If the measure itself introduces time averaging or snapshot aggregation, document the averaging basis.

Example:

`Average of month-end Headcount snapshots across the selected months.`

A normal measure evaluated by Month on a visual does not require monthly wording in its description.

### 8.5 Distinct counts

Where entity grain may be ambiguous, state the distinct entity/key counted.

Example:

`Distinct count of Employee ID.`

### 8.6 Weighted measures

State the weighting basis when a measure is weighted.

Example:

`Weighted by employee FTE.`

### 8.7 Blank vs zero

- Use `BLANK()` for not applicable/unavailable unless the business definition requires otherwise.
- Use `0` only when zero is a valid observed value.
- Do not use magic numbers such as `-1`, `999`, or `999999` to represent unknown states.

Document non-obvious blank behaviour where it materially affects interpretation.

### 8.8 Totals and additivity

Classify material measures conceptually as additive, semi-additive, or non-additive.

Document unusual total behaviour, including:

- intentionally suppressed totals;
- custom recalculated totals;
- invalid aggregate levels.

Do not manufacture totals where no valid business meaning exists.

## 9. Formula and dependency design

### 9.1 Reusable base logic

Prefer composing business measures from reusable measures where logic is shared.

Avoid embedding the same population, denominator, or business rule independently across many measures.

### 9.2 Dependencies

Do not manually duplicate a full dependency list in every description.

Use the calculation statement to expose business dependencies where useful. Technical dependency maps should be generated from model metadata where possible.

### 9.3 Numeric source does not imply valid aggregation

Do not expose arithmetic aggregations solely because a source field is numeric.

Ordinal or categorical encodings must have a valid business interpretation before measures such as Average or Sum are created.

## 10. Fact-table row count standard

Every fact table must have a standard row-count measure representing its physical/business grain.

Examples:

- `Reward Records`
- `Performance Records`
- `Equity Grants`
- `Vesting Events`
- `International Assignments`

These are normally hidden QA/backend measures unless the fact grain is itself a legitimate business metric.

Effective-dated facts may also require an effective/current record count where temporal resolution is material.

## 11. Formatting

Every business-facing measure must have an intentional format.

Currency and numeric measures may use approved dynamic format strings. The shared dynamic-format specification is maintained separately and should be referenced rather than reimplemented inconsistently.

Dynamic formatting is appropriate when the underlying business metric is unchanged. It must not be used to disguise fundamentally different metrics.

Units/currencies belong in measure names only where users must distinguish multiple exposed variants.

## 12. Synonyms and glossary integration

Canonical business vocabulary belongs in the shared business glossary.

Measure synonyms should reflect terms users genuinely search for and may inherit/select from glossary synonyms.

Do not use synonyms that collapse materially different concepts.

Approved abbreviations must be:

1. defined in the glossary;
2. unambiguous within the intended domain;
3. commonly understood by intended model users.

## 13. Calculation groups

Calculation groups must follow the same controlled naming vocabulary as physical measures.

Do not create separate physical measures solely to reproduce behaviour already provided by an approved calculation group.

Typical calculation items may include:

- Current
- Prior Year
- YoY Change
- YoY Change %
- FYTD
- Previous Cycle
- Cycle Change
- Cycle Change %

Domain lifecycle periods such as review cycles are not automatically equivalent to calendar or financial-year periods.

## 14. Field parameters and selectors

Generated objects are governed objects and must be renamed consistently.

Selectors may include:

- `Selected Metric`
- `Selected Currency`
- `Selected Review Cycle`
- `Selected Benchmark`

Visible selectors use business names. Hidden technical selectors may remain under `_Technical` without a mandatory `SEL -` prefix.

## 15. Conditional formatting and UI measures

### Conditional formatting

Use `CF -` for measures whose purpose is to return formatting instructions or tokens.

Examples:

- `CF - Reward Variance Colour`
- `CF - Performance Background`

### UI / dynamic text

Use `UI -` for presentation-only measures such as:

- dynamic titles;
- subtitles;
- tree/navigation labels;
- filter summaries used only for presentation.

If a text measure is meaningful business information in its own right, expose it without `UI -`.

Technical prefix identifies purpose, not return type.

## 16. QA measures

Use `QA - <failure condition>`.

Preferred:

- `QA - Missing Currency Rate`
- `QA - Duplicate Reward Record`
- `QA - Orphan Organisation Node`

Avoid vague names such as `QA - Reward Check`.

Default QA output should be the number of failing records/entities where practical:

- `0` = pass
- `>0` = investigate

Domain standards define expected validation themes; implementations define the exact QA set needed.

## 17. Ownership and cross-domain measures

Measure ownership follows the **primary business concept being measured**.

Rules:

1. Slicing dimensions do not change ownership.
2. Denominators do not normally change ownership.
3. Shared dependencies do not automatically create a cross-domain measure.
4. Cross-domain ownership applies only when the metric itself represents a relationship between domains.
5. Create a cross-domain measure table only when a coherent family exists.
6. Physical storage follows semantic ownership unless a shared technical measure genuinely serves multiple domains.

Examples:

- `Turnover %` -> Workforce
- `Fixed Reward per FTE` -> Fixed Reward
- `Equity Participation %` -> Equity
- `Fixed Reward % of Parent` -> Fixed Reward, despite Organisation dependency
- `Performance Reward Alignment Index` -> potentially a cross-domain Performance & Reward family

## 18. Shared technical measures

A shared technical measure table is allowed only where the measure genuinely supports multiple domains.

Examples:

- `Selected Reporting Date`
- `Selected Currency`
- `Current Hierarchy Depth`

Do not create a generic dumping ground.

## 19. Lifecycle and deprecation

Experimental measures must be hidden or isolated until approved.

Deprecated measures should be hidden and moved to `_Technical\Deprecated` where needed during migration.

Description should state:

- `DEPRECATED.`
- replacement measure;
- reason where useful.

Do not silently change the semantic meaning of an existing measure. A breaking semantic change should normally result in a new measure and controlled migration.

## 20. Search-first quality test

Before approving a measure name, ask:

> If an author searches the likely business concept, do the relevant measures appear together and can the correct one be distinguished quickly?

Example search `Fixed Reward` should surface:

- `Fixed Reward`
- `Fixed Reward Average`
- `Fixed Reward Median`
- `Fixed Reward Change`
- `Fixed Reward Change %`

This test takes precedence over grammatical elegance.

## 21. Domain standards

Domain files extend this standard. They may define:

- canonical concepts;
- default populations;
- default currency/time assumptions;
- approved measure families;
- domain-specific edge cases;
- required description details;
- domain-specific QA themes;
- backend patterns.

Domain standards should not duplicate generic rules unless an explicit specialisation or exception is required.
