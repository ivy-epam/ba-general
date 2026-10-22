---
name: generate-prd
description: Create a new Product Requirements Document (PRD) or update an existing one, built from a BRD and/or other supplementary source material (Confluence pages, SharePoint/OneDrive files, local files), or purely from conversation when no source documents exist. Covers problem statement, product vision with OKRs and a North Star Metric, actors and end users, user journeys with pain points, scope with prioritized key features, roadmap, product-level risk register, decision notes, and open questions. Use when the user asks to create/draft/generate a PRD, write a PRD from existing files, or update/revise an existing PRD.
---

# Generate PRD

Produces or updates a PRD at the **product/capability level** — not a functional spec. Functional requirements, user stories, NFRs, data/integration specs, acceptance criteria, and traceability matrices belong in later artifacts; where sources go that deep, summarize up to capability level.

- Template: `templates/prd-template.md`
- Output: `outputs/<project-code>-PRD.md`

**Domain analysis** (`outputs/*-<project-code>-domain-analysis.md`), if it exists: Part 1 explains the domain; Part 2 is a provisional, high-level product model. The PRD holds the product detail and is cross-checked against Part 2. Never edit the domain analysis or rebuild its entity model here — corrections go through `generate-domain-analysis` update mode.

## Step 0 — Determine mode: create or update

Ask (or infer from the user's request) whether this is:
- **Create**: a new PRD, no existing PRD file yet.
- **Update**: an existing PRD file already exists and needs to be revised.

If the user references an existing `outputs/*-PRD.md` file, or an existing PRD is otherwise supplied/linked, treat it as **Update**. Otherwise treat it as **Create**.

## Create mode

1. **Gather sources** — ask what's available: a BRD, supplementary files (notes, research, specs, emails), or nothing (conversation only). Fetch each by type:
   - Local file → `Read`, or the `docx`/`pdf` skills.
   - Confluence → Atlassian Rovo MCP tools (e.g. `getConfluencePage`).
   - SharePoint/OneDrive → the `msgraph` skill.

   Also read this project's domain analysis, if any: Part 1 to ask better-informed questions (don't restate it), Part 2's entity names for consistent vocabulary, and point the Glossary to it rather than copying domain terms.

2. **Flag every conflict.** All sources, the domain analysis included, carry equal weight. Where two disagree, don't pick one — record it as an Open Question naming both sources and what each says. Compare against the domain analysis's Part 2 using the alignment map in `generate-domain-analysis` (Step 2.2).

3. **Interview for gaps** — only for sections no source covers:
   - Problem Statement → "What is the ultimate problem this product exists to solve, and why now?"
   - User Journeys → "Walk me through the user's experience end to end, including outside the product: what starts it, what stages and touchpoints follow, and what goes wrong at each — for which role?"
   - Vision & Objectives → "What's the vision? What single metric best shows the product delivers value? What objectives and measurable key results is it accountable for?"
   - Actors & End Users → "Who uses the product directly? Who supports, approves, or is consulted? Who ultimately benefits?"
   - Scope & Key Features → "What should the product be able to do, at a high level? What's out of scope?" If no source gives feature priorities, ask the user to choose one or two Implementation Prioritisation methods from `references/prioritisation-methods.md` (always the current file) — offer RICE, MoSCoW and WSJF by name, each with its "Best for" line — or to state P0–P3 directly. Then gather each method's inputs per feature.
   - Roadmap → "What are the phases, timeframes, and what marks each phase done?"
   - Risk Register → "What could put the product's outcomes, adoption, or delivery at risk?"
   - Assumptions/Constraints/Dependencies → "Any known assumptions, constraints, or dependencies on other teams or systems?"
   - Decision Notes → "Any product decisions already made, and by whom?"

4. **Confirmation gate (hard stop).** Present everything derived rather than lifted from a source — North Star Metric and OKRs, actor types, journey stages, pain points, feature breakdown and priorities, feature-to-phase mapping, risks and severity — each tagged with its source. Wait for the user to confirm, correct, or remove each.

5. **Draft** to the `templates/prd-template.md` structure, applying the drafting rules below.

6. **Project code and product name** — reuse the domain analysis's, else take them from the sources (e.g. a Jira key), else ask. Both appear in the title; the project code also sets the filename.

7. **Write** to `outputs/<project-code>-PRD.md` (trigger e.g. "Created from BRD", "Created from conversational input").

