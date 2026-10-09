---
template: case-study
title: Project Case Study Template
version: 1.0
last_updated: 2026-10-09
owner: ivy_li@epam.com
used_by_skill: generate-case-study
---

# merck — Case Study

## 1. Document Control

| Field | Value |
|---|---|
| Client | merck |
| Author | Ivy Li (ivy_li@epam.com) |
| Created | 2026-10-09 |
| Confidentiality Level | Client name and industry/domain shareable externally |

## 2. Confidentiality & Sharing Notes

| Field | Value |
|---|---|
| Client / Company Name | Merck |
| Industry / Domain | Pharmaceutical — clinical trials data management and discrepancy reporting (GxP-regulated) |

## 3. Industry & Business Context

Merck is a global pharmaceutical company operating in the highly regulated clinical trials space, where data integrity and audit-trail rigor are enforced under frameworks such as FDA 21 CFR Part 11, ICH E6 GCP, and ALCOA+ principles. As trial data volumes grow and studies span multiple global sites, pharmaceutical sponsors face increasing pressure to validate and reconcile clinical data quickly without compromising regulatory compliance.

## 4. Problem Statement

Clinical Data Managers (CDMs) reviewed trial data through a fully manual, fragmented process that grew harder to sustain as data volumes increased.

- **Manual, multi-tool workflow**: CDMs manually requested outsourced data, validated sources offline, generated individual SAS reports, and used external comparison tools to reconcile them against prior versions.
- **Human intervention at every step**: discrepancy identification and reporting required manual effort throughout, from data pulls to emailing results.
- **Fragmented tooling**: reliance on isolated tools and scripts left the process disjointed, with no single system of record.
- **Didn't scale**: as data volumes grew, the manual process became increasingly inefficient and difficult to sustain.

## 5. Solution Delivered

| Feature / Capability | Description |
|---|---|
| Automated data requesting & readiness checks | Automated the process of requesting outsourced data and checking its readiness, replacing manual requests. |
| Automated report scheduling | Automated scheduling for report generation, removing manual SAS report generation and downloading. |
| Job status notifications | Notified stakeholders of job status automatically, keeping the review process visible. |
| Report consolidation | Consolidated reports into a single file, removing the need for external comparison tools. |
| Delta comparison | Highlighted changes from previous runs, directly surfacing discrepancies without manual reconciliation. |
| Performance monitoring | Tracked system usage and efficiency to support ongoing optimization. |
| Cloud-native ETL pipeline | Built on AWS services (Glue, S3, DynamoDB, ELB, Lambda, Step Functions), integrating clinical data comparison logic within a robust ETL pipeline. |

## 6. My Role & Key Contributions

**Title:** Business Analyst.

As BA on this GxP-regulated clinical data program, I:

- **Led requirements elicitation** — engaged clinical operations, data management, and regulatory affairs stakeholders, translating clinical data and blinding/unblinding workflows into functional specifications and user stories aligned with FDA 21 CFR Part 11, ICH E6 GCP, and ALCOA+ principles.
- **Mapped as-is and to-be processes** — for clinical data and blinding management, identifying compliance gaps and defining audit trail, access control, and data integrity requirements.
- **Managed requirements approval and change control** — under GxP procedures, and supported the Product Owner in prioritizing the backlog across compliance obligations, system dependencies, and business value.
- **Standardized BA practices and documentation for GxP delivery** — producing validation-ready artefacts (URS, FRS, traceability matrices) to support system qualification (IQ/OQ/PQ).
- **Aligned global stakeholders** — business and IT stakeholders across Eastern Europe, the USA, China, and India on regulatory requirements and validation expectations.

## 7. Outcomes & Measurable Impact

| Metric | Value |
|---|---|
| Review time reduced | Data review time was reduced from approximately 4 hours to under 15 minutes per study trial. |
| Improved data quality | Automation minimized manual work, resulting in fewer errors and enhanced data integrity. |
| Timely data access | Automated scheduling ensured data was available when needed. |
| Streamlined collaboration | The system enabled smoother data delivery and coordination across roles and teams. |
| Validation-ready delivery | Standardized GxP documentation and traceability matrices supported system qualification (IQ/OQ/PQ) and audit readiness. |
