---
name: generate-feature-analysis
description: Create a new As-Is/To-Be Process & Gap Analysis document or update an existing one, for a specific feature/process. Covers the current-state process, business rules, systems, pain points, and user journey (as-is); the intended future-state process, rule changes, and user journey as described by stakeholders (to-be); and a factual gap comparison between the two. Use when the user asks to analyze/document the as-is process, to-be process, current-state process, business rules, pain points, gap analysis, or end-to-end user journey for a feature.
---

# Generate Feature Analysis (As-Is / To-Be / Gap Analysis)

Produces or updates a feature-level process analysis document that sits between the PRD (product-level what/why) and detailed functional requirements (a later, separate artifact). It captures how a process works **today** (as-is), how stakeholders say it **should** work once the feature is delivered (to-be), and the factual **gaps** between the two.

**Scope discipline:** to-be content must always come from what a stakeholder actually says during interview — never invent, design, or infer a future-state step, rule, or journey stage on their behalf. Gap Analysis states *what differs*, not *how to solve it* — actual solution/functional design belongs to a later artifact, not this one.

The template lives at `templates/feature-analysis-template.md` in this project. Always read that file first to get the current section structure — do not hardcode the structure from memory, in case the template has been edited.

All output files are written inside this project, under `outputs/feature-<feature>/<feature>-feature-analysis.md` — named by the **feature**, not the project code, since a project can span multiple features and each needs its own analysis, and grouped in a folder alongside that feature's other artifacts (`generate-use-cases`, `generate-knowledge-page`). Never write these documents anywhere else (not to the user's home directory, Desktop, or another project).

## Step 0 — Determine mode: create or update

Ask (or infer from the user's request) whether this is:
- **Create**: no existing analysis document for this feature yet.
- **Update**: an analysis document already exists and needs to be revised.

If the user references an existing `outputs/feature-*/*-feature-analysis.md` file, or one is otherwise supplied/linked, treat it as **Update**. Otherwise treat it as **Create**.

## Create mode

1. **Get the feature name** (this is the primary key for this run — used for the title and filename) and, separately, **the project code** if not already known (used only to locate the related PRD). **Check for a related PRD.** If a project code is given (or inferable), check whether `outputs/<project-code>-PRD.md` exists in this project. If it does, read it for context:
   - Feature scope and target users → helps ground as-is interview questions.
   - Key Features/Capabilities Overview → helps ground to-be interview questions.
   Do not copy or restate PRD content into this document — use it only to ask better-informed interview questions.

2. **Interview-first, as-is before to-be.** This information usually lives in stakeholders' heads, not documents, so lead with structured questions rather than waiting for source material:
   - **As-is first:**
     - Process Overview/Scope → "What triggers this process, and what marks it as complete?"
     - Stakeholders/Roles → "Who's involved, and what does each do?"
     - Process Description → "Walk me through the steps as they happen today, in order."
     - Business Rules → "What rules, validations, or exceptions actually apply today — not what's officially documented, but what people actually do?"
     - User Journey → "From the end user's point of view, what do they experience at each stage?"
     - Systems Involved → "What systems or tools are used at each step?"
     - Pain Points → "Where does this break down or frustrate people? Root cause if known?"
   - **Then to-be**, grounded in the linked PRD's capabilities where available:
     - Process Description → "Once this feature exists, how should this process work instead?"
     - Business Rules → "Will any current rules change, get removed, or will new ones be introduced?"
     - User Journey → "What should the end user's experience look like instead?"

3. **Treat any supplied documents (SOPs, process docs, BRD/PRD mentions) as equal-priority supplements, not the primary source.** Use them to confirm or fill gaps in interview answers. Do not let a document silently override what a stakeholder said, or vice versa — if a document and an interview answer disagree (e.g., documented policy vs. actually-practiced rule, or a PRD capability vs. a stakeholder's stated to-be process), record the conflict verbatim under Open Questions, naming both sources.

4. **No fabrication, on either side.** Do not invent as-is steps/rules/systems that weren't confirmed. Do not invent or design to-be steps/rules — every to-be item must trace back to something a stakeholder actually said. Anything unconfirmed on either side goes to Open Questions instead of being filled in.

5. **Build the Gap Analysis table** by pairing as-is and to-be items the stakeholder described for the same step/rule, tagging each row New / Modified / Removed / Unchanged. Only fill in "Pain Point Addressed" when the stakeholder explicitly linked the to-be change to a pain point — do not infer that connection yourself.

6. **Build the Non-Functional Requirements section.** This section is feature-level and is the single source of truth other artifacts (use cases, user stories) will reference by NFR ID rather than duplicate — so it belongs here, not in those downstream documents. Propose NFR candidates inferred from this document's own As-Is: Current Performance Baseline and As-Is: Pain Points/Issues content, plus any relevant constraints from the linked PRD, each tagged with its source. Present the proposed list to the user for confirmation before finalizing — do not add an NFR silently. Interview directly for concrete targets/thresholds none of these sources specify (e.g., "any specific response-time or uptime requirement here?").

7. **Populate the Mermaid diagrams** (as-is process flowchart, as-is journey, to-be process flowchart, to-be journey) using only confirmed content — role-based subgraphs for the flowcharts, stage/satisfaction entries for the journeys. Omit or simplify a diagram rather than padding it with unconfirmed detail.

8. **Draft the document** following `templates/feature-analysis-template.md` exactly, in Markdown.

9. **Write the output** to `outputs/feature-<feature>/<feature>-feature-analysis.md`, using the feature name gathered in step 1 (create the `outputs/feature-<feature>/` folder if it doesn't exist). Set version `1.0` with a first Revision History row: "Initial draft" and an appropriate trigger/reason.

10. **Summarize for the user** (in chat, not in the document): what came from interview (as-is vs. to-be) vs. from supplied documents, the key gaps identified, which NFRs were inferred vs. interview-confirmed, and what's left as an open question.

## Update mode

1. **Locate the existing analysis document** by feature name, at `outputs/feature-<feature>/<feature>-feature-analysis.md`. Read its full current content and note its current version from the Revision History table.

2. **Gather what's driving the update** — re-interview on as-is and/or to-be as needed, incorporate newly supplied documents, or add/revise an NFR (including one raised by a downstream use case or user story that found a gap in this section). Apply the same equal-priority, flag-every-conflict rule, now also checking new input against the *existing document's* current content.

3. **Apply changes only to the affected sections**, including regenerating the relevant Mermaid diagram(s), Gap Analysis rows, or Non-Functional Requirements rows if the underlying content changed. A new or changed NFR still goes through the same propose-then-confirm step as in Create mode — never added silently. Leave unaffected sections untouched.

4. **Bump the version and log the change** in the Revision History table: increment the version (minor for small updates, major for a significant scope change — ask the user if unclear), with date, a plain-language description of what changed, and the trigger/reason.

5. **Write the updated file back** to the same `outputs/feature-<feature>/<feature>-feature-analysis.md` path.

6. **Summarize the delta for the user**: what changed, what stayed the same, and any new open questions the update raised.
