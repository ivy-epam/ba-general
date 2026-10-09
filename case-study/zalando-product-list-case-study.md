---
template: case-study
title: Project Case Study Template
version: 1.0
last_updated: 2026-10-09
owner: ivy_li@epam.com
used_by_skill: generate-case-study
---

# zalando — product-list — Case Study

## 1. Document Control

| Field | Value |
|---|---|
| Client | zalando |
| Project | product-list |
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

Zalando's site offerings lacked direct relevance to each customer's recent actions, preferences, and style interests, limiting inspiration, engagement, and order placement.

- **Generic product surfacing**: product lists weren't tied to a customer's recent behavior or style interests, making the browsing experience feel one-size-fits-all.
- **Missed re-engagement opportunities**: there was no systematic way to resurface relevant items — like wishlisted products going on sale or running low in stock — at the moment they mattered most.
- **Reduced inspiration and engagement**: without content tailored to individual preferences, customers had fewer compelling reasons to keep browsing or return to the site.
- **Lower order placement**: the gap between what was shown and what customers actually wanted left conversion opportunities on the table.

## 5. Solution Delivered

| Feature / Capability | Description |
|---|---|
| Personalized product lists | Launched "GenAI Product List," offering a range of tailored lists — wishlists on sale, low-stock wishlists, "complete the look" suggestions, and items similar to recently viewed products. |
| Daily/weekly refresh for relevance | Refreshed personalized product lists daily or weekly to maintain relevance and a sense of novelty. |
| Real-time stock and price accuracy | Monitored product availability and pricing hourly so lists always reflected current stock and prices. |
| LLM-driven personalization | Trained LLMs on customer and contextual data (recent trends, growing popularity, individual preferences) to recommend products and curated outfits matching each customer's interests and purchasing behavior. |
| GenAI content enrichment | Used LLMs to generate personalized product list titles, subtitles, and cover images for each user. |
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
| Production launch | The personalized product list experiment was successfully launched to production across the planned rollout markets, moving from design/experimentation into a live, customer-facing feature. |
| Data collection enablement | The live rollout began collecting user feedback and behavioral statistics against the defined measurement goals (business/GMV impact, customer engagement, content effectiveness), feeding further product improvement and GMV growth. |
| KPI framework established | Experiment success was tracked against GMVaR, AppDAU, and Product List High-Value Actions (HVAs), providing a consistent measurement framework for personalization impact. |
| Cross-border delivery alignment | Coordination across China-Shenzhen and EU teams kept tasks on track against planned deliverables, with regular status reporting sustained to both local and global management. |
| Requirement quality & compliance | BRD, technical design, and experiment design reviews maintained requirement completeness, statistical soundness, and EU-to-China data localization compliance throughout delivery. |
| UAT quality signal | Databricks-based UAT analysis surfaced defect patterns and output-quality trends that informed fix prioritization ahead of product sign-off. |
