# Business Glossary

## Purpose

This glossary is the canonical vocabulary source for semantic-model naming, descriptions, synonyms, abbreviations, and related business documentation.

It is intentionally separate from the DAX measure standard so the same vocabulary can be reused across measures, columns, reports, documentation, Copilot/Q&A, and other semantic-model artefacts.

## Governance

For each term maintain:

- **Canonical Term**
- **Definition**
- **Domain**
- **Approved Abbreviations**
- **Approved Synonyms**
- **Disallowed / Ambiguous Terms**
- **Related Terms**

A synonym must not introduce a materially different concept.

An abbreviation is approved only when it is widely understood by the intended audience and unambiguous within the relevant domain.

## Shared terms to define

The following terms should be progressively populated with enterprise-approved definitions:

### Workforce

- Headcount
- FTE
- Employee
- Worker
- Employment
- Starter
- Leaver
- Turnover
- Voluntary Turnover

### Organisation

- Organisation Node
- Cost Centre
- Manager
- Reporting Line
- Direct Report
- Indirect Report
- Span of Control
- Hierarchy Depth
- Parent Node
- Child Node
- Descendant
- Leaf Node

### Performance

- Performance Population
- Performance Eligible Employee
- Performance Participant
- Performance Outcome
- Performance Rating
- Performance Score
- Completion

### Fixed Reward

- Base Salary
- Fixed Reward
- Total Fixed Reward
- Compa-Ratio
- Range Penetration
- Market Position
- P25
- P50
- P75

### Variable Reward

- Variable Reward
- Variable Reward Eligible Employee
- Participant
- Target
- Award
- Payout
- GPI
- IPM

### Equity

- Equity
- Equity Participant
- Grant
- Award
- Unit
- Tranche
- Vesting Event
- Granted Value
- Vested Value
- Unvested Value
- Fair Value

### International Assignments

- International Assignment
- International Assignee
- Home Country
- Host Country
- Home Entity
- Host Entity
- Assignment Duration

### Shared analytical vocabulary

- Average
- Median
- Change
- Variance
- Rate
- Ratio
- Index
- Percentage Point (`pp`)
- Current
- Prior Year
- Previous Cycle
- Actual
- Proposed
- Projected
- Modelled
- Forecast
- Scenario

## Initial abbreviation policy

Candidate approved business abbreviations, subject to enterprise confirmation:

- FTE
- AUD
- FX
- P25
- P50
- P75
- VR
- STI
- LTI
- GPI
- IPM
- pp

Avoid developer shorthand such as:

- HCElig
- FRAvg
- Calc01
- mFR
- IntCalc

## Synonym guidance

Synonyms support discoverability and natural-language querying.

Example:

### Fixed Reward

Potential synonyms, subject to business validation:

- fixed pay
- salary
- base pay
- fixed remuneration

Do not automatically make `Total Reward` a synonym of `Fixed Reward` because they are materially different concepts.

## Maintenance rule

Domain standards reference this glossary. They should not recreate full vocabulary definitions unless a domain-specific clarification is necessary.
