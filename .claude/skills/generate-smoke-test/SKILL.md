---
name: generate-smoke-test
description: Create or update the product's cumulative smoke test suite for build-stability verification (not exhaustive testing). Applies production-safety rules since these tests run against production. Use when the user asks to create/update smoke tests, or review smoke test coverage/scope.
---

# Generate Smoke Test

Maintains a **single, cumulative, product-wide** smoke test suite, organised by module. It is built from scratch on the first run (Creation mode) and updated in place on later runs as features are added or changed (Modification mode) — see Step 0.

The templates live at `templates/smoke-test-scope-analysis-template.md` (scope analysis) and `templates/smoke-test-template.md` (suite) in this project.

All outputs live in `outputs/smoke-tests/`:
- `scope-analysis.md` — application context, modules, their use cases, and statuses (Steps 1–2).
- `smoke-tests.md` — use case priorities and the smoke test suite itself (Step 7).

Both outputs are organised by **module**. **Features** only matter as the trigger for change in Modification mode: each new or changed feature is rolled up to its module (see *Key concepts* in `README.md`).

**Statuses** — used for modules, use cases, and test cases alike: `New`, `Updated`, `Unchanged` (carried forward as-is), `Deprecated` (retired). Deprecated use cases stay listed in the scope analysis, not deleted, so retirement is traceable.

## Step 0 — Identify mode

