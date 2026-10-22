---
template: use-cases
title: Use Case Specifications Template
version: 1.1
last_updated: 2026-10-22
owner: ivy_li@epam.com
used_by_skill: generate-use-cases
---

# {{Feature Name}} — Use Case Specifications

**Feature Analysis:** {{link/path to outputs/features/<feature>/<feature>-feature-analysis.md, or "None"}}

## 1. Use Case Summary

| ID | Name | Primary Actor | Brief Description |
|---|---|---|---|
| UC-01 | {{...}} | {{...}} | {{one-line goal}} |
| UC-02 | {{...}} | {{...}} | {{one-line goal}} |

## 2. Use Case Details

*One block per use case.*

### UC-01: {{Use Case Name}}

| Field | Value |
|---|---|
| Primary Actor | {{...}} |
| Secondary Actor(s) | {{... or "None"}} |
| Trigger | {{what initiates this use case}} |
| Preconditions | {{what must be true before this use case can start}} |
| Postconditions (Success Guarantee) | {{what must be true after successful completion}} |

**Basic Flow**

1. {{Actor action}} → {{System response}}
2. {{Actor action}} → {{System response}}

**Alternate Flow(s)**

- **A1 (at step {{n}}):** {{condition}} → {{what happens instead}}

**Exception Flow(s)**

- **E1 (at step {{n}}):** {{error condition}} → {{system/actor response}}

**Business Rules Referenced:** {{Rule name(s) from the linked Feature Analysis's Business Rules table, or "None"}}

**Related Use Cases:** {{"Includes UC-0X" / "Extends UC-0X" / "None"}}

## 3. Open Questions

- **{{UC-0X}}:** {{unresolved item}}

## 4. Document Control & Revision History

| Field | Value |
|---|---|
| Status | Draft / In Review / Approved |

**Revision History**

| Version | Date | Change Description | Trigger / Reason |
|---|---|---|---|
| 1.0 | {{date}} | Initial draft | {{e.g., "Derived from To-Be process in Feature Analysis"}} |
