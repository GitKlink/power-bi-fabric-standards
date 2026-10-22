# Power BI / Fabric Engineering Standards

Canonical policy and governance home for Power BI/Fabric-focused analytics engineering, from source acquisition and analytical modelling through Power Query, semantic models, DAX, report experience and validation.

## Source of truth and ownership

- **This repository:** reusable *engineering policy* — naming, metadata, modelling practice, quality gates, conformance.
- **[Power BI / Fabric Architect](https://github.com/GitKlink/performance-reward-dashboard-architect):** orchestrates workflows, standards consumption and platform/domain composition; does not duplicate normative standards.
- **Domain packs (initially Performance & Reward):** business meaning, definitions, populations, eligibility, KPI contracts, business calculations and reconciliation rules.
- **[DAX/M Query Library](https://github.com/GitKlink/dax-m-query-library):** reusable executable DAX, M, Python and Deneb implementations, patterns and tests.
- **Microsoft-maintained skills:** platform execution and validation where suitable, augmented by policy/domain requirements.

One authority per concern; reference rather than maintain competing copies.

## Current content

- [Semantic Model Standards](semantic-model/README.md) — **11 original Markdown files** migrated unchanged from the File Library `Semantic Model Standards/` collection, including the core measure standard, business glossary, improvement backlog and seven P&R-oriented domain extensions.
- [Migration source/parity record](docs/migration/2026-10-16-semantic-model.md) — independently verifiable content fingerprints of the original files.

The domain extensions contain historical semantic and domain-related content. Separate generic semantic rules from P&R business authority **only after** original migration parity is accepted (see [Architect #6](https://github.com/GitKlink/performance-reward-dashboard-architect/issues/6)).

## Planned standards families

`semantic-model/` is populated first. Future families will be introduced when normative content is ready, not as empty scaffolding:

- `dax/` — DAX expression and engineering policy
- `power-query/` — M/Dataflows engineering policy
- `data-architecture/` — analytics-serving data patterns, dimensional modelling, effective dating and history
- `reporting-ux/` — Power BI report/analytical experience and design standards
- `validation/` — standards conformance and acceptance policy

## Governance

- Treat the **core measure standard** as the normative generic source for governed measures. Read its domain extensions and glossary as defined in [the source README](semantic-model/README.md).
- The **improvement backlog contains proposals, not approved requirements**.
- Keep migration-only changes separate from amendments to substantive standards.
- Standards consumers should identify a reviewed revision and avoid uncontrolled content copies. The Architect now provides a first read-only [DAX Measure Standards Reviewer](https://github.com/GitKlink/performance-reward-dashboard-architect/tree/main/.agents/skills/dax-measure-standards-review), which reads a pinned commit of this standards repository. General installation/bootstrap and native PBIP/TMDL validation remain future work.

See [Architect #5](https://github.com/GitKlink/performance-reward-dashboard-architect/issues/5) for the authority decision and [#21](https://github.com/GitKlink/performance-reward-dashboard-architect/issues/21) for migration tracking.

## Consuming these standards in the Architect

This repository is **public and authoritative for engineering policy**. It is not the installer or the DAX reviewer. Use the [Architect's DAX reviewer setup guide](https://github.com/GitKlink/performance-reward-dashboard-architect/blob/main/.agents/skills/dax-measure-standards-review/README.md) to test measure inventories and the [Architect repository](https://github.com/GitKlink/performance-reward-dashboard-architect) for setup/orchestration work. The reviewer currently requires the immutable standards commit `2d6eb0c2dd627b7607c0ad28a4ea6866e5427aa9`; an updated `main` must not be used as an unreviewed substitute. The private/public visibility change does **not** invalidate that Git commit pin.

**Terminology:** **Power BI / Fabric Architect** is the analytical-engineering project. **Wayfinder** refers solely to Matt Pocock's planning skill used during architecture research, not to this standards repository or the Architect product.
