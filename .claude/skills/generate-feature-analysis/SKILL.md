---
name: generate-feature-analysis
description: Create a new As-Is/To-Be Process & Gap Analysis document or update an existing one, for a specific feature/process. Covers the current-state process, systems and pain points (as-is); the intended future-state process as described by stakeholders (to-be); the business rules both follow — each process covering every actor and step, including hidden back-office tasks; and a factual gap comparison between the two. Use when the user asks to analyze/document the as-is process, to-be process, current-state process, business rules, pain points, or gap analysis for a feature.
---

# Generate Feature Analysis (As-Is / To-Be / Gap Analysis)

Produces or updates a feature-level process analysis document that sits between the PRD (product-level what/why) and detailed functional requirements (a later, separate artifact). It captures how a process works **today** (as-is), how stakeholders say it **should** work once the feature is delivered (to-be), and the factual **gaps** between the two.

**Scope discipline:** to-be content must always come from what a stakeholder actually says during interview — never invent, design, or infer a future-state step on their behalf. Business rules are fundamental: the feature changes how they are carried out, not the rules themselves, so one Business Rules section serves both as-is and to-be. Gap Analysis states *what differs*, not *how to solve it* — actual solution/functional design belongs to a later artifact, not this one.

The template lives at `templates/feature-analysis-template.md` in this project.

All output files are written inside this project, under `outputs/features/<feature>/<feature>-feature-analysis.md` — named by the **feature**, not the project code, since a project can span multiple features and each needs its own analysis, and grouped in a folder alongside that feature's other artifacts (`generate-use-cases`, `generate-knowledge-page`).

## Step 0 — Determine mode: create or update

