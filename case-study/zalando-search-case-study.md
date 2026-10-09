---
template: case-study
title: Project Case Study Template
version: 1.0
last_updated: 2026-10-09
owner: ivy_li@epam.com
used_by_skill: generate-case-study
---

# zalando — search — Case Study

## 1. Document Control

| Field | Value |
|---|---|
| Client | zalando |
| Project | search |
| Author | Ivy Li (ivy_li@epam.com) |
| Created | 2026-10-09 |
| Confidentiality Level | Client name and industry/domain shareable externally |

## 2. Confidentiality & Sharing Notes

| Field | Value |
|---|---|
| Client / Company Name | Zalando |
| Industry / Domain | European fashion & lifestyle e-commerce — personalized search and GenAI-driven discovery |

## 3. Industry & Business Context

Zalando is one of Europe's largest fashion and lifestyle e-commerce platforms, competing in a market where online retailers are under growing pressure to move beyond pure search-and-buy transactions toward AI-driven, inspiration-led discovery that keeps exploratory shoppers engaged. 

## 4. Problem Statement

Zalando's search experience served customers with clear, intent-driven queries well, but under-served exploratory shoppers who arrived with only a vague idea and were open to inspiration.

- **Under-served exploration**: existing search logic favored intent-driven queries, leaving customers with only a vague idea in mind and no clear search term underserved.
- **Not timely refreshed trend/style lists**: trending content wasn't refreshed often enough to feel current, undercutting the sense of novelty needed to keep exploratory shoppers coming back.
- **No personalized recommendations**: discovery content wasn't tailored to individual customers' age, gender, geo-location, or recent interactions, making the experience feel generic rather than relevant.
- **Unused engagement signals**: rich signals such as recent interactions, contextual factors, and high-value actions went uncaptured in the discovery experience, leaving engagement and conversion opportunities on the table.

## 5. Solution Delivered

| Feature / Capability | Description |
|---|---|
| "Your Weekly Trend Leaderboard" | Introduced an engaging leaderboard on the search page that showcases and ranks the latest trending brands and products, surfacing trending topics during search to encourage discovery and exploration. |
| Weekly refresh for novelty | Refreshed the leaderboard weekly to maintain a sense of novelty and relevance rather than showing static, stale content. |
| Personalized content and ranking | Personalized both the content and ranking of leaderboard items for each customer, factoring in age, gender, and preferred sales channel to address each customer's subtle interests. |
| Multi-source content blending | Combined customer personal data, contextual signals (seasonality, location, weather), and marketing/sponsored content into a single, balanced ranking. |
| Phased experiment rollout | Experiment scoped and launched across a selected set of sales channels/countries/markets, chosen by market size, exposure targets, and product stockability. |

## 6. My Role & Key Contributions

**Title:** Project Coordinator (China-EU).

The role bridged EU and China-Shenzhen teams co-building a GenAI personalization feature across different languages, working styles, and cooperation norms. As Project Coordinator, I:

- **Coordinated cross-location delivery** — ran agile ceremonies and tracked risks/dependencies across China-Shenzhen and EU stakeholders (Principal Engineer, Experiment Analysts, Portfolio Manager, PMO) to keep work on track.
- **Reviewed requirements and designs** — checked BRDs, technical designs, and experiment designs for completeness, statistical soundness, and EU-to-China data localization compliance.
- **Translated roadmap to backlog** — partnered with the Product Manager to turn the GenAI roadmap into delivery plans, managing a prioritized backlog across experiments, feature rollouts, and tech debt.
- **Built requirements traceability** — linked GenAI features to product KPIs (engagement, conversion uplift, personalization accuracy).
- **Led UAT** — used Databricks to analyze test results, defect patterns, and output-quality trends, prioritizing fixes for sign-off.
- **Managed reporting and ad hoc requests** — supported the Product Manager, Tech Lead, and dev team, and ran regular reporting to local and global management.

## 7. Outcomes & Measurable Impact

| Metric | Value |
|---|---|
| Production launch | The personalized search leaderboard experiment was successfully launched to production across the planned rollout markets, moving from design/experimentation into a live, customer-facing feature. |
| Data collection enablement | The live rollout began collecting user feedback and behavioral statistics, feeding further product improvement, deeper user-behavior understanding, and ultimately GMV growth. |
| Cross-border delivery alignment | Coordination across China-Shenzhen and EU teams kept tasks on track against planned deliverables, with regular status reporting sustained to both local and global management. |
| Requirement quality & compliance | BRD, technical design, and experiment design reviews maintained requirement completeness, statistical soundness, and EU-to-China data localization compliance throughout delivery. |
| UAT quality signal | Databricks-based UAT analysis surfaced defect patterns and output-quality trends that informed fix prioritization ahead of product sign-off. |

