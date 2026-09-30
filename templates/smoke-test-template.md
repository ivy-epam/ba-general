---
template: smoke-test
title: Smoke Test Suite Template
version: 1.0
last_updated: 2026-09-28
owner: ivy_li@epam.com
used_by_skill: generate-smoke-test
---

# Smoke Test Suite

*A single, cumulative, product-wide suite for build-stability verification — not exhaustive testing. Updated iteratively as features are added or changed.*

## 1. Document Control & Revision History

| Field | Value |
|---|---|
| Status | Draft / In Review / Approved |

**Revision History**

| Version | Date | Feature(s) | Iteration Delta | Trigger / Reason |
|---|---|---|---|---|
| 1.0 | {{date}} | {{feature(s)}} | Added: {{IDs}} | {{e.g., "Initial smoke suite seeded from <feature>"}} |

## 2. Module (Feature) Status

*Doubles as the scope baseline for future runs — compare against this table rather than a separate baseline file.*

| Feature | Project Code | Status | Last Reviewed |
|---|---|---|---|
| {{...}} | {{...}} | {{New / Updated / Unchanged / Deprecated}} | {{date}} |

## 3. Smoke Test Coverage Matrix

| Feature | P0 Count | P1 Count |
|---|---|---|
| {{...}} | {{n}} | {{n}} |

## 4. Smoke Test Cases

*Grouped by feature. P0/P1 only. Happy flow or critical parallel alternatives only — not exhaustive.*

#### {{Feature}}-{{UC-0X}}-ST-001

**Priority:** {{P0/P1}}
**Iteration Action:** {{New / Updated / Carry-Forward / Deprecated}}
**Title:** {{1-line scenario description}}
**Source:** {{use case + func-test Test ID this was pulled from, e.g. "UC-02, POS-1"}}

**Given:** {{precondition}}
**When:** {{action}}
**Then:** {{expected result}}

**Dependencies:** {{external services or test data required, or "None"}}
**Cleanup:** {{rollback/cleanup step if this test writes anything, or "Not applicable — read-only"}}
**Assumptions:** {{"None" or noted assumption}}

<!-- Repeat the test case block above for each additional smoke test case -->

## 5. Out of Scope

*Use cases/flows excluded solely by the production-safety rules (not by low priority) — kept cumulatively, not just this run's exclusions.*

| Feature / Use Case | Reason Excluded |
|---|---|
| {{...}} | {{e.g., "Write visible to a real user (access grant) with no dedicated-QA-account path"}} |

## 6. Recommendations

{{Critical paths not covered that should be added; ambiguities needing clarification before execution.}}

## 7. Open Questions

{{Unresolved items, including use cases with no func-test file yet to pull priority from.}}
