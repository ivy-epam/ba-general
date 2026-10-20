---
template: rbac
title: Role-Based Access Control (RBAC) Matrix Template
version: 1.0
last_updated: 2026-09-28
owner: ivy_li@epam.com
used_by_skill: generate-rbac
---

# RBAC Matrix

*This is a single cumulative, product-wide document — not scoped to one feature or project code. It grows as each feature's PRD, Feature Analysis, and Use Cases are produced or updated.*

## 1. Roles Inventory

| Role Name | Description | Source(s) |
|---|---|---|
| {{Role}} | {{description}} | {{e.g., "PRD ABC-123 → Target Users"}} |

## 2. Features / Resources Inventory

| Feature/Resource Name | Source Feature |
|---|---|
| {{...}} | {{project-code / feature name}} |

## 3. RBAC Matrix

*One row per role–resource grant.*

| Role | Feature/Resource | Create | Read | Update | Delete | Source |
|---|---|---|---|---|---|---|
| {{Role}} | {{Feature/Resource}} | {{Y/blank}} | {{Y/blank}} | {{Y/blank}} | {{Y/blank}} | {{e.g., "UC-03 Basic Flow step 2" / "stakeholder interview"}} |

## 4. Open Questions

{{Unresolved items.}}

## 5. Document Control & Revision History

| Field | Value |
|---|---|
| Author | {{author}} |
| Status | Draft / In Review / Approved |

**Revision History**

| Version | Date | Feature/Project Code | Change Description |
|---|---|---|---|
| 1.0 | {{date}} | {{project-code/feature that seeded this}} | Initial draft |
