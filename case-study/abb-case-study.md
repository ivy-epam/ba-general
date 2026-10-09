---
template: case-study
title: Project Case Study Template
version: 1.0
owner: ivy_li@epam.com
---

# ABB EasyOrder (China) — Case Study

## 1. Document Control

| Field | Value |
|---|---|
| Project Code | abb |
| Author | Ivy Li (ivy_li@epam.com) |
| Created | 2026-10-09 |
| Confidentiality Level | Client name shareable externally; industry/domain shareable |

## 2. Confidentiality & Sharing Notes

| Field | Value |
|---|---|
| Client / Company Name | ABB |
| Industry / Domain | Electrification business, industrial B2B e-commerce |

## 3. Industry & Business Context

ABB's Electrification business runs EasyOrder (EO), a B2B e-commerce platform serving customers across 40+ markets, currently being migrated module-by-module off the legacy cBOL system onto a cloud-native microservices architecture. China is one of ABB's most significant markets and operates as a separate regional deployment from Global/West Europe due to regulatory requirements, including cross-border data controls under the Great Firewall, making the region both high-value and high-stakes for EasyOrder's rollout.

## 4. Problem Statement

The China cutover of EasyOrder carried outsized risk: migrating **100+ B2B customer accounts** and **five critical modules** across a global-to-China regulatory and organizational boundary, with no dedicated local coordination role in place. This opened seven concrete gaps between global and China teams:

1. **Communication & alignment gaps** on planned tasks/deliverables.
2. **Lack of system feedback** — low visibility into stability and change-request status.
3. **Slow response & turnaround** on issue resolution.
4. **Customer dissatisfaction** with unfriendly changes.
5. **Release & change transparency gaps**.
6. **Trust & cooperation issues** between global and local teams.
7. **Unaligned expectations** causing friction and rework.

## 5. Solution Delivered

*Scope note: the solution was to onboard a dedicated Business Engagement Manager (CN) role to own five areas of China-specific EasyOrder operations — not to rebuild the underlying platform itself, which remained owned by other teams.*

| Feature / Capability | Description |
|---|---|
| Local stakeholder management | Single point of contact bridging the Global Core EO IT Team and Chinese business/IT stakeholders |
| Customer onboarding management | Coordinated 3-wave onboarding of China customers onto EasyOrder |
| Incident management | Owned full incident lifecycle — intake, documentation, escalation with context, and SLA-bound resolution |
| Change request management | Analyzed China-originated change requests and brokered feasibility/alignment between dev and business stakeholders |
| Team coordination | Coordinated module cutover (5 modules), UAT, and production smoke testing across onshore BAs, global and local dev, support, and SAP integration teams |

## 6. My Role & Key Contributions

**Title:** EasyOrder — Business Engagement Manager (CN).

As the sole Global IS resource embedded with the local China team, I served as the primary point of contact for Chinese business stakeholders across the EasyOrder program, applying:

- **Stakeholder management** — understanding and managing China stakeholder needs, expectations, and priorities across onboarding, incidents, and change requests.
- **Incident lifecycle management** — accurately capturing, documenting, and escalating incidents with context, then tracking them through to SLA-bound resolution.
- **Change request analysis** — assessing technical feasibility and implications of China-originated change requests and communicating them in business terms to stakeholders.
- **UAT and quality coordination** — supporting UAT and running production smoke tests ahead of each biweekly release to catch regressions before they reached customers.
- **Governance and reporting** — operating within ABB's IS Regulations, Guidelines, and agreed RACIS specifications, and preparing weekly status reports to local and global leadership.

**Scope note:** this role managed a focused slice of the much larger EasyOrder Platform 2.0 migration — China-side stakeholder engagement, incident/change coordination, and cutover coordination — rather than the underlying microservices architecture and engineering build-out of the platform itself, which is owned by other teams.

## 7. Outcomes & Measurable Impact

| Metric | Value | Source / Evidence |
|---|---|---|
| B2B customer accounts migrated | 100+ accounts in China market | Documented role achievement |
| Modules cut over from cBOL to EasyOrder | 5 critical modules (Order Dashboard, Order Management, Cart Pages, Availability Check, Reporting & Documentation) | Documented role achievement |
| Release cadence maintained | Biweekly releases shipped with production stability and minimal disruption | Documented role achievement |
| Incident frequency | Fewer incidents overall, including sustained stretches with zero incidents | User interview (team-observed, not independently quantified) |
| Incident resolution speed | Raw resolution time did not improve materially (constrained by fixed release dates), but communication and resolution *progress* became noticeably faster and easier to track | User interview |
| Stakeholder satisfaction | Local and global stakeholders acknowledged and expressed satisfaction with the improvement in production support, incident handling, and change request communication | User interview / stakeholder feedback (qualitative, not formally scored) |

**Open Questions / unverified items:**
- No numeric baseline/after figures exist for incident count or resolution time — the reduction is team-observed, not benchmarked against a tracked metric.
- Stakeholder satisfaction is reported qualitatively (acknowledgement of improvement); no formal satisfaction score or survey was cited.


