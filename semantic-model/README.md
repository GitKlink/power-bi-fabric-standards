# Semantic Model Standards

## Purpose

This folder contains the canonical standards for designing, naming, describing, organizing, governing, and evolving measures and related semantic-model concepts.

The standards are designed to make the right measure easy to find and hard to misuse, while keeping the architecture extensible for future semantic-model, AI, validation, and domain standards.

## File Architecture

```text
Semantic Model Standards/
├── README.md
├── semantic_measure_standard.md
├── business_glossary.md
├── semantic_measure_standard_improvement_backlog.md
└── domains/
    ├── semantic_measure_standard_workforce.md
    ├── semantic_measure_standard_organisation.md
    ├── semantic_measure_standard_performance.md
    ├── semantic_measure_standard_fixed_reward.md
    ├── semantic_measure_standard_variable_reward.md
    ├── semantic_measure_standard_equity.md
    └── semantic_measure_standard_international_assignments.md
```

Future standards may add sibling families such as `ai/`, `validation/`, `modeling/`, or `dimensions/`.

## Authority and Inheritance

### 1. Core standard

`semantic_measure_standard.md` is the authoritative domain-agnostic measure standard.

It defines generic rules for naming, measure families, descriptions, visibility, display folders, formatting, QA, technical/backend measures, lifecycle, calculation groups, selectors, ownership, cross-domain measures, and discoverability.

A domain file must not contradict the core standard unless it explicitly declares an approved domain-specific exception.

### 2. Business glossary

`business_glossary.md` is the canonical shared vocabulary source.

It governs canonical business terms, approved abbreviations, approved synonyms, ambiguous/disallowed terms, and related concepts.

Domain standards reference the glossary rather than duplicating enterprise terminology.

### 3. Domain extensions

`domains/semantic_measure_standard_<domain>.md` files extend the core standard with domain-specific rules.

A domain extension may define canonical concepts, domain defaults, measure families, grain distinctions, time/population semantics, hierarchy/reporting patterns, QA themes, backend/support patterns, and specialized description requirements.

Domain files should stay focused and avoid repeating generic rules already defined in the core standard.

### 4. Improvement backlog

`semantic_measure_standard_improvement_backlog.md` is not authoritative.

It records research findings, open design questions, candidate enhancements, and future build priorities.

Backlog items must not be treated as approved rules until they are explicitly reviewed, decided, and incorporated into a canonical standard.

## Recommended Read Order

```text
1. README.md
2. semantic_measure_standard.md
3. business_glossary.md
4. relevant domains/semantic_measure_standard_<domain>.md
5. semantic_measure_standard_improvement_backlog.md
```

Read the backlog last because it contains proposed future changes rather than current rules.

## How the Files Interact

The core standard defines the general rule.

The glossary defines the approved business language.

The domain extension specializes the rule for a particular business area.

The backlog records possible future improvements.

Example:

```text
semantic_measure_standard.md
    ↓
Defines root-first naming, descriptions, visibility, folders, QA, lifecycle

business_glossary.md
    ↓
Defines what "Fixed Reward", "P50", "Compa-Ratio", etc. mean

domains/semantic_measure_standard_fixed_reward.md
    ↓
Defines Fixed Reward-specific families, currency assumptions,
market benchmark distinctions, and QA themes
```

The effective rule set for a Fixed Reward measure is:

```text
Core measure standard
+ shared business glossary
+ Fixed Reward domain extension
```

## Conflict Resolution

Use this order when standards appear to conflict:

```text
1. Explicit approved exception in the relevant domain standard
2. semantic_measure_standard.md
3. business_glossary.md for terminology
4. Current model-specific documentation
5. improvement backlog only as research context
```

The improvement backlog must never override a canonical standard.

If a domain file appears to contradict the core without declaring an exception, treat it as a standards defect that requires review.

## Adding a New Domain Measure Standard

Create:

```text
domains/semantic_measure_standard_<domain>.md
```

A new domain file should generally cover:

```text
1. Scope
2. Canonical concepts
3. Default assumptions
4. Typical measure families
5. Domain-specific semantic rules
6. Population / grain / time distinctions
7. Backend/support patterns where relevant
8. Description requirements where specialized
9. QA themes
10. Examples / edge cases
```

Do not copy large sections from `semantic_measure_standard.md`. Only add rules that genuinely specialize the domain.

## Navigation Principle

The primary design objective is:

> Make the right measure easy to find and hard to misuse.

When choosing between architectural purity and easier navigation, prefer the design that reduces search cost and ambiguity.

Do not create folder hierarchies, prefixes, or technical classifications unless they materially improve navigation, governance, correctness, or maintainability.

## Human and AI Consumers

The current measure standards primarily govern the semantic model itself.

Future work will add a dedicated AI semantic-governance layer covering:

- AI Data Schemas
- AI eligibility vs human visibility
- AI instructions
- preferred metrics
- verified answers
- glossary-driven AI terminology
- AI regression/evaluation test sets

Until those standards are approved, do not infer AI-specific rules from the improvement backlog.

## Handover Guidance for AI / Maintainers

Before changing any canonical standard:

1. Read this README.
2. Read `semantic_measure_standard.md`.
3. Read the relevant domain file.
4. Read `business_glossary.md` if terminology is involved.
5. Read the improvement backlog for known open questions.
6. Verify current Power BI / Fabric behavior using up-to-date primary Microsoft documentation when the change depends on platform behavior.
7. Treat backlog items as proposals, not rules.
8. Discuss and lock the design decision before editing a canonical standard.
9. Preserve navigation and semantic clarity as the primary objective.
10. Avoid adding complexity unless it produces a clear benefit.

## Current Build Priorities

The improvement backlog is the detailed source for future work.

The current highest-priority build area is the AI semantic-governance layer, including AI Data Schema design and AI-facing semantic guidance.

Do not implement that work implicitly inside the existing measure standards until the architecture is deliberately designed and approved.
