---
name: generate-test-cases
description: Formalize a single story's existing Gherkin acceptance criteria (from generate-user-stories) into a classified, prioritized, execution-ordered functional test suite — Positive/Alternative/Negative/Boundary scenario groups, P0/P1/P2 priority, full traceability, and a hard-stop confirmation gate before generating the full suite. One test file per story, written alongside it. Use when the user asks to generate/create functional test cases for a story.
---

# Generate Test Cases (one file per story)

Formalizes a single story's existing Gherkin Acceptance Criteria (written by `generate-user-stories`) into a classified, prioritized, execution-ordered functional test suite. This skill does not re-derive test content independently from the source Use Case's raw flows — the ACs already written on the story are the primary source; this skill's job is classification, scenario grouping, priority, traceability discipline, and execution ordering on top of them.

**Scope is one story, not a whole use case.** Each story file gets its own func-test file. Known tradeoff: this skill's execution-order optimization (Step 5) reasons only within this one story's own scenarios — it does not reuse test data or sequence across sibling stories of the same use case, since those may live in different files (and different sprint buckets) entirely.

**Adapted from the `func-test` skill pattern** (scenario groups, priority levels, traceability rules, execution-order optimization), but without a separate living checklist file — coverage analysis and quality checks are folded into inline self-verification steps here, consistent with every other skill in this project (one output artifact, no helper files).

The template lives at `templates/func-test-template.md` in this project.

The output is written to `outputs/<bucket>/US-<use-case-name>/<use-case-name>-func-test-0X.md` — right next to its source story file, in whichever sprint bucket that story currently lives in. Named `-func-test` specifically (not a generic `-tests`) since other test types (e.g. smoke tests) are tracked separately.

## Step 1 — Analyze & classify

1. Locate the source story file by globbing `outputs/*/US-<use-case-name>/<use-case-name>-US-0X.md` across all three sprint buckets. Read its "As a/I want/so that," Covers Flow(s), Gherkin Acceptance Criteria, Related NFRs, and Feature field (needed to locate the feature's Feature Analysis document for Boundary-case sourcing below). Note which bucket it's currently in — the func-test file is written alongside it, in the same bucket.
2. Classify the story as one of:
   - **`UI-related`** — change limited to presentation/layout with no logic or data impact; test focus is visual verification, layout, and user interaction.
   - **`Functionality-related`** — affects behavior/logic of a specific function, no data cleanup/migration risk; test focus is functional correctness, edge cases, and error handling.
   - **`Functionality+Data-related`** — affects behavior/logic and also touches stored data (e.g. removing/renaming an option, field, or state) such that leftover data, orphaned references, or migration must be verified; test focus adds explicit no-leftover-data and data-migration checks on top of the above.
3. List any ambiguities in the source ACs as clarification questions, and any assumptions you'd otherwise need to make as assumptions to confirm.

## Step 2 — Hard stop (confirmation gate)

Present the classification, its reasoning, and any ambiguities/assumptions from Step 1, and **stop** — do not generate the full test suite yet. If the user resolves them, proceed with the resolved answers. If the user proceeds without resolving something, record it verbatim as `[UNRESOLVED - user proceeded without clarification]` in Assumptions & Clarifications, and continue.

## Step 3 — Generate test cases from the existing ACs

1. **Map this story's Gherkin scenarios to scenario groups**, not re-derived independently from the use case's raw flows:
   - Happy-path scenario (from the Basic Flow) → **Positive**.
   - Valid-variation scenarios (from Alternate Flows) → **Alternative**.
   - Invalid-input/error scenarios (from Exception Flows) → **Negative**.
   - **Boundary** cases are proposed only where implied by a specific NFR (read `outputs/feature-<feature>/<feature>-feature-analysis.md`'s Non-Functional Requirements section, using the feature name noted in Step 1) or an explicit limit stated in an AC or business rule — cite the source (NFR ID or AC). If no source implies a boundary case for a given input/limit, do not invent one; note the gap in Open Questions instead.
2. **Assign priority** to each test case:
   - `P0` — critical path or blocker AC.
   - `P1` — important, non-blocker behavior.
   - `P2` — edge or low-impact coverage.
3. **Assign a Test ID** as `<Scenario>-<Sequential Number>` (e.g. `POS-1`, `ALT-2`, `NEG-3`, `BND-4`), sequential within each scenario group.

## Step 4 — Apply traceability rules

- `Given` must be derivable from the source story or its AC only.
- `When` must map to a user action/event stated or directly implied by that AC.
- `Then` must map to an outcome stated in the story or AC.
- Do not add unstated UI details, and do not infer behavior from other features or conventions.
- Untraceable content must go into that test case's Assumptions field as `[ASSUMPTION - not stated in AC]` — never into Given/When/Then.
- If one AC/scenario is split into multiple test cases, each test case references only the portion of it that it covers.

## Step 5 — Apply execution-order optimization

- Order test cases for practical execution flow, not just by priority (priorities themselves stay unchanged; only the run order/numbering reflects this).
- Place non-destructive or cancel/rollback validations before destructive/finalizing validations within this story's flow.
- Prefer sequences that let one test-data record be reused across consecutive cases within this story.
- If a destructive step removes or archives data (e.g., a confirmed delete), run cancellation/back-path tests first when they share the same entry state.
- When an AC defines multiple mutually-exclusive terminal outcomes for the same entity (e.g., approve vs. deny vs. cancel vs. expire on one request), order them from least state-mutating/cheapest-to-reset to most: an outcome that grants/creates a persistent artifact (e.g., an approval granting access) is sequenced last among the terminal cases, since it needs an explicit rollback before the entry is reusable; outcomes that leave no artifact (deny, cancel, expire) run first.
- If reusing one test-data record across terminal-outcome cases would force a rollback step not stated in any AC, generate a fresh Given/entry per case instead and note it, rather than chaining through a state-mutating outcome.

## Step 6 — Inline coverage analysis

Validate coverage against: happy path and alternative flows, all of this story's acceptance criteria, boundary conditions, invalid input handling, error conditions, data validation, permission/authorization (cross-checked against `outputs/rbac.md` for this story's actor — a role-based access denial scenario should exist if RBAC restricts something relevant here), and state transitions. Record the result in the Coverage Notes section — no separate checklist file; this is a step within this run, not a persisted artifact.

## Step 7 — Inline quality self-check

Before finalizing, confirm: every test case has a traceable source reference; no Given/When/Then contains fabricated/untraceable content; every test case has a priority; execution order has been applied; Step 6's coverage analysis is complete. If something fails, revise internally rather than presenting an incomplete draft.

## Step 8 — Draft and write the output

1. Draft the document following `templates/func-test-template.md` exactly — Classification & Scope, Assumptions & Clarifications, Test Case Summary (counts per scenario group × priority), Test Cases (in execution order), Coverage Notes, Open Questions.
2. Write to `outputs/<bucket>/US-<use-case-name>/<use-case-name>-func-test-0X.md`, using the same `<bucket>` and story number `0X` as the source story file.
3. **Summarize for the user**, also covering classification, test case counts per scenario group/priority, and what's traceable vs. flagged as an assumption.
