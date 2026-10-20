---
template: smoke-test
title: Smoke Test Suite Template
version: 1.0
last_updated: 2026-09-28
owner: ivy_li@epam.com
used_by_skill: generate-smoke-test
---

# Smoke Test Suite

*A single, cumulative, product-wide suite for build-stability verification — not exhaustive testing. Organised by module; updated iteratively as features are added or changed.*

## 1. Module Status & Coverage

| Module | Status | P0 Count | P1 Count | Last Reviewed |
|---|---|---|---|---|
| {{...}} | {{New / Updated / Unchanged / Deprecated}} | {{n}} | {{n}} | {{date}} |

## 2. Use Case Priorities & Smoke Test Cases

*Grouped by module: a priority table of all its use cases, then details and test cases for the `P0`/`P1` use cases.*

### {{Module}}

**Use Case Priorities**

| UC ID | Use Case | Compliance | Frequency | User Volume | Business Value | Score | Priority | Priority Basis | Rationale |
|---|---|---|---|---|---|---|---|---|---|
| UC-01 | {{...}} | {{0/1}} | {{0/1}} | {{0/1}} | {{0/1/2}} | {{S, or "Gate"}} | {{P0/P1/P2}} | {{Matrix / func-test}} | {{one line per dimension score}} |

#### {{UC-0X}} — {{Use Case Name}} ({{P0/P1}})

**Description:** {{what the actor accomplishes}}
**Primary Actor:** {{role}}
**Primary Flow:** {{Step → Step → Step}}

##### {{Module}}-{{UC-0X}}-ST-001

**Priority:** {{P0/P1}}
**Status:** {{New / Updated / Unchanged / Deprecated}}
**Title:** {{1-line scenario description}}
**Source:** {{module use case, e.g. "{{Module}} / UC-02"; plus feature use case and func-test Test ID where applicable}}

**Given:** {{precondition}}
**When:** {{action}}
**Then:** {{expected result}}

**Dependencies:** {{external services or test data required, or "None"}}
**Cleanup:** {{rollback/cleanup step if this test writes anything, or "Not applicable — read-only"}}
**Assumptions:** {{"None" or noted assumption}}

## 3. Out of Scope

*Use cases or flows excluded by the production-safety rules.*

| Module / Use Case | Reason Excluded |
|---|---|
| {{...}} | {{e.g., "Write visible to a real user (access grant) with no dedicated-QA-account path"}} |

## 4. Recommendations

{{Critical paths not covered that should be added; ambiguities needing clarification before execution.}}

## 5. Open Questions

{{Unresolved items.}}

## 6. Document Control & Revision History

| Field | Value |
|---|---|
| Status | Draft / In Review / Approved |

**Revision History**

| Version | Date | Module(s) | Trigger Feature(s) | Iteration Delta | Trigger / Reason |
|---|---|---|---|---|---|
| 1.0 | {{date}} | {{module(s)}} | {{feature(s), or "None"}} | Added: {{IDs}} | {{e.g., "Initial smoke suite seeded from scope analysis"}} |
