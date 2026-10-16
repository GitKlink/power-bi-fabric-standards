# Variable Reward Measure Standard

## Scope

Extends `semantic_measure_standard.md` for variable-reward eligibility, participation, target, award, payout, and related lifecycle measures.

## Canonical lifecycle

Keep lifecycle concepts distinct:

- Eligibility
- Target
- Award
- Payout

Do not use these terms interchangeably.

## Typical measure families

Within a `Variable Reward` context, examples include:

- `Eligible Employees`
- `Participants`
- `Participation %`
- `Target %`
- `Target Value`
- `Award %`
- `Award Value`
- `Payout %`
- `Payout Value`

Context compression is allowed when the display folder/table makes the Variable Reward root unambiguous.

Where context is not reliable, use full root-first names:

- `Variable Reward Target %`
- `Variable Reward Target Value`
- `Variable Reward Award %`
- `Variable Reward Award Value`

## Population semantics

Descriptions must distinguish:

- eligible employees;
- participants;
- recipients;
- paid employees where applicable.

Do not substitute generic Headcount unless that is explicitly the denominator definition.

## Lifecycle status qualifiers

Use controlled qualifiers such as:

- Actual
- Proposed
- Projected
- Modelled
- Forecast
- Scenario

Do not invent near-synonyms such as `Future`, `Potential`, or `Expected` where an approved status term already exists.

## GPI / IPM

Approved abbreviations such as GPI and IPM must be defined in the business glossary and used consistently.

Measures involving these factors must clearly state whether they are inputs, calculated outcomes, or applied payout factors.

## Blank vs zero

Not eligible should normally return `BLANK()` rather than `0` unless the business definition explicitly treats non-eligibility as zero.

## Fact row counts

Every Variable Reward fact table requires a row-count measure matching its grain.

## QA themes

Expected validation themes include:

- eligible employee without target;
- participant without award;
- award without eligibility;
- payout without award;
- duplicate employee-cycle record;
- missing/invalid GPI or IPM;
- invalid payout factor;
- inconsistent lifecycle status.
