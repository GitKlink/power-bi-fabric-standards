# Performance Measure Standard

## Scope

Extends `semantic_measure_standard.md` for performance eligibility, participation, completion, outcomes, ratings, and distribution measures.

## Canonical concepts

Distinguish at minimum:

- Performance Eligible Employees
- Performance Participants
- Rated Employees / Completed Employees
- Performance Outcome
- Performance Rating
- Performance Score
- Performance Category

Do not treat these as interchangeable.

## Default assumptions

The domain standard should state the model's default performance population and selected performance/review cycle behaviour.

Do not assume a source-system status or numeric coding is equivalent to the business concept without validation.

## Typical measure families

### Eligibility

- `Eligible Employees`
- `Ineligible Employees`

### Completion

- `Completed Employees`
- `Outstanding Employees`
- `Completion %`

### Outcomes

Examples inside an `Outcomes` folder:

- `Exceeds Expectations Employees`
- `Exceeds Expectations %`
- `Meets Expectations Employees`
- `Meets Expectations %`

Folder context may carry the `Performance` root where unambiguous.

## Numeric rating caution

A numeric source code does not automatically justify `Average` or other arithmetic measures.

If outcome codes are ordinal categories, an average must only be exposed when the business has explicitly defined a meaningful interpretation.

## Population semantics

A description should distinguish:

- eligible population;
- participating population;
- completed/rated population;
- outcome population.

Do not use a generic employee count where these denominators differ.

## Filter behaviour

Measures that intentionally remove outcome filters or lock to a selected review-cycle population must state this in the description.

## Fact row counts

Every performance fact table requires a row-count measure, e.g. `Performance Records`.

## QA themes

Expected validation themes include:

- unmapped performance outcomes;
- duplicate employee-cycle records;
- eligible employees without a valid record;
- multiple final outcomes;
- invalid source rating/outcome combinations;
- missing cycle keys.
