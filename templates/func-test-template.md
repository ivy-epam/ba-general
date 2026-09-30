---
template: func-test
title: Functional Test Cases Template
version: 2.0
last_updated: 2026-09-28
owner: ivy_li@epam.com
used_by_skill: generate-test-cases
---

# {{Use Case Name}} — {{US-0X}} — Functional Test Cases

*Scoped to a single story, matching its source story file — not the whole use case.*

## 1. Document Control & Revision History

| Field | Value |
|---|---|
| Story ID | {{US-0X}} |
| Use Case | {{UC-0X: Name}} |
| Source Story File | {{link/path to the story's current file, e.g. outputs/current-sprint/US-<use-case-name>/<use-case-name>-US-0X.md}} |
| Author | {{author}} |
| Status | Draft / In Review / Approved |

**Revision History**

| Version | Date | Change Description | Trigger / Reason |
|---|---|---|---|
| 1.0 | {{date}} | Initial draft | {{e.g., "Derived from <use-case-name>-US-0X.md"}} |

## 2. Classification & Scope

**Classification:** {{`UI-related` / `Functionality-related` / `Functionality+Data-related`}}

**Reasoning:** {{why this classification applies — e.g., "touches stored order data, so leftover-data/migration checks apply"}}

## 3. Assumptions & Clarifications

{{Ambiguities raised during analysis and how they were resolved, or logged as "[UNRESOLVED - user proceeded without clarification]" if the user proceeded without resolving them.}}

## 4. Test Case Summary

| Scenario Group | P0 | P1 | P2 | Total |
|---|---|---|---|---|
| Positive | {{n}} | {{n}} | {{n}} | {{n}} |
| Alternative | {{n}} | {{n}} | {{n}} | {{n}} |
| Negative | {{n}} | {{n}} | {{n}} | {{n}} |
| Boundary | {{n}} | {{n}} | {{n}} | {{n}} |

## 5. Test Cases

*Ordered for execution, not just by priority — see the source skill's execution-order optimization rules. One block per test case.*

#### Test ID: {{POS-1}}

**Scenario Group:** {{Positive/Alternative/Negative/Boundary}}
**Priority:** {{P0/P1/P2}}
**Source Scenario:** {{Scenario name from this story's Acceptance Criteria}}

**Given:** {{precondition}}
**When:** {{action}}
**Then:** {{expected result}}

**Assumptions:** {{"None" or "[ASSUMPTION - not stated in AC] ..."}}

<!-- Repeat the "Test ID" block above for each additional test case -->

## 6. Coverage Notes

{{Result of the coverage analysis: happy path + alternative flows, all ACs, boundary conditions, invalid input handling, error conditions, data validation, permission/authorization (cross-checked against outputs/rbac.md), state transitions. Note which categories are covered, and which are explicitly not applicable and why.}}

## 7. Open Questions

{{Boundary conditions or other coverage gaps with no source to draw from, and anything else unresolved.}}