8. **Summarize** for a sanity check before it goes to the PO. If a domain analysis exists, add a **Domain analysis alignment** list — each mismatch with Part 2, and any new product concept Part 2 lacks — and recommend running `generate-domain-analysis` in update mode with the PRD as trigger.

## Drafting rules

- **Problem Statement & Business Context:** the ultimate, high-level problem — the root issue behind the journey pain points — and its cost. No solution, no list of pain points.
- **User Journeys:**
  - The user's whole experience, in their terms: how it starts, each stage, and every touchpoint, including those outside the product. Never mention the product or its features.
  - One journey per distinct end-to-end experience, for a named actor or end user; typically 3–8 stages, one row per touchpoint.
  - Pain points: one row per role per touchpoint, only where a pain point is known; touchpoints match the journey table, roles match Actors & End Users. Sourced only — never inferred from the product.
  - Experience level only; step-by-step flows and root causes belong in the feature analysis.
  - Never link pain points to features here. Each feature analysis records the pain points its feature addresses and validates them against this list.
- **Product Vision & Objectives:**
  - Vision: one sentence on the outcome for end users.
  - One North Star Metric capturing value to end users (revenue or activity counts only if a source frames them so).
  - OKRs: qualitative objectives, 2–4 measurable key results each; flag in the summary any key result that wouldn't move the North Star Metric.
- **Actors & End Users:**
  - **Primary** uses the product for their own goal; **Secondary** supports, approves, or is consulted; **End user** is the ultimate beneficiary, whether or not they touch the product.
  - Roles, not individuals; external systems go under Dependencies.
  - Use / Interaction says concretely what each does with the product — for an indirect end user, how the outcome reaches them (e.g. through staff, or a statement the product produces).
- **Product Scope & Key Features:**
  - One row per capability-level feature, IDs `F-01`, `F-02`, …, with a one-sentence description of what it lets users do. Out of scope only where a source or the user excludes it.
  - Group by priority (P0–P3). Omit empty groups.
  - **Method-based priorities:** score each feature with each chosen method and map the result to P0–P3 as the reference defines. Inputs (reach, effort, value, category, …) come only from sources or the user; a feature with unknown inputs goes under P3 as "(priority TBD)" with an Open Question. At the confirmation gate, show both methods' results side by side (inputs, calculation, score, mapped priority) and ask the user which one method to apply; its priorities set the grouping for all features — no feature-by-feature mixing.
  - Fill the method line (methods used, applied method) and one result column per chosen method, each showing calculation → score → priority, plus Effort (RICE) or Job Size (WSJF) for eye-checking — these never change the priority. With a single method, drop the second column; with priorities stated directly, drop both and write "Stated directly".
  - A P0 feature belongs in the first phase; record any priority–roadmap mismatch as an Open Question.
- **Roadmap:** each feature in exactly one phase; phase names and timeframes as sourced, else "TBD" plus an Open Question.
- **Risk Register — product level only:**
  - Only risks to the product's objectives, adoption, viability, delivery, or compliance. Roll feature- or task-level risks up if they threaten an objective; otherwise omit them and mention them in the summary.
  - Severity per the template legend; Impact names the affected objective or North Star Metric where possible.
  - Mitigation and owner as sourced — never assign an owner; else "TBD" plus an Open Question.
- **Decision Notes:** only decisions actually made, with rationale and decision-maker if known — recommendations and open options are Open Questions.
- **Open Questions:** for a source conflict, name both sources and what each says.
- **IDs:** `F-`, `R-`, `D-`, `OQ-` numbered `01`, `02`, …; never renumber — reprioritized features keep theirs, new items take the next number.

## Update mode

1. **Locate the existing PRD.** Read its full current content and note its current version number from the Revision History table.

2. **Gather what's driving the update**, using the same flexible input handling as Create mode (a revised BRD, new supplementary files, or a conversational description of the change). Apply the same equal-priority, flag-every-conflict rule — now also checking new input against the *existing PRD's* current content, not just against other new sources.

3. **Run the confirmation gate** (Create mode step 4) for any newly derived content. New or reprioritised features are scored with the method(s) recorded in the PRD and use its applied method, unless the user chooses different methods — then rescore every feature so the grouping stays consistent.

4. **Apply changes, bump the version, and write back** to the same `outputs/<project-code>-PRD.md` path. When an Open Question is answered with a decision, remove it from Open Questions and record it in Decision Notes, ending the decision text with the question it resolves (e.g. "(resolves OQ-03)").

5. **Summarize the delta for the user:** what changed, what stayed the same, and any new Open Questions — plus the Domain analysis alignment list, as in Create mode.
