---
template: user-stories
title: User Story & Acceptance Criteria Template
version: 2.0
last_updated: 2026-09-28
owner: ivy_li@epam.com
used_by_skill: generate-user-stories
---

# {{Use Case Name}} — {{US-0X}}: {{Story Title}}

*Scoped to a single story. Each story confirmed for a use case gets its own file like this one.*

## 1. Story

As a **{{role}}**, I want **{{goal}}**, so that **{{benefit}}**.

**Covers Flow(s):** {{e.g., "Basic Flow" / "Alternate Flow A1" / "Exception Flow E1"}}

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

{{NFR ID(s) from outputs/feature-<feature>/<feature>-feature-analysis.md, or "None"}}

## 4. Open Questions

{{Unresolved items.}}

## 5. Document Control & Revision History

| Field | Value |
|---|---|
| Story ID | {{US-0X}} |
| Use Case | {{UC-0X: Name}} |
| Feature | {{feature name}} |
| Source Use Cases Doc | {{link/path to outputs/feature-<feature>/<feature>-use-cases.md}} |
| Sprint Bucket | {{Future Sprint / Current Sprint / Delivered}} |
| Author | {{author}} |
| Status | Draft / In Review / Approved |
| Verification Status | {{Not Verified / Verified — v{{version}}, {{date}}, reviewed by {{reviewer model}}}} |
| Delivery Status | {{Not Delivered / Delivered — {{date}}}} |

**Revision History**

| Version | Date | Change Description | Trigger / Reason |
|---|---|---|---|
| 1.0 | {{date}} | Initial draft | {{e.g., "Derived from UC-0X"}} |
