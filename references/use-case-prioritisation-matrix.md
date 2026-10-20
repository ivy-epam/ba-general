---
description: This article explains the structured framework and criteria for use case prioritisation. 
metadata:
  version: 06-10-2026
---

# Prioritisation Definition

## Use Case Prioritisation Matrix and Rules
### Dimensions
| # | Dimension        | Description                                      |
|---|------------------|--------------------------------------------------|
| 1 | **Compliance**       | Regulatory or policy obligation                  |
| 2 | **Usage Frequency**  | How often the use case is triggered in production |
| 3 | **User Volume**      | Number of distinct users affected                |
| 4 | **Business Value** | Impact on operational process or user usability: not functioning will break the flow, critical features |

Each dimension is assigned a binary value: **0** (not applicable) or **1** (applicable).
Exceptional, the Business Value dimension can be assigned 0, or 2.

### Decision Logic
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

### Threshold
| Condition                  | Classification              |
|----------------------------|-----------------------------|
| S >= 0.45                  | **P0** — High Priority      |
| S < 0.45 && >= 0.35        | **P1** — Medium Priority    |
| S < 0.35                   | **P2** — Low Priority       |

- P0 Use Cases cover the main user journey for data discovery and access.
- P1 Use Cases are supportive but not critical for basic operation.
- P2 Use Cases are either admin/edge or less frequently used.

### Matrix Table Template
| Use Case ID | Use Case Name | Compliance | Frequency | User Volume | Business Value | Score | Priority |
|-------------|---------------|------------|-----------|-------------|----------------|-------|----------|
|             |               |            |           |             |                |       |          |
|             |               |            |           |             |                |       |          |
|             |               |            |           |             |                |       |          |
|             |               |            |           |             |                |       |          |
|             |               |            |           |             |                |       |          |
|             |               |            |           |             |                |       |          |
|             |               |            |           |             |                |       |          |
|             |               |            |           |             |                |       |          |
|             |               |            |           |             |                |       |          |
|             |               |            |           |             |                |       |          |


## Flow Prioritisation Matrix and Rules

### Priority Criteria
- P0/MUST-HAVE: business stopped, direct impacts on revenue or user.
- P1/SHOULD-HAVE: business degraded, indirect impacts on revenue or user; have workarounds.
- P2/NICE-TO-HAVE: business inconvenience.

### Decision Logic
Flow priority is derived from two factors: the priority of its parent use case and the flow type.

| Use Case Priority | Flow Type                              | Flow Priority |
|-------------------|----------------------------------------|---------------|
| P0                | Happy path (main success scenario)     | P0            |
| P0                | Alternative — high frequency or volume | P1            |
| P0                | Alternative — low frequency or volume  | P2            |
| P1                | Happy path (main success scenario)     | P1            |
| P1                | Alternative — high frequency or volume | P1            |
| P1                | Alternative — low frequency or volume  | P2            |
| P2                | Any                                    | Out of scope  |

> Only P0 and P1 flows are included in smoke test coverage. P2 flows are excluded.

### Matrix Table Template
| Flow ID | Flow Name | Derived From (UC ID) | Use Case Priority | Flow Type | Flow Priority |
|---------|-----------|----------------------|-------------------|-----------|---------------|
|         |           |                      |                   |           |               |
|         |           |                      |                   |           |               |
|         |           |                      |                   |           |               |
|         |           |                      |                   |           |               |
|         |           |                      |                   |           |               |
|         |           |                      |                   |           |               |
|         |           |                      |                   |           |               |
|         |           |                      |                   |           |               |
|         |           |                      |                   |           |               |
|         |           |                      |                   |           |               |