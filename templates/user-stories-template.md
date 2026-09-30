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

## 1. Document Control & Revision History

| Field | Value |
|---|---|
| Story ID | {{US-0X}} |
| Use Case | {{UC-0X: Name}} |
| Feature | {{feature name}} |
| Source Use Cases Doc | {{link/path to outputs/feature-<feature>/<feature>-use-cases.md}} |
| Sprint Bucket | {{Future Sprint / Current Sprint / Delivered — must match wherever this file physically lives; update manually when the file is moved}} |
| Author | {{author}} |
| Status | Draft / In Review / Approved |
| Verification Status | {{"Not Verified" by default, or "Verified — v{{version}}, {{date}}, reviewed by {{reviewer model}}" once confirmed via the verify-user-stories skill. Editing this story's content resets it to "Not Verified".}} |
| Delivery Status | {{"Not Delivered" by default, or "Delivered — {{date}}" once marked via the generate-knowledge-page skill.}} |

**Revision History**

| Version | Date | Change Description | Trigger / Reason |
|---|---|---|---|
| 1.0 | {{date}} | Initial draft | {{e.g., "Derived from UC-0X"}} |

## 2. Story

As a **{{role}}**, I want **{{goal}}**, so that **{{benefit}}**.

**Covers Flow(s):** {{e.g., "Basic Flow" / "Alternate Flow A1" / "Exception Flow E1"}}

## 3. Acceptance Criteria

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

## 4. Related NFRs

{{NFR ID(s) from outputs/feature-<feature>/<feature>-feature-analysis.md, or "None"}}

## 5. Open Questions

{{Unresolved items for this story, including any AC gaps not covered by this use case's flows, and any NFR needs raised here but not yet present in the feature analysis document's NFR section.}}
