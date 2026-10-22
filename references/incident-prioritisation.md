---
description: This article explains the structured framework and criteria for incident prioritisation and RCA analysis. 
metadata:
  version: 05-25-2026
---

# Prioritization Framework

## Incident Prioritization Framework

**Purpose:** Define how incidents are classified and prioritized based on business impact, scope, and severity.

---

### Nature Definition

Before prioritizing, identify what type of incident this is:

| Nature | Definition | Example | Response |
|--------|-----------|---------|----------|
| **Defect** | Something that worked before but is now broken; a regression or failure in existing functionality | Payment button worked yesterday, returns errors today | Fix immediately; RCA needed to prevent recurrence |
| **Requirement Gap** | Functionality was never built to handle this scenario; user expectations don't match system capability | Users expect real-time notifications but system only sends hourly digests | Clarify requirements; may become a change request, not an incident fix |
| **Design Limitation** | System works as designed but design is inadequate for the current business need | Report generation takes 2 hours for large datasets; users need results in 15 minutes | Escalate as improvement; may require architecture review |

**Why it matters:** Defects need RCA and permanent fixes. Gaps need requirements clarification. Limitations need design review. Treating them the same wastes time.

### Prioritization Dimensions

If identified and determined as Defect, then proceed to prioritization. Ask these four questions for every incident. Answer each question directly — no calculation needed.

| Dimension | Question | Possible Answers |
|-----------|----------|------------------|
| **Compliance** | Does this incident create or expose a regulatory, legal, or contractual risk? | Yes / No |
| **Scope** | Who is affected? | Single user / Multiple users |
| **Severity** | Can users still complete the process? | No — completely blocked <br/> Partially — workaround exists <br/> Yes — core process intact |
| **Path** | Which part of the workflow is broken? | Happy path (primary workflow) <br/> Alternative path (backup option) <br/> Error handling / edge case |

---

## Decision Rules

**Use this decision tree to determine defect priority. Read top to bottom; stop at the first match.**

| # | If… | Then… |
|---|-----|-------|
| 1 | Compliance = **Yes** | → **S1** (stop here, do not continue) |
| 2 | Scope = **Multiple** AND Severity = **No — completely blocked** | → **S1** |
| 3 | Scope = **Multiple** AND Severity = **Partially — workaround exists** | → **S2** |
| 4 | Scope = **Single** AND Severity = **No — completely blocked** | → **S2** |
| 5 | Scope = **Single** AND Severity = **Partially — workaround exists** | → **S3** |
| 6 | Severity = **Yes — core process intact** AND Path = **Happy path** | → **S3** |
| 7 | Severity = **Yes — core process intact** AND Path = **Alternative path** or **Error handling** | → **S4** |

---

## Priority Levels

| Priority | Response Time | Resolution Target | Definition |
|----------|----------------|-------------------|-----------|
| **S1 – Critical** | Within 15 minutes | 4 hours | Core business process blocked; multiple users unable to work; regulatory exposure; compliance breach |
| **S2 – High** | Within 15 minutes | 12 hours | Multiple users affected with workaround; single user with no workaround on critical process |
| **S3 – Medium** | Within 6 hours | 24 business hours | Non-core feature broken or single user blocked with workaround; happy path working |
| **S4 – Low** | Within 6 hours  | 40 business hours | Error handling or alternative paths broken; cosmetic issues; happy path intact |

---

## Quick Assessment Template

| Incident ID | Title | Compliance | Scope | Severity | Path | Priority | Notes |
|-------------|-------|-----------|-------|----------|------|----------|-------|
| | | Yes/No | Single/Multiple | Blocked/Workaround/Intact | Happy/Alt/Error | S1/S2/S3/S4 | |

**How to fill this:**
1. Ask the four questions above
2. Circle or mark your answer for each dimension
3. Use the decision tree to find the matching priority
4. Document any additional context in Notes

---

## Examples

**Example 1: Payment Processing Down**
- Compliance: No
- Scope: Multiple users
- Severity: No — completely blocked (customers cannot complete transactions)
- Path: Happy path (this is the primary workflow)
- **Priority: S1** (matches Rule 2: Multiple + completely blocked)

---

**Example 2: Report Export Fails, But Download Works**
- Compliance: No
- Scope: Multiple users
- Severity: Partially — workaround exists (users can download raw data instead)
- Path: Happy path (this is a primary user need)
- **Priority: S2** (matches Rule 3: Multiple + workaround)

---

**Example 3: Dashboard Widget Formatting Broken**
- Compliance: No
- Scope: Single user
- Severity: Yes — core process intact (data is correct, display is wrong)
- Path: Alternative path (user can view data in table form)
- **Priority: S4** (matches Rule 7: Core process intact + alternative path)

---

**Example 4: PII Data Exposed in Error Log**
- Compliance: Yes
- Scope: N/A
- Severity: N/A
- Path: N/A
- **Priority: S1** (matches Rule 1: Compliance = Yes, stop here)

---

## Notes for Incident Response Teams

- **Use this framework consistently** so stakeholders develop confidence in prioritization
- **Reassess as new information arrives** — initial priority may change if scope or severity expands
- **Document the scoring** so future reviews understand the reasoning
- **Collect feedback** — if the same incident type keeps getting misclassified, refine your definitions
