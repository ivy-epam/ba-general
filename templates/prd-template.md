---
template: prd
title: Product Requirements Document Template
version: 2.0
last_updated: 2026-10-22
owner: ivy_li@epam.com
used_by_skill: generate-prd
---

# {{Product Name}} ({{Project Code}}) — Product Requirements Document

## 1. Problem Statement & Business Context

**Problem statement:** {{the ultimate, high-level problem and its consequence}}

**Business context:** {{business drivers, why now, strategic fit}}

## 2. User Journeys

### {{Journey name}} — {{actor or end user}}

**Scene:** {{who the user is at the start, what triggers the journey, and the outcome they are after}}

| Stage | Touchpoint | What the User Does |
|---|---|---|
| {{stage}} | {{channel, person, or system the user meets}} | {{action}} |

**Pain points by role and touchpoint**

| Touchpoint | Role | Pain Point |
|---|---|---|
| {{touchpoint}} | {{role}} | {{problem this role faces at this touchpoint}} |

## 3. Product Vision & Objectives

**Vision:** {{one-sentence product vision}}

**North Star Metric**

| Metric | Definition |
|---|---|
| {{metric name}} | {{how it is measured}} |

**OKRs**

| Objective | Key Result |
|---|---|
| O1 — {{objective}} | KR1.1 — {{measurable result}} |
| | KR1.2 — {{measurable result}} |

## 4. Actors & End Users

*Primary actors use the product directly to achieve their goals. Secondary actors support, approve, or are consulted in what primary actors do. End users are the ultimate beneficiaries of the product's outcome, whether or not they use it themselves.*

| Type | Actor / User | Use / Interaction with Product | Goal / Benefit |
|---|---|---|---|
| Primary | {{actor}} | {{how they use or interact with the product}} | {{what they achieve with the product}} |
| Secondary | {{actor}} | {{how they use or interact with the product}} | {{how they take part}} |
| End user | {{beneficiary}} | {{how they use or interact with the product}} | {{benefit received}} |

## 5. Product Scope & Key Features

**In scope — key features:**

*Priority: **P0** — critical; the product cannot launch without it. **P1** — high; needed for the product to meet its core objectives, soon after launch if not at it. **P2** — medium; adds clear value but can wait. **P3** — low; nice to have, candidate for later.*

*Prioritisation method(s): {{one or two of RICE / MoSCoW / WSJF, or "Stated directly"}} — applied: {{method}}*

### P0 — Critical

| ID | Feature | Description | {{Method 1}} Result | {{Method 2}} Result |
|---|---|---|---|---|
| F-01 | {{feature name}} | {{one-sentence description}} | {{calculation → score → priority (effort), e.g. "4 × 2 × 80% = 6.4 → P0 (Effort: 3 person-weeks)"}} | {{e.g. "Must → P0"}} |

### P1 — High

| ID | Feature | Description | {{Method 1}} Result | {{Method 2}} Result |
|---|---|---|---|---|
| {{F-0X}} | {{...}} | {{...}} | {{...}} | {{...}} |

### P2 — Medium

| ID | Feature | Description | {{Method 1}} Result | {{Method 2}} Result |
|---|---|---|---|---|
| {{F-0X}} | {{...}} | {{...}} | {{...}} | {{...}} |

### P3 — Low

| ID | Feature | Description | {{Method 1}} Result | {{Method 2}} Result |
|---|---|---|---|---|
| {{F-0X}} | {{...}} | {{...}} | {{...}} | {{...}} |

**Out of scope:**
- {{capability-level item}}

## 6. Roadmap

| Phase | Timeframe | Features | Milestone / Exit Criteria |
|---|---|---|---|
| {{e.g., "MVP"}} | {{e.g., "Q1 2027" or TBD}} | {{F-01, F-02}} | {{what marks the phase complete}} |

## 7. Risk Register

*Severity: **High** — threatens the product's viability or a core objective; **Medium** — delays or reduces achievement of an objective; **Low** — limited, contained effect.*

| ID | Risk Description | Severity | Impact | Mitigation Plan | Owner |
|---|---|---|---|---|---|
| R-01 | {{risk}} | {{High / Medium / Low}} | {{effect on product outcomes or objectives}} | {{...}} | {{role or person}} |

## 8. Assumptions, Constraints & Dependencies

**Assumptions:**
- {{...}}

**Constraints:**
- {{...}}

**Dependencies:**
- {{...}}

## 9. Decision Notes

| ID | Date | Decision | Rationale | Decided By |
|---|---|---|---|---|
| D-01 | {{date}} | {{decision}} | {{why}} | {{person / forum}} |

## 10. Open Questions

| ID | Question |
|---|---|
| OQ-01 | {{question}} |

## 11. Glossary / Appendix

Domain analysis: {{outputs/<client>-<project-code>-domain-analysis.md, or "none"}}

| Term | Definition |
|---|---|
| {{term}} | {{definition}} |

{{Supporting reference material.}}

## 12. Document Control & Revision History

| Field | Value |
|---|---|
| Status | Draft / In Review / Approved |

**Revision History**

| Version | Date | Change Description | Trigger / Reason |
|---|---|---|---|
| 1.0 | {{date}} | Initial draft | {{e.g., "Created from BRD"}} |