Ask (or infer from the user's request) whether this is:
- **Create**: no existing analysis document for this feature yet.
- **Update**: an analysis document already exists and needs to be revised.

If the user references an existing `outputs/features/*/*-feature-analysis.md` file, or one is otherwise supplied/linked, treat it as **Update**. Otherwise treat it as **Create**.

## Create mode

1. **Get the feature name** (this is the primary key for this run — used for the title and filename) and, separately, **the project code** if not already known (used only to locate the related PRD). **Check for a related PRD.** If a project code is given (or inferable), check whether `outputs/<project-code>-PRD.md` exists in this project. If it does, read it as the product-level reference for this feature:
   - User Journeys (pain points by role and touchpoint) and Actors & End Users → ground as-is interview questions.
   - The feature's row in Product Scope & Key Features, and Product Vision & Objectives → ground to-be interview questions and the PRD Alignment check (step 5).
   Reference PRD items by ID or name rather than restating them.

   **Scope check:** find the feature in Product Scope & Key Features. If it isn't listed, or the PRD puts it out of scope, tell the user before continuing, and on proceeding record it as an Open Question and recommend updating the PRD with `generate-prd`.

2. **Interview-first, as-is before to-be.** This information usually lives in stakeholders' heads, not documents, so lead with structured questions rather than waiting for source material:
   - **As-is first:**
     - Process Overview/Scope → "What triggers this process, and what marks it as complete?"
     - Roles Involved → "Who's involved, and what does each do? Who drives the process, and who supports, approves, or is consulted?"
     - Process Description → "Walk me through every step as it happens today, in order, and who does each — including behind-the-scenes work the end user never sees, such as checks, handoffs, and manual workarounds."
     - Business Rules → "What rules, policies, validations, or exceptions govern this process, whoever or whatever carries it out?" A workaround people use to get around a rule is part of the as-is process or a pain point, not a rule.
     - Systems Involved → "What systems or tools are used at each step?"
     - Pain Points → "Where does this break down or frustrate people — for each role, including those who only wait on or receive the outcome? Root cause if known?"
   - **Then to-be**, grounded in the linked PRD's capabilities where available:
     - Process Description → "Once this feature exists, how should this process work instead — every step and who does it, including behind-the-scenes work?"
     - If a stakeholder says a rule itself will change, don't record it as a to-be rule: it's a policy decision beyond this feature. Add an Open Question, and recommend recording the decision in the PRD's Decision Notes once it's made.

3. **Treat any supplied documents (SOPs, process docs, BRD/PRD mentions) as equal-priority supplements, not the primary source.** Use them to confirm or fill gaps in interview answers. Do not let a document silently override what a stakeholder said, or vice versa — if a document and an interview answer disagree (e.g., documented policy vs. actually-practiced rule, or a PRD capability vs. a stakeholder's stated to-be process), record the conflict verbatim under Open Questions, naming both sources.

4. **No fabrication applies to both sides** — to-be items in particular must trace to something a stakeholder actually said, not a document alone.

5. **PRD Alignment** (skip, with PRD "none", if no PRD exists). Using the confirmed to-be content, propose — each tagged with its source:
   - **Product scope:** the feature's PRD ID and name.
   - **Roles:** Roles Involved uses the PRD's Actors & End Users names and types — **Primary** drives the process for their own goal; **Secondary** supports, approves, or is consulted. A role the PRD lacks, or typed differently, is listed in the summary as a PRD candidate.
   - **North Star Metric & OKRs:** which the feature contributes to, and how.
   - **Journey pain points:** which PRD pain points (journey, touchpoint, role) the feature addresses, and how. Pain points stay as worded in the PRD; an as-is pain point the PRD doesn't have is recorded in As-Is: Pain Points only, and listed in the summary as a candidate for the PRD.

   Wait for the user to confirm, correct, or remove each. A feature that contributes to no metric or key result, or addresses no PRD pain point, gets an Open Question.

   **Validate against the PRD pain points:** compare the confirmed list with every PRD pain point at the journey touchpoints this feature's process covers. Any left unaddressed means the feature may fall short of its intended goal — list each in the summary and add an Open Question asking whether another feature covers it or the gap is accepted.

6. **Build the Gap Analysis table** by pairing as-is and to-be steps the stakeholder described for the same part of the process, tagging each row New / Modified / Removed / Unchanged. Only fill in "Pain Point Addressed" when the stakeholder explicitly linked the to-be change to a pain point — do not infer that connection yourself.

7. **Build the Non-Functional Requirements section.** This section is feature-level and is the single source of truth other artifacts (user stories) will reference by NFR ID rather than duplicate — so it belongs here, not in those downstream documents. Propose NFR candidates inferred from this document's own As-Is: Current Performance Baseline and As-Is: Pain Points/Issues content, plus any relevant constraints from the linked PRD, each tagged with its source. Present the proposed list to the user for confirmation. Interview directly for concrete targets/thresholds none of these sources specify (e.g., "any specific response-time or uptime requirement here?").

8. **Populate the Mermaid flowcharts** (as-is and to-be process) using only confirmed content — one role-based subgraph per actor, so every handoff and hidden step is visible. Omit or simplify a diagram rather than padding it with unconfirmed detail.

9. **Draft the document** following `templates/feature-analysis-template.md` exactly, in Markdown.

10. **Write the output** to `outputs/features/<feature>/<feature>-feature-analysis.md`, using the feature name gathered in step 1.

11. **Summarize for the user**, also covering: as-is vs. to-be interview content, the key gaps identified, which NFRs were inferred vs. interview-confirmed, and PRD alignment — scope status, metrics/OKRs and pain points covered, and any as-is pain points to add to the PRD.

## Update mode

1. **Locate the existing analysis document** by feature name, at `outputs/features/<feature>/<feature>-feature-analysis.md`. Read its full current content and note its current version from the Revision History table.

2. **Gather what's driving the update** — re-interview on as-is and/or to-be as needed, incorporate newly supplied documents, add/revise an NFR (including one raised by a downstream use case or user story that found a gap in this section), or a created or updated PRD — re-run the scope check (step 1) and PRD Alignment (step 5) against it. Apply the same equal-priority, flag-every-conflict rule, now also checking new input against the *existing document's* current content.

3. **Apply changes**, including regenerating the relevant Mermaid diagram(s), Gap Analysis rows, or Non-Functional Requirements rows if the underlying content changed. A new or changed NFR or PRD Alignment row still goes through the same propose-then-confirm step as in Create mode.

4. **Bump the version and write back** to the same `outputs/features/<feature>/<feature>-feature-analysis.md` path.

5. **Summarize the delta for the user:** what changed, what stayed the same, and any new Open Questions.