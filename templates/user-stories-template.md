---
template: user-stories
title: User Story & Acceptance Criteria Template
version: 2.1
last_updated: 2026-10-22
owner: ivy_li@epam.com
used_by_skill: generate-user-stories
---

# {{UC-0X}} {{Use Case Name}} — {{US-0X}}: {{Story Title}}

**Feature:** {{feature name}} · **Use Cases:** {{link/path to outputs/features/<feature>/<feature>-use-cases.md}}

*Scoped to a single story. Each story confirmed for a use case gets its own file like this one.*

## 1. Story

As a **{{role}}**, I want **{{goal}}**, so that **{{benefit}}**.

**Covers Flow(s):** {{e.g., "Basic Flow" / "Alternate Flow A1" / "Exception Flow E1"}}

**Priority:** {{P0 / P1 / P2 / P3 / TBD}}

| Method | Calculation | Score | Mapped Priority | Effort / Job Size | Applied |
|---|---|---|---|---|---|
| {{RICE / MoSCoW / WSJF}} | {{e.g. "4 × 2 × 80%"}} | {{e.g. "6.4"}} | {{P0–P3}} | {{e.g. "3 person-weeks", or "—" for MoSCoW}} | {{✓ or blank}} |
| {{second method, if chosen}} | {{...}} | {{...}} | {{...}} | {{...}} | {{...}} |

## 2. Acceptance Criteria

```gherkin
Scenario: {{happy path scenario name}}
  Given {{precondition}}
  When {{action}}
  Then {{expected result}}

Scenario: {{alternate/exception scenario name}}
  Given {{precondition}}
  When {{action}}
  Then {{expected result}}
```

## 3. Related NFRs

{{NFR ID(s) from outputs/features/<feature>/<feature>-feature-analysis.md, or "None"}}

## 4. Open Questions

{{Unresolved items.}}

## 5. Document Control & Revision History

| Field | Value |
|---|---|
| Status | Draft / In Review / Approved |
| Verification Status | {{Not Verified / Verified — v{{version}}, {{date}}, reviewed by {{reviewer model}}}} |
| Delivery Status | {{Not Delivered / Delivered — {{date}}}} |

**Revision History**

| Version | Date | Change Description | Trigger / Reason |
|---|---|---|---|
| 1.0 | {{date}} | Initial draft | {{e.g., "Derived from UC-0X"}} |
