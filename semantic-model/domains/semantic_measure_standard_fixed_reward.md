# Fixed Reward Measure Standard

## Scope

Extends `semantic_measure_standard.md` for Fixed Reward, salary positioning, market benchmarks, ranges, annualisation, and related measures.

## Canonical concepts

Treat these as distinct unless the business glossary explicitly defines otherwise:

- Base Salary
- Fixed Reward
- Superannuation
- Fixed Reward including Superannuation
- Total Cash
- Total Reward
- Compa-Ratio
- Range Penetration
- Market Position

## Default assumptions

Current default reporting currency: **AUD**, subject to model validation.

A measure named `Fixed Reward` may imply AUD only if the semantic model actually implements AUD as its documented default reporting currency.

Default value basis such as annualised Fixed Reward must be explicitly confirmed in the domain/model documentation.

## Typical measure families

- `Fixed Reward`
- `Fixed Reward Average`
- `Fixed Reward Median`
- `Fixed Reward Change`
- `Fixed Reward Change %`
- `Compa-Ratio`
- `Compa-Ratio Average`
- `Compa-Ratio Median`
- `Range Penetration %`

## Currency variants

Only expose currency suffixes where users must choose between variants.

Examples:

- `Fixed Reward`
- `Fixed Reward - Local`
- `Fixed Reward - AUD`

If AUD is the validated model default, avoid adding `AUD` to every ordinary measure name.

## Average semantics

`Fixed Reward Average` means average Fixed Reward in the current filter context unless the DAX itself imposes a special calculation grain.

Do not encode visual grouping such as Business Unit, Month, or Job Family in the measure name.

If the DAX calculates at Employee level before aggregation, state that in the description.

## Market percentiles

Do not confuse statistical distribution percentiles with market benchmark percentiles.

Use `Fixed Reward Median` for the employee distribution median.

Use explicitly market-oriented naming for benchmark percentiles, for example:

- `Market P25`
- `Market P50`
- `Market P75`

within an unambiguous Market Position folder, or longer forms where needed.

## Compa-Ratio and range penetration

Treat `Compa-Ratio` and `Range Penetration %` as distinct business concepts.

Descriptions must state the reference point/range basis and any invalid-grain behaviour where material.

## Fact row counts

Every Fixed Reward fact table requires a row-count measure, e.g. `Reward Records`.

Effective-dated reward facts may also require:

- `Effective Reward Records`
- `Employees with Effective Reward`

where useful for QA and temporal validation.

## QA themes

Expected validation themes include:

- missing currency rate;
- duplicate effective reward record;
- missing Fixed Reward;
- invalid salary range;
- missing benchmark;
- invalid range minimum/midpoint/maximum;
- overlapping effective dates;
- reporting-currency conversion failures.
