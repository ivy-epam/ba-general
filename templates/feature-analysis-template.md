---
template: feature-analysis
title: As-Is / To-Be Process & Gap Analysis Template
version: 1.1
last_updated: 2026-10-22
owner: ivy_li@epam.com
used_by_skill: generate-feature-analysis
---

# {{Feature Name}} — As-Is / To-Be Process & Gap Analysis

**Project Code:** {{project-code}}

## 1. Process Overview & Scope

{{Which business process is being analyzed, and its boundaries — what triggers the start of the process, and what marks its end.}}

## 2. PRD Alignment

PRD: {{outputs/<project-code>-PRD.md, or "none"}}

**Product scope**

| PRD Feature ID | Feature |
|---|---|
| {{F-0X, or "Not in PRD"}} | {{feature name in the PRD}} |

**Contribution to North Star Metric & OKRs**

| Metric / Key Result | How This Feature Contributes |
|---|---|
| {{North Star Metric, or KR ID and text}} | {{...}} |

**User journey pain points addressed**

| Journey | Touchpoint | Role | Pain Point | How This Feature Addresses It |
|---|---|---|---|---|
| {{journey name}} | {{touchpoint}} | {{role}} | {{pain point as in the PRD}} | {{...}} |

## 3. Roles Involved

| Actor Type | Role | Responsibility in this process |
|---|---|---|
| {{Primary / Secondary}} | {{role}} | {{...}} |

## 4. Business Rules

*Rules, policies, validations, and exceptions that govern this process. They apply to both the as-is and to-be process.*

| Rule | Description | Source (policy doc / SOP / stated by role) |
|---|---|---|
| {{...}} | {{...}} | {{...}} |

## 5. As-Is: Process Description

{{How the process currently runs, in order — every actor and every step that delivers the user's outcome, including back-office and hidden tasks the end user never sees.}}

1. {{Role}} — {{step}}
2. {{Role}} — {{step}}

```mermaid
flowchart TD
    subgraph Role_A[{{Role A}}]
        A1[{{Step}}] --> A2[{{Step}}]
    end
    subgraph Role_B[{{Role B}}]
        B1[{{Step}}]
    end
    A2 --> B1
```

## 6. As-Is: Systems Involved

| Process Step | System/Tool | Notes |
|---|---|---|
| {{...}} | {{...}} | {{...}} |

## 7. As-Is: Pain Points / Issues

| Pain Point | Process Step(s) Affected | Root Cause (if known) | Who Raised It |
|---|---|---|---|
| {{...}} | {{...}} | {{...}} | {{...}} |

## 8. To-Be: Process Description

{{How the process should run once the feature is delivered — every actor and every step, including back-office and hidden tasks.}}

1. {{Role}} — {{step}}
2. {{Role}} — {{step}}

```mermaid
flowchart TD
    subgraph Role_A[{{Role A}}]
        A1[{{Step}}] --> A2[{{Step}}]
    end
    subgraph Role_B[{{Role B}}]
        B1[{{Step}}]
    end
    A2 --> B1
```

## 9. Gap Analysis — As-Is vs. To-Be

*Factual comparison of how the process steps differ between as-is and to-be.*

| As-Is Step | To-Be Step | Change Type (New/Modified/Removed/Unchanged) | Pain Point Addressed |
|---|---|---|---|
| {{...}} | {{...}} | {{...}} | {{...}} |

## 10. Non-Functional Requirements

*Feature-level NFRs; user stories reference them by ID.*

| NFR ID | Category | Requirement | Source |
|---|---|---|---|
| {{NFR-01}} | {{Performance/Security/Usability/Scalability/Availability/Compliance/Other}} | {{...}} | {{e.g., "As-Is: Current Performance Baseline" / "As-Is: Pain Points" / "stakeholder interview"}} |

## 11. Open Questions

{{Unresolved items.}}

## 12. Document Control & Revision History

| Field | Value |
|---|---|
| Status | Draft / In Review / Approved |

**Revision History**

| Version | Date | Change Description | Trigger / Reason |
|---|---|---|---|
| 1.0 | {{date}} | Initial draft | {{e.g., "Initial interviews with process owners"}} |
