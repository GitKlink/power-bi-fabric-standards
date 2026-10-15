# Workforce Measure Standard

## Scope

Extends `semantic_measure_standard.md` for workforce population, headcount, FTE, movement, and turnover measures.

## Canonical concepts

Use enterprise-approved glossary definitions for:

- Headcount
- FTE
- Employees
- Starters
- Leavers
- Turnover
- Voluntary Turnover

Established business metric names override generic grammatical rules. `Headcount` is valid even though it is not a plural entity name.

## Typical measure families

### Headcount

- `Headcount`
- `Headcount Average`
- `Headcount Change`
- `Headcount Change %`

### FTE

- `FTE`
- `FTE Average`
- `FTE Change`
- `FTE Change %`

### Movement

- `Starters`
- `Leavers`
- `Internal Moves`

### Turnover

- `Turnover %`
- `Voluntary Turnover %`

## Time semantics

Headcount and FTE are commonly snapshot or semi-additive measures.

If a measure introduces time averaging, its description must state the averaging basis.

Example:

`Headcount Average` may mean average month-end Headcount across selected months. Do not assume daily or monthly averaging without documentation.

## Population and grain

Descriptions must distinguish person, worker, employment, position, and assignment grain where ambiguity is possible.

`Headcount` should state the canonical distinct entity/key counted.

## Turnover

Turnover measures must define:

- numerator population;
- denominator population;
- denominator averaging methodology;
- time window;
- voluntary/involuntary treatment where applicable.

`Turnover %` remains a Workforce measure even when calculated using a Headcount denominator.

## Fact row counts

Every workforce fact table requires a row-count measure matching its fact grain.

Examples:

- `Workforce Records`
- `Movement Records`

## QA themes

Expected validation themes include:

- duplicate employee/worker grain;
- missing employee keys;
- conflicting active records;
- invalid effective dates;
- invalid or missing FTE values;
- inconsistent starter/leaver status.
