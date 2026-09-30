---
template: knowledge-page
title: Feature Knowledge Page Template
version: 1.0
last_updated: 2026-09-28
owner: ivy_li@epam.com
used_by_skill: generate-knowledge-page
---

# {{Feature Name}}

*A plain-language reference for dev, product, and ops — not a formal BA document. Written and updated incrementally as stories for this feature are delivered.*

## 1. Document Control & Revision History

| Field | Value |
|---|---|
| Feature | {{feature name}} |
| Status | Draft / In Review / Approved |

**Revision History**

| Version | Date | Change Description | Trigger / Reason |
|---|---|---|---|
| 1.0 | {{date}} | Initial page | {{e.g., "Created on delivery of US-01 (UC-01)"}} |

## 2. Overview

{{Plain-language explanation of what this feature is and why it exists — no BA jargon.}}

## 3. Key Capabilities

{{What the feature does, in plain terms — limited to what's actually been delivered so far, not what's merely planned.}}

## 4. How It Works

{{Plain-language walkthrough of the process, once the feature is live. May reuse the Mermaid diagram from the linked Feature Analysis document's To-Be: Process Description as-is.}}

## 5. Roles & Access

{{Plain-language summary of who can do what, translated from the RBAC matrix — e.g., "Customers can view and update their own orders; Support agents can view all orders and issue refunds," not a raw CRUD table.}}

## 6. Delivered Scope So Far

| Use Case | Story | Title | Delivered Date |
|---|---|---|---|
| {{UC-0X}} | {{US-0X}} | {{...}} | {{date}} |

## 7. Known Limitations / Open Items

{{Only Open Questions from source docs that are still unresolved AND relevant to what's actually live today — not the full upstream backlog.}}

## 8. Operational Notes

{{Ops-relevant NFRs from the Feature Analysis document's Non-Functional Requirements section, phrased as "what to expect / what to watch" — plus anything ops-specific gathered via interview that those NFRs don't cover.}}

## 9. Related Artifacts

- PRD: {{link}}
- Feature Analysis: {{link}}
- Use Cases: {{link}}
- RBAC: {{link}}
- User Stories: {{link(s), one per use case with a delivered story}}
