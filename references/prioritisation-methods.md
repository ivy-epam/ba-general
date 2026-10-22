---
description: This article explains the prioritisation methods available to skills, grouped into Test Prioritisation (Custom) and Implementation Prioritisation (RICE, MoSCoW, WSJF), and how each maps to the common P0–P3 priority scale.
metadata:
  version: 10-22-2026
---

# Prioritisation Methods

## Overview

| Group | Method | Applies to | Best for | Inputs | Native output |
|-------|--------|------------|----------|--------|---------------|
| Test | **Custom** | Smoke-test use cases | Deciding which use cases need build-stability coverage | Compliance, Usage Frequency, User Volume, Business Value | Weighted score (or compliance gate) |
| Implementation | **RICE** | Features, user stories | Comparing items by how many users they reach and how much they help each | Reach, Impact, Confidence (Effort shown alongside) | Priority score |
| Implementation | **MoSCoW** | Features, user stories | Agreeing release scope with stakeholders | Category judgement | Must / Should / Could / Won't |
| Implementation | **WSJF** | Features, user stories | Ranking items by the cost of delaying them | User/Business Value, Time Criticality, Risk Reduction/Opportunity Enablement (Job Size shown alongside) | Cost of Delay |

## Common Priority Scale

Every method maps its native output to this scale. Custom, RICE and WSJF use P0–P2; only MoSCoW uses P3 (Won't have this time).

| Priority | Meaning |
|----------|---------|
| **P0** — Critical | Cannot launch or operate without it |
| **P1** — High | Needed to meet core objectives, at or soon after launch |
| **P2** — Medium | Adds clear value but can wait |
| **P3** — Low | Nice to have; candidate for later |

---

# Part 1 — Test Prioritisation

## Custom

Decides which use cases need smoke tests. Produces P0–P2; P3 is not used.

### Matrix and Rules
#### Dimensions
| # | Dimension        | Description                                      |
|---|------------------|--------------------------------------------------|
| 1 | **Compliance**       | Regulatory or policy obligation                  |
| 2 | **Usage Frequency**  | How often the use case is triggered in production |
| 3 | **User Volume**      | Number of distinct users affected                |
| 4 | **Business Value** | Impact on operational process or user usability: not functioning will break the flow, critical features |

Each dimension is assigned a binary value: **0** (not applicable) or **1** (applicable).
Exceptional, the Business Value dimension can be assigned 0, or 2.

#### Decision Logic
Step 1 — Compliance Gate (One-Vote Override)
> If **Compliance = 1**, the use case is **automatically classified as a P0 smoke-test case** — no further scoring is required.

Step 2 — Weighted Scoring (when Compliance = 0)
When the compliance dimension does not apply, the remaining three dimensions are evaluated using a weighted formula.

**Weights**
| Dimension            | Weight |
|----------------------|--------|
| Usage Frequency      | 25 %   |
| User Volume          | 55 %   |
| Business Value       | 20 %   |

**Weighted Score Formula**

S = 0.25 × x_frequency + 0.55 × x_users + 0.20 × (x_business / 2)

Where:
- x_frequency = Usage Frequency (0 or 1)
- x_users = User Volume (0 or 1)
- x_business = Business Value (0, 1, or 2)

#### Threshold
| Condition                  | Classification              |
|----------------------------|-----------------------------|
| S >= 0.45                  | **P0** — High Priority      |
| S < 0.45 && >= 0.35        | **P1** — Medium Priority    |
| S < 0.35                   | **P2** — Low Priority       |

- P0 Use Cases cover the main user journey for data discovery and access.
- P1 Use Cases are supportive but not critical for basic operation.
- P2 Use Cases are either admin/edge or less frequently used.

#### Matrix Table Template
| Use Case ID | Use Case Name | Compliance | Frequency | User Volume | Business Value | Score | Priority |
|-------------|---------------|------------|-----------|-------------|----------------|-------|----------|
|             |               |            |           |             |                |       |          |

---

# Part 2 — Implementation Prioritisation

## RICE

### Factors
| Factor | Question | Scale |
|--------|----------|-------|
| **Reach** | What share of the product's users will this affect? | 5 = all or almost all, 4 = most, 3 = about half, 2 = a minority, 1 = very few |
| **Impact** | How much will it move the objective for each user reached? | 3 = massive, 2 = high, 1 = medium, 0.5 = low, 0.25 = minimal |
| **Confidence** | How sure are we of the reach and impact estimates? | 100% = high, 80% = medium, 50% = low |
| **Effort** | How much work will it take across all disciplines? | Person-weeks or person-months (use one unit for the whole set) |

### Formula

Priority Score = Reach × Impact × Confidence  (range 0.125 – 15)

Effort is not part of the priority. It is shown in its own column so effort can be weighed by eye alongside the priority.

### Mapping to Priority
| Priority Score | Priority |
|----------------|----------|
| ≥ 6            | **P0**   |
| 3 – < 6        | **P1**   |
| < 3            | **P2**   |

### Table Template
| ID | Item | Reach | Impact | Confidence | Calculation | Priority Score | Priority | Effort |
|----|------|-------|--------|------------|-------------|----------------|----------|--------|
|    |      |       |        |            |             |                |          |        |

## MoSCoW

### Categories
| Category | Definition |
|----------|------------|
| **Must have** | Non-negotiable for this release; without it the release fails or is unusable, unsafe, or non-compliant |
| **Should have** | Important but not vital; a workaround exists if it slips |
| **Could have** | Desirable; included if time and capacity allow |
| **Won't have (this time)** | Agreed as out of this release; may return later |

Guideline: Must haves should take no more than about 60% of the available capacity, so Should and Could items leave room to absorb risk.

### Mapping to Priority
| Category | Priority |
|----------|----------|
| Must have | **P0** |
| Should have | **P1** |
| Could have | **P2** |
| Won't have (this time) | **P3** |

### Table Template
| ID | Item | Category | Rationale | Priority |
|----|------|----------|-----------|----------|
|    |      |          |           |          |

## WSJF (Weighted Shortest Job First)

### Components
| Component | Question |
|-----------|----------|
| **User/Business Value** | How much value does this deliver to users or the business? |
| **Time Criticality** | How quickly does the value decay if delivery is delayed (e.g. a fixed deadline)? |
| **Risk Reduction / Opportunity Enablement** | Does this reduce a risk or enable other work or opportunities? |
| **Job Size** | How large is the effort to deliver it? |

Score every component on the modified Fibonacci scale **1, 2, 3, 5, 8, 13, 20** — 1 is the lowest value, urgency, risk reduction, or size; 20 the highest.

### Formula

Cost of Delay = User/Business Value + Time Criticality + Risk Reduction/Opportunity Enablement  (range 3 – 60)

Priority is set by Cost of Delay alone. Job Size is not divided in; it is shown in its own column so size can be weighed by eye alongside the priority.

### Mapping to Priority
| Cost of Delay | Priority |
|---------------|----------|
| ≥ 30          | **P0**   |
| 15 – 29       | **P1**   |
| < 15          | **P2**   |

### Table Template
| ID | Item | User/Business Value | Time Criticality | Risk Reduction / Opportunity Enablement | Calculation | Cost of Delay | Priority | Job Size |
|----|------|---------------------|------------------|-----------------------------------------|-------------|---------------|----------|----------|
|    |      |                     |                  |                                         |             |               |          |          |
