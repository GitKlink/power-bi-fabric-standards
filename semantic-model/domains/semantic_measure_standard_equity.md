# Equity Measure Standard

## Scope

Extends `semantic_measure_standard.md` for equity eligibility, participation, grants, awards, units, tranches, vesting, and valuation measures.

## Grain distinctions

One employee may have multiple:

- grants;
- awards;
- tranches;
- vesting events;
- vesting dates.

Entity counts must therefore distinguish person and transaction/event grain.

Examples:

- `Equity Participants`
- `Equity Grants`
- `Vesting Events`

## Typical measure families

### Participation

- `Eligible Employees`
- `Participants`
- `Participation %`

### Grants

- `Equity Grants`
- `Granted Units`
- `Grant Date Value`

### Vesting

- `Vesting Events`
- `Vested Units`
- `Vested Value`
- `Unvested Units`
- `Unvested Value`

## Units vs value

Always distinguish unit counts from monetary values where both exist.

Avoid ambiguous measures such as `Equity Granted` or `Equity Vested` when users need to distinguish units and value.

## Valuation basis

Monetary equity measures must document valuation basis when value depends on price/date methodology.

Possible bases include:

- grant-date value;
- vest-date value;
- current value;
- face value;
- fair value.

If multiple bases are exposed, include the basis in the measure name, e.g.:

- `Vested Value - Current`
- `Vested Value - Vest Date`

Description should state the price source/date basis where material.

## Blank vs zero

No grant / not applicable should normally remain `BLANK()` rather than being coerced to zero.

## Fact row counts

Every Equity fact table requires a row-count measure matching its grain, for example:

- `Equity Grants`
- `Vesting Events`

These may be business-facing when the fact grain is itself a legitimate business metric.

## QA themes

Expected validation themes include:

- duplicate grant;
- missing participant key;
- invalid tranche sequence;
- vesting event without grant;
- invalid or missing valuation price;
- inconsistent vested/unvested units;
- valuation-date mismatch.
