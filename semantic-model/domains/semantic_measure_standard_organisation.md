# Organisation Measure Standard

## Scope

Extends `semantic_measure_standard.md` for reporting-line, manager, cost-centre, parent-child, ragged hierarchy, and organisation-tree reporting patterns.

Organisation is a measure-heavy domain. Structural columns/tables and hierarchy-aware measures are complementary.

## Hierarchy types

Treat these as distinct unless the model explicitly proves they are equivalent:

1. **Reporting hierarchy** — Employee -> Manager -> Manager -> ...
2. **Organisation-unit hierarchy** — Cost Centre / Organisation Node -> Parent Node -> ...

A manager may span multiple cost centres, and a cost-centre hierarchy may not mirror reporting lines.

## Parent-child patterns

The domain may use parent-child/path logic to support:

- ancestor/descendant testing;
- reporting-line traversal;
- hierarchy depth;
- ragged hierarchy suppression;
- manager-node identification;
- selected-node context;
- parent-relative calculations;
- dynamic navigation or tree visibility.

Backend measures are often necessary and should be governed, readable, and hidden by default.

## Typical business measure families

### Reporting lines

- `Direct Reports`
- `Indirect Reports`
- `Total Reports`
- `Managers`
- `Span of Control`
- `Span of Control Average`

### Hierarchy

- `Organisation Nodes`
- `Manager Nodes`
- `Leaf Nodes`
- `Hierarchy Depth Maximum`
- `Selected Hierarchy Depth`

### Cost centres

- `Cost Centres`
- `Cost Centres Below Node`
- `Leaf Cost Centres`
- `Child Cost Centres`

## Backend/support patterns

Keep `_Technical` flat unless volume creates a navigation problem.

Examples:

- `Current Node Depth`
- `Parent Node Filter`
- `Descendant Match`
- `Show Manager Node`
- `Show Organisation Node`
- `CF - Node Colour`
- `UI - Organisation Node Label`
- `QA - Orphan Node`

Do not over-classify backend measures into many technical subfolders unless authors genuinely benefit.

## Visual/navigation measures

Measures are appropriate when visibility or behaviour depends on current filter/drill context.

Examples:

- `UI - Show Organisation Node`
- `UI - Show Manager Node`
- `UI - Organisation Node Label`
- `UI - Selected Organisation Path`

These may support:

- suppressing padded ragged levels;
- showing manager nodes only;
- stopping expansion at a selected depth;
- hiding empty branches;
- restricting visible descendants;
- context-aware labels.

## Parent-relative calculations

Measures such as `% of Parent` may depend on Organisation hierarchy logic but remain owned by the metric's semantic domain.

Examples:

- `Headcount % of Parent` -> Workforce
- `Fixed Reward % of Parent` -> Fixed Reward

Organisation owns hierarchy context/traversal infrastructure, not every metric that uses it.

## Stable attributes vs measures

Use columns/model structures for stable row-level hierarchy attributes where practical.

Use measures for:

- traversal-dependent calculations;
- current-context structural logic;
- hierarchy-aware aggregation;
- dynamic visibility/navigation;
- parent/ancestor-relative calculations;
- effective-date-sensitive logic where model design requires measure evaluation.

## Effective dating

Where hierarchy structure changes over time, descriptions must state whether logic uses:

- current-state hierarchy;
- selected reporting date;
- source-system status;
- derived effective-date logic.

## QA themes

Expected validation themes include:

- orphan nodes;
- circular reporting lines;
- missing parents;
- duplicate nodes;
- invalid hierarchy depth;
- employees without a valid manager where one is required;
- conflicting effective-dated hierarchy relationships.
