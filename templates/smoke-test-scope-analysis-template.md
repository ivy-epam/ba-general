---
template: smoke-test-scope-analysis
title: Smoke Test Scope Analysis Template
version: 1.1
last_updated: 2026-10-22
owner: ivy_li@epam.com
used_by_skill: generate-smoke-test
---

# Smoke Test Scope Analysis — {{Application Name}}

*Context analysis for the smoke test suite: what the application is, which modules are in scope, and each module's status this run. Created in Creation mode and updated in Modification mode.*

## 1. Application Overview

### 1.1 Primary Business Nature

**{{Short label}}** — {{What the application is and the problem it solves.}}

### 1.2 Read/Write Balance

**{{Read-Heavy / Write-Heavy / Balanced}}** — {{Which operations dominate production traffic; which writes exist and how often.}}

### 1.3 End User and Primary Intent

**Primary User Segments:**
- **{{Segment}}**: {{who they are and what they do}}

**Primary Intent:** {{The core outcome users come to the application for.}}

### 1.4 Compliance Concerns

- **{{Concern}}**: {{why it matters for what smoke tests may touch in production}}

## 2. Module Overview

### Module {{N}}: {{Module Name}}

| Attribute | Value |
|---|---|
| **Module Name/Code** | {{...}} |
| **Module Status** | {{New / Updated / Unchanged / Deprecated}} |
| **Features** | {{features in this module, each linking to `outputs/features/<feature>/`, or blank}} |
| **Main Usage Patterns** | {{frequency; read vs. write}} |
| **Module Criticality** | {{Low / Medium / High}} — {{rationale}} |
| **Scope Notes** | {{confirmed scope decisions and assumptions, or "None"}} |

**Use Cases — {{Module Name}}**

| UC ID | Use Case | Description | Primary Actor | Primary Flow | Status |
|---|---|---|---|---|---|
| UC-01 | {{...}} | {{...}} | {{role}} | {{Step → Step → Step}} | {{New / Updated / Unchanged / Deprecated}} |

## 3. Document Control & Revision History

| Field | Value |
|---|---|
| Status | Draft / Confirmed |

**Revision History**

| Version | Date | Module(s) | Change Summary |
|---|---|---|---|
| 1.0 | {{date}} | {{module(s)}} | {{e.g., "Initial scope analysis"}} |
