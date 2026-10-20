---
name: generate-use-cases
description: Create a new Use Case Specifications document or update an existing one, for a specific feature. A feature can involve multiple use cases (distinct actor-goal interactions); this skill identifies them from the feature's To-Be process, confirms the set with the user, and drafts each as a classic use case (actors, trigger, pre/postconditions, basic/alternate/exception flows). Use when the user asks to write/create/document use cases, use case specifications, or actor flows for a feature.
---

# Generate Use Cases

Produces or updates a use case specification document for a feature, building on the to-be process already captured by the `generate-feature-analysis` skill rather than re-deriving it from scratch. Sits after Feature Analysis and before detailed functional requirements/acceptance criteria (a later, separate artifact) in the artifact chain: BRD → PRD → Feature Analysis (as-is/to-be + gaps) → **Use Cases** → functional requirements.

The template lives at `templates/use-cases-template.md` in this project.

All output files are written inside this project, under `outputs/feature-<feature>/<feature>-use-cases.md` — named by **feature name**, not project code, since one project/project code can involve multiple features and this artifact is scoped per feature, and grouped in a folder alongside that feature's other artifacts (`generate-feature-analysis`, `generate-knowledge-page`).

## Step 0 — Determine mode: create or update

Ask (or infer from the user's request) whether this is:
- **Create**: no existing use case document for this feature yet.
- **Update**: a use case document already exists and needs to be revised (new use case, or a flow/condition change to an existing one).

If the user references an existing `outputs/feature-*/*-use-cases.md` file, or one is otherwise supplied/linked, treat it as **Update**. Otherwise treat it as **Create**.

## Create mode

1. **Check for linked source documents.** Ask for the project code to locate:
   - `outputs/feature-<feature>/<feature>-feature-analysis.md` — primary source for candidate use cases and each Basic Flow's backbone (the To-Be: Process Description section).
   - `outputs/<project-code>-PRD.md` — context only (feature intent), not a direct source of flow detail.
   These two source documents are keyed by project code; only this skill's own output filename is keyed by feature name. If the Feature Analysis document doesn't exist, fall back to a fully interview-first flow: ask the user directly what the use cases are, one at a time, and gather all flow detail through interview instead of step 2 below.

2. **Propose candidate use cases from the To-Be process.** Read the To-Be: Process Description and identify distinct actor-goal interactions (each place a specific actor accomplishes a specific goal is a candidate). Present the candidate list to the user — tentative ID, name, primary actor, one-line goal — and ask them to confirm, merge, split, rename, add to, or remove from it before drafting details.

3. **Draft each confirmed use case:**
   - **Basic Flow:** derive the step sequence from the relevant portion of the To-Be process, reworded into actor-action → system-response pairs. Interview to fill gaps where the source is too vague or incomplete for a proper step-by-step flow.
   - **Preconditions / Postconditions / Alternate Flows / Exception Flows:** interview-first — the To-Be process typically only describes the happy path. Ask, for each use case: "What must be true before this can start? What must be true once it succeeds? What could go differently at each step? What could fail, and what happens then?"
   - **Business Rules Referenced:** cross-check against the Feature Analysis's To-Be: Business Rules table and reference matching rules by name — do not restate rule text in this document. If a rule is needed for a flow/exception but isn't documented there, note it under Open Questions rather than inventing it.
   - **Related Use Cases:** ask whether this use case includes or extends any other confirmed use case in the same set.

4. **Multi-source handling — equal priority, flag every conflict.** If additional documents are supplied alongside the Feature Analysis (e.g. a revised process doc), treat them as equal priority — don't let one silently override another. Record any factual conflict verbatim under Open Questions, naming both sources.

5. **Draft the document** following `templates/use-cases-template.md` exactly: the Use Case Summary table, then one detail block per confirmed use case, in Markdown. Never omit or leave a field blank — write "Not applicable", or move an unresolved item to Open Questions. Tag each Open Question with its UC ID.

6. **Get the feature name** — use the linked Feature Analysis's "Feature / Process Name" field if available, otherwise ask. This name drives the output filename, not the project code.

7. **Write the output** to `outputs/feature-<feature>/<feature>-use-cases.md` (lowercase, hyphenated; trigger e.g. "Derived from To-Be process in Feature Analysis").

8. **Summarize for the user**, also covering which use cases came directly from the To-Be process vs. were added/adjusted by the user.

## Update mode

1. **Locate the existing document** at `outputs/feature-<feature>/<feature>-use-cases.md`. Read its full current content and note its current version from the Revision History table.

2. **Gather what's driving the update** — a new use case to add, an existing use case's flow/conditions to revise, or changes cascading from a revised Feature Analysis or PRD. Apply the same equal-priority, flag-every-conflict rule, now also checking new input against the *existing document's* current content.

3. **Apply changes** to the affected use case block(s) or Summary table rows.

4. **Bump the version** — adding/removing a use case counts as major — **and write back** to the same `outputs/feature-<feature>/<feature>-use-cases.md` path.

5. **Summarize the delta for the user:** what changed, what stayed the same, and any new Open Questions.