Check which files exist in `outputs/smoke-tests/`:
- **Neither → Creation mode.** The user provides modules only; every module is `New` and the suite is built from scratch.
- **Only `scope-analysis.md` → interrupted Creation run.** A previous run stopped before writing the suite. Offer to resume from Step 3 using the existing scope analysis (re-confirming it at Step 2 if its Status isn't `Confirmed`), or to start over. Never overwrite it without asking.
- **`smoke-tests.md` exists → Modification mode.** Read it first — its Module Status & Coverage table is the baseline — then ask which features are new or changed.

Tell the user which mode applies before starting scope analysis.

## Step 1 — Scope analysis

### Creation mode

1. Ask the user for:
   - Application business nature
   - Read/write balance
   - Primary end user intent
   - Compliance concerns
   - Module list, and the use cases of each module
2. Work at module level only — features are not assigned to modules in this mode. Supplement the user's answers with sources where available:
   - `outputs/<project-code>-PRD.md` — product context.
   - `outputs/feature-*/*-feature-analysis.md` — a feature is a flow of use cases, so its To-Be process helps ground each use case's Primary Actor and Primary Flow.
   - `outputs/rbac.md` — authorization-sensitive flows.
3. **Propose the details the later steps need**, grounded in the user's answers and sources, for the user to confirm or correct at Step 2:
   - Per module: Main Usage Patterns and Module Criticality (Low / Medium / High, with a rationale based on usage frequency, write behaviour — writes that change data or affect other users — and the importance of the data handled).
   - Per use case: Primary Actor and Primary Flow (`Step → Step → Step`).
   Where nothing supports a proposal, ask instead of guessing.
4. **Assess each module's use cases** and propose modifications where needed, each with its rationale — e.g. a critical flow that seems missing, use cases that overlap and could merge, one too broad to test as a single flow, or one that isn't smoke-worthy (rarely used, low criticality). If no modification is needed, say so. These proposals are confirmed at Step 2.
5. Write `outputs/smoke-tests/scope-analysis.md` (Status: `Draft`) using `templates/smoke-test-scope-analysis-template.md`, with the user's use cases as given. Group use cases under their module, with IDs numbered per module (`UC-01`, `UC-02`, …) — a use case is always referenced together with its module (e.g. `Homepage / UC-02`). Every module and use case is `New`.

### Modification mode

1. Read `outputs/smoke-tests/scope-analysis.md` and the Module Status & Coverage table in `outputs/smoke-tests/smoke-tests.md`.
2. Ask which features are new or changed, and ask the user to confirm which module each belongs to — an existing module from `scope-analysis.md`, or a new module the feature introduces. Do not assign a feature to a module yourself. Then read each feature's PRD, Feature Analysis, Use Cases, and RBAC entries.
3. **Compare each feature's use cases against its module's existing use cases** and propose, with rationale:
   - **New** use cases to add (next module UC ID), with Primary Actor and Primary Flow taken from the feature's Use Cases document.
   - **Updated** use cases whose flow changed.
   - **Deprecated** use cases the feature removes or replaces — their smoke tests will be retired.
   Everything else in the module stays `Unchanged`.
4. Set each module's status this run: `New` (not previously in the table), `Updated` (any of its use cases is New, Updated, or Deprecated), `Unchanged`, or `Deprecated` (explicitly retired by the user).
5. Update `outputs/smoke-tests/scope-analysis.md` (Status: `Draft`) with the proposed statuses, the features assigned to each module, and the proposed use case changes, and add a Revision History row.

### Rules

- Step 1 is context analysis only.
- If details are unclear, ask the user to confirm assumptions or clarify. Record confirmed scope decisions in that module's **Scope Notes** so later runs respect them.

## Step 2 — Hard stop (scope confirmation)

Ask the user to review `outputs/smoke-tests/scope-analysis.md`, and present: the module list with statuses, the proposed details and use case modifications from Step 1 (with rationale), carry-forward modules kept unchanged, and deprecations that require retiring smoke tests. **Stop and wait for explicit confirmation.** Apply only what the user confirms, revise and ask again if they request changes, then set the scope analysis Status to `Confirmed`. Do not proceed to prioritization on an unconfirmed scope.

## Step 3 — Prioritization

### Creation mode

1. Take each module's confirmed use cases from `outputs/smoke-tests/scope-analysis.md` as smoke-test candidates.
2. Read `references/use-case-prioritisation-matrix.md` and prioritise each use case using its **Use Case Prioritisation Matrix** — always read the current file for the dimensions, weights, and thresholds rather than applying them from memory, in case it has been edited.
3. Score each dimension with a one-line rationale grounded in the confirmed scope analysis (compliance concerns, usage patterns, module criticality). Where the scope analysis doesn't support a score, ask the user.
4. Present the filled-in matrix table (per the reference doc's Matrix Table Template), one table per module. `P0`/`P1` use cases become smoke-test candidates; `P2` use cases get no smoke tests.

### Modification mode

1. For each New or Updated use case, glob `outputs/*/US-<use-case-name>/<use-case-name>-func-test-*.md` (produced by `generate-test-cases`) across all three sprint buckets — a use case's stories, and their test files, may be split across buckets — and pull only `P0`/`P1` test cases as smoke-test candidates, ignoring `P2`.
2. If a story has no func-test file yet, flag it as a gap: offer to run `generate-test-cases` for it first, or — if the user prefers not to — interview directly for a minimal P0 happy-path candidate, noting the shortcut taken.
3. Propose each New or Updated use case's priority as the highest priority among its P0/P1 func-test cases (`P2` if it has none). In the priority table, its matrix columns (Compliance → Score) read "—" and Priority Basis is "func-test".
4. **Re-check the affected module's Unchanged use cases**: if the change makes one less (or more) critical — e.g. a new use case supersedes it as the main path — propose a priority change with rationale.
5. Deprecated use cases have all their smoke tests marked `Deprecated`.

## Step 4 — Hard stop (prioritization confirmation)

Present each use case's proposed priority, grouped by module (Creation mode: with the prioritisation matrix scores from Step 3, so the user can adjust any dimension score; Modification mode: including any proposed priority changes to Unchanged use cases). For every carry-forward module, explicitly confirm whether its underlying behavior changed enough to require regenerating its smoke flows (a module can be `Unchanged` at the scope level but still need its smoke flow revisited if a use case detail shifted). **Stop and wait for confirmation** before generating the full test cases. The confirmed priorities are recorded in `smoke-tests.md` in Step 7.

## Step 5 — Generate smoke test cases

Apply these rules, since these tests run against production:
1. **P0/P1 only.** If no P0/P1 candidates remain after Step 4, stop and say so plainly rather than generating anything.
2. **Happy flow and critical parallel alternatives only** — smoke tests are build-stability checks, not exhaustive coverage. Pull the happy-path (Positive) scenario from the source func-test case (Creation mode: from the use case's confirmed Primary Flow), and at most one critical Alternative if it represents a genuinely critical parallel path.
3. **Keep only non-obvious, test-specific preconditions**; omit universal test-environment assumptions.
4. **No shared-data writes:** exclude any candidate whose write is visible to or affects another real user or role (e.g. submitting a request someone must act on) — even with a rollback step. Exception: a write whose only other party is a dedicated, team-owned test/QA account (not a real colleague) is in scope, since no real user's data or visibility is affected; it requires a cleanup step that reverses it (e.g. sharing or assigning an item to the test account, then removing it).
5. **Self-scoped writes OK:** a write that only affects the test user's own state, isn't visible to others, and triggers no notification (e.g. saving a preference or bookmarking an item) is allowed if paired with a rollback/cleanup step. Read-only actions (view, search, filter, preview, navigate) are always fine.
6. **No notifications:** exclude any candidate that sends a notification, message, or approval request to a real user, whether as the main action or a side effect. Exception: notifications from a Rule 4 test-account write are in scope when delivered only to that test/QA account.
7. **Traceability of exclusions:** a candidate excluded solely by Rules 4 or 6 must be listed in the Out of Scope section with the specific reason — never silently dropped.
8. **Assign Test IDs** as `<Module>-<UC-ID>-ST-00X`, using the module use case ID from `scope-analysis.md`. The Source field references that module use case and, in Modification mode, also the feature use case and its originating func-test Test ID (e.g., "checkout UC-02, POS-1") for traceability.

## Step 6 — Pre-output validation

Check every item before writing. If one fails, fix it and re-check — never write or present a draft that fails any item. This is a step within the run, not a separate checklist file.

1. **Confirmed inputs** — the scope analysis is `Confirmed` (Step 2), and every module use case has a priority confirmed at Step 4.
2. **Coverage** — every P0/P1 use case has smoke tests or an Out of Scope entry with its reason; no P2 or Deprecated use case has active tests.
3. **Minimal flows** — each P0/P1 use case has one happy-path test, plus at most one critical parallel alternative; no negative or boundary tests. Each test validates one critical workflow and runs independently of the others.
4. **Production safety** — Step 5 Rules 4–6 hold for every test; every write has a cleanup step; safety-only exclusions are listed in Out of Scope.
5. **Traceability** — every Given/When/Then traces to the source use case or func-test case, the Source field is filled, and nothing is vague or invented.
6. **Iteration integrity** — every module, use case, and test case carries a status (`New` / `Updated` / `Unchanged` / `Deprecated`); Unchanged tests are untouched unless Step 4 confirmed otherwise; Deprecated tests are removed from the active suite.
7. **Consistency** — Test IDs are unique and follow `<Module>-<UC-ID>-ST-00X`; P0/P1 counts in Module Status & Coverage match the test cases; the Revision History row lists added/updated/deprecated Test IDs; the output follows the template.

## Step 7 — Write/update the output

1. Update `outputs/smoke-tests/smoke-tests.md` (create it, using `templates/smoke-test-template.md`, if this is the first run):
   - Update the Module Status & Coverage table for every in-scope module (status, P0/P1 counts, Last Reviewed).
   - Update the Use Case Priorities & Smoke Test Cases section, grouped by module. Each module has one consolidated priority table listing **all** its active use cases with confirmed priority, priority basis, and rationale (plus matrix scores in Creation mode). Below the table, only `P0`/`P1` use cases get a details block (description, primary actor, primary flow) with their test cases beneath. Add new cases, revise updated ones, remove deprecated ones — this section always reflects the current full suite, not just this run's delta.
   - Update Out of Scope cumulatively (add this run's exclusions; don't remove prior ones unless the excluded item no longer exists).
2. Bump the version; the Revision History row logs the module(s) affected, the feature(s) that triggered the change (Modification mode), and the iteration delta (added/updated/deprecated Test IDs) — this is where the delta lives, not a separate section.

## Step 8 — Summarize

Also cover: in-scope modules and their status, P0/P1 counts, what was added/updated/deprecated this run, what's newly Out of Scope and why, and (Modification mode) any use case still missing a func-test file.
