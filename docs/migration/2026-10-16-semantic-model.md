# Semantic Model Standards — source migration parity

Migration review date: **2026-10-16**

**Source:** User File Library folder `/Semantic Model Standards/` and `/Semantic Model Standards/domains/`.

**Target:** `GitKlink/power-bi-fabric-standards`, `semantic-model/`. The **11 source Markdown documents** are copied unchanged. This manifest and the repository-root README are new repository documentation, **not** part of the original source set.

**Verification method:** Original Library document bytes were materialized and hashed; uploaded Git blob IDs were checked against independently calculated Git blob SHA-1 IDs (`SHA1("blob <byte-count>\\0" + original bytes)`). These identifiers prove byte parity for each Markdown file independent of any conceptual rewording. After the branch commit, verify repository paths and blob SHAs again.

**Expected original file checksums** (SHA-256):

```text
8e3434d6aea49ee00db19403bde8fcfea8cca406e23a638bf9c4333ff0616e1b  semantic-model/README.md
95357fb308d1ae181a9ed90e1ed2957a20bcc4156cc4ea50fd30b1af319d54d9  semantic-model/business_glossary.md
e1c0b8de46872bc81535d399722ccdffb3244853f18452a5704e1d58d8ae5210  semantic-model/semantic_measure_standard.md
b41ee8a4bfe5ac26c7bdd160393cd727d98d771d08822e9d51fcb7ff0709609c  semantic-model/semantic_measure_standard_improvement_backlog.md
a6c2e2dddba72c7ee52da113fc75c3fbb6918779f38f81f4e4ce6797a24f6cb4  semantic-model/domains/semantic_measure_standard_workforce.md
b8f4fd441a86f333a8a16a6df766e71688ee187f6ee1d22a57203cff8f08620a  semantic-model/domains/semantic_measure_standard_organisation.md
732d950e2667fe44ee6cc2dbb859c1f384c18a317318382935ac8fd0df57341f  semantic-model/domains/semantic_measure_standard_performance.md
4bea11ab6bacc51fa5f0cd5643c30496a3f10d3e8ced3e8e9a44587ee4c15fb1  semantic-model/domains/semantic_measure_standard_fixed_reward.md
7dd54491afe71cccca2ca7e5676bfd0f23b502d316ac5623939bd5fd2e2a7abc  semantic-model/domains/semantic_measure_standard_variable_reward.md
cabad09e9ae0477c452cf438328a72043b7d16e3df5f3ac92cfa0e7062113d04  semantic-model/domains/semantic_measure_standard_equity.md
c47466da2298dfbb3c558c9795537023c769c3279e34ffe314f9e3d5fd47ed14  semantic-model/domains/semantic_measure_standard_international_assignments.md
```

**Expected original Git blob object IDs** (SHA-1):

```text
238d93921c0f90f7ba9c825c66105ffe9f309449  semantic-model/README.md
29953679aa2752748219575b7983fdff986b7be0  semantic-model/business_glossary.md
d74dc7ddd79b2a4bc4d7d239c309bb9674fa87c3  semantic-model/semantic_measure_standard.md
f7cc6980ce0b84d81af1c3d46ef07bb4c4682825  semantic-model/semantic_measure_standard_improvement_backlog.md
9e2c270cb2133f853555112b01a0212a5a9ca74a  semantic-model/domains/semantic_measure_standard_workforce.md
af58cc029a5a258186c5741610341fb16e984abe  semantic-model/domains/semantic_measure_standard_organisation.md
a96b30a3349ac28510fab4f0cd978238a68de158  semantic-model/domains/semantic_measure_standard_performance.md
8d30029c5193636b35bb008fbe8a2726fc27a2df  semantic-model/domains/semantic_measure_standard_fixed_reward.md
3c84887b468c3f9cc7fa9488f189868a1b6bb69f  semantic-model/domains/semantic_measure_standard_variable_reward.md
c38fdb9d7202d8588892f5035b63525e0195fc11  semantic-model/domains/semantic_measure_standard_equity.md
4942c8254a4a297979f04a7fec510a3e754aa644  semantic-model/domains/semantic_measure_standard_international_assignments.md
```

**Scope and follow-ups**

- This is a **preservation migration**, not an endorsement of every proposed backlog item.
- The inherited folder layout has not been refactored; domain-governance boundaries are the subject of [Wayfinder #6](https://github.com/GitKlink/performance-reward-dashboard-architect/issues/6).
- The AI semantic governance backlog and naming improvements are not implemented by this migration.
- The File Library source remains unchanged. [Wayfinder #21](https://github.com/GitKlink/performance-reward-dashboard-architect/issues/21) tracks migration closure.
