---
template: func-test
title: Functional Test Cases Template
version: 2.1
last_updated: 2026-10-22
owner: ivy_li@epam.com
used_by_skill: generate-test-cases
---

# {{UC-0X}} {{US-0X}}: {{Story Title}} — Functional Test Cases

**Source Story:** {{link/path to outputs/features/<feature>/user-stories/<UC-ID>/<UC-ID>-<short-title>.md}}

*Scoped to a single story, matching its source story file — not the whole use case.*

## 1. Classification & Scope

**Classification:** {{`UI-related` / `Functionality-related` / `Functionality+Data-related`}}

**Reasoning:** {{why this classification applies — e.g., "touches stored order data, so leftover-data/migration checks apply"}}

## 2. Assumptions & Clarifications

{{Ambiguities raised during analysis and how each was resolved.}}

## 3. Test Case Summary

| Scenario Group | P0 | P1 | P2 | Total |
|---|---|---|---|---|
| Positive | {{n}} | {{n}} | {{n}} | {{n}} |
| Alternative | {{n}} | {{n}} | {{n}} | {{n}} |
| Negative | {{n}} | {{n}} | {{n}} | {{n}} |
| Boundary | {{n}} | {{n}} | {{n}} | {{n}} |

## 4. Test Cases

*Ordered for execution, not just by priority. One block per test case.*

#### Test ID: {{POS-1}}

**Scenario Group:** {{Positive/Alternative/Negative/Boundary}}
**Priority:** {{P0/P1/P2}}
**Source Scenario:** {{Scenario name from this story's Acceptance Criteria}}

**Given:** {{precondition}}
**When:** {{action}}
**Then:** {{expected result}}

**Assumptions:** {{"None" or "[ASSUMPTION - not stated in AC] ..."}}

## 5. Open Questions

{{Unresolved items.}}

## 6. Document Control & Revision History

| Field | Value |
|---|---|
| Status | Draft / In Review / Approved |

**Revision History**

| Version | Date | Change Description | Trigger / Reason |
|---|---|---|---|
| 1.0 | {{date}} | Initial draft | {{e.g., "Derived from <UC-ID>-<short-title>.md"}} |
