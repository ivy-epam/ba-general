---
template: case-study
title: Project Case Study Template
version: 1.0
last_updated: 2026-10-13
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

*Scope note: as the offshore Business Analyst, I owned requirement engineering for the capabilities below — eliciting, specifying, and managing their requirements — and managed hypercare after go-live, while the platform itself was built by the engineering teams.*

| Feature / Capability | Description |
|---|---|
| Automated data requesting & readiness checks | Automated the process of requesting outsourced data and checking its readiness, replacing manual requests. |
| Automated report scheduling | Automated scheduling for report generation, removing manual SAS report generation and downloading. |
| Job status notifications | Notified stakeholders of job status automatically, keeping the review process visible. |
| Report consolidation | Consolidated reports into a single file, removing the need for external comparison tools. |
| Delta comparison | Highlighted changes from previous runs, directly surfacing discrepancies without manual reconciliation. |
| Performance monitoring | Tracked system usage and efficiency to support ongoing optimization. |
| Cloud-native ETL pipeline | Built on AWS services (Glue, S3, DynamoDB, ELB, Lambda, Step Functions), integrating clinical data comparison logic within a robust ETL pipeline. |

## 6. My Role & Responsibilities

**Title:** Offshore Business Analyst

I was the offshore BA on this GxP-regulated clinical data program, owning requirement engineering from elicitation through approval and change control, and managing hypercare after go-live. I worked with clinical operations, data management, and regulatory affairs stakeholders, and with business and IT teams across Eastern Europe, the USA, China, and India.

- **Requirements elicitation and specification** — eliciting requirements from clinical operations, data management, and regulatory affairs, and translating clinical data and blinding/unblinding workflows into functional specifications and user stories aligned with FDA 21 CFR Part 11, ICH E6 GCP, and ALCOA+ principles.
- **Process and compliance gap analysis** — mapping as-is and to-be processes for clinical data and blinding management, identifying compliance gaps, and defining audit trail, access control, and data integrity requirements.
- **GxP documentation** — standardizing BA practices and producing validation-ready artefacts (URS, FRS, traceability matrices) for system qualification (IQ/OQ/PQ).
- **Requirements approval and change control** — managing requirement approval and change control under GxP procedures, and supporting the Product Owner in prioritizing the backlog across compliance obligations, system dependencies, and business value.
- **Global stakeholder alignment** — aligning business and IT stakeholders across Eastern Europe, the USA, China, and India on regulatory requirements and validation expectations.
- **Hypercare management** — managing the hypercare period after go-live.

## 7. Key Achievements & Contributions

| Dimension | Achievement |
|---|---|
| Efficiency | Specified the requirements for automated data requesting, report scheduling, consolidation, and delta comparison, contributing to a cut in data review time from approximately 4 hours to under 15 minutes per study trial. |
| Data Quality | Defined the audit trail, access control, and data integrity requirements that, together with the removal of manual steps, contributed to fewer errors and stronger data integrity. |
| Data Availability | Specified the automated scheduling and job status notification requirements that made data available when needed. |
| Compliance | Produced standardized, validation-ready GxP documentation (URS, FRS, traceability matrices) that supported system qualification (IQ/OQ/PQ) and audit readiness. |
| Stakeholder Alignment | Aligned business and IT stakeholders across Eastern Europe, the USA, China, and India on regulatory requirements and validation expectations, contributing to smoother data delivery and coordination across roles and teams. |

