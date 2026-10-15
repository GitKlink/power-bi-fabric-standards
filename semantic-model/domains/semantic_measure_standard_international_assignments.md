# International Assignments Measure Standard

## Scope

Extends `semantic_measure_standard.md` for international assignees, assignments, home/host semantics, assignment lifecycle, duration, and cost measures.

## Canonical entity

Use `International Assignment` as the formal business entity unless enterprise vocabulary defines another canonical term.

Distinguish:

- `International Assignees` — distinct people
- `International Assignments` — assignment records/entities

One person may have multiple historical or concurrent assignments.

## Home vs host semantics

`Home` and `Host` are controlled qualifiers because they change the entity/context being described.

Examples:

- `Home Fixed Reward`
- `Host Fixed Reward`
- `Home Country`
- `Host Country`
- `Home Entity`
- `Host Entity`

## Typical measure families

### Population

- `International Assignees`
- `International Assignments`
- `Active Assignments`

### Duration

- `Assignment Duration`
- `Assignment Elapsed Days`
- `Assignment Remaining Days`

### Cost

- `Assignment Cost`
- `Assignment Cost Average`
- `Assignment Cost per Assignee`

## Status semantics

`Active Assignments` must document whether active status is based on:

- source-system status;
- reporting date between start/end dates;
- another derived lifecycle rule.

If source and derived status can differ, the description must explicitly identify which is used.

## Duration

`Assignment Duration` should have one canonical documented unit unless multiple unit variants are intentionally exposed.

Use explicit names such as `Assignment Elapsed Days` or `Assignment Remaining Days` where the temporal concept differs.

## Currency

Assignment cost may involve home, host, local, and reporting currencies. Currency suffixes are required where users must distinguish exposed variants.

## Fact row counts

Every assignment fact table requires a row-count measure, e.g. `International Assignments` or a backend `Assignment Records` measure depending on the fact grain.

Effective-dated facts may require an effective/current record count for temporal validation.

## QA themes

Expected validation themes include:

- assignment without assignee;
- invalid home/host pairing;
- missing start/end date;
- overlapping assignments;
- invalid active-status derivation;
- missing currency rate;
- missing home/host entity;
- negative or inconsistent duration.
