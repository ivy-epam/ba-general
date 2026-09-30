---
name: generate-smoke-test
description: Create or update the product's cumulative smoke test suite for build-stability verification (not exhaustive testing). Iteratively folds in P0/P1 coverage from each feature's use cases as they're added or changed, deriving scope/status from that feature's own PRD/Feature Analysis/Use Cases rather than a separate baseline file, and pulling priority from each use case's own func-test file rather than a separate prioritization matrix. Applies production-safety rules since these tests run against production. Use when the user asks to create/update smoke tests, or review smoke test coverage/scope.
---

# Generate Smoke Test

Maintains `outputs/smoke-tests.md` — a **single, cumulative, product-wide** smoke test suite, not a per-feature artifact (same pattern as `generate-rbac`'s `outputs/rbac.md`). Every time a feature is onboarded or changes, this skill reconciles that feature's status and P0/P1 coverage into the existing suite.

**Adapted from the `smoke-test` skill pattern** (module-level iterative scope, two-stage hard-stop workflow, production-safety rules, Out-of-Scope traceability), but without separate baseline/prioritization files — this project's own upstream artifacts (PRD, Feature Analysis, Use Cases, RBAC, and `generate-test-cases`' func-test files) supply what those files would have, and `outputs/smoke-tests.md`'s own Module Status section doubles as the baseline to reconcile against. Also unlike the original, this skill versions one evolving file with a Revision History changelog rather than creating a new dated snapshot file each run.

The template lives at `templates/smoke-test-template.md` in this project. Always read that file first to get the current section structure — do not hardcode the structure from memory, in case the template has been edited.

The output is always `outputs/smoke-tests.md` — never parameterized by feature or project code, and never written anywhere else (not the user's home directory, Desktop, or another project).

## Step 1 — Scope analysis

1. Ask which feature(s)/project code(s) are in scope for this run — a new feature to onboard, or an existing one that changed.
2. For each, read what's available: `outputs/<project-code>-PRD.md`, `outputs/feature-<feature>/<feature>-feature-analysis.md`, `outputs/feature-<feature>/<feature>-use-cases.md`, and `outputs/rbac.md` for context (business nature, module purpose, use cases, authorization-sensitive flows).
3. If `outputs/smoke-tests.md` already exists, read its Module (Feature) Status table and determine each in-scope feature's status this run: `New` (not previously in the table), `Updated` (in the table, but its source Feature Analysis/Use Cases changed since Last Reviewed), `Unchanged` (carry-forward, nothing material changed), or `Deprecated` (explicitly retired by the user). If the file doesn't exist yet, every in-scope feature is `New`.

## Step 2 — Hard stop (scope confirmation)

Present: the in-scope feature list with statuses, which features are being carried forward unchanged, and any deprecations/removals that require retiring their smoke tests. **Stop and wait for explicit confirmation** before continuing — do not proceed to prioritization on an unconfirmed scope.

## Step 3 — Prioritization

1. For each in-scope feature, find its use cases via `outputs/feature-<feature>/<feature>-use-cases.md`.
2. For each use case, glob `outputs/*/US-<use-case-name>/<use-case-name>-func-test-*.md` (produced by `generate-test-cases`) across all three sprint buckets — a use case's stories, and their test files, may be split across buckets — and pull only `P0`/`P1` test cases from each as smoke-test candidates, ignoring `P2`. This reuses priority already assigned in this chain rather than requiring a separate prioritization document.
3. If a story has no func-test file yet, flag it as a gap: offer to run `generate-test-cases` for it first, or — if the user prefers not to — interview directly for a minimal P0 happy-path candidate, noting the shortcut taken.
4. Tag each candidate with iteration status: `new`, `updated`, `carry-forward`, or `deprecated`, relative to what's already in `outputs/smoke-tests.md`.

## Step 4 — Hard stop (prioritization confirmation)

Present the prioritized candidate list. For every carry-forward feature specifically, explicitly confirm whether its underlying behavior changed enough to require regenerating its smoke flows (a feature can be "unchanged" at the scope level but still need its smoke flow revisited if a use case detail shifted). **Stop and wait for confirmation** before generating the full test cases.

## Step 5 — Generate smoke test cases

Apply these rules (carried over from the reference skill, since these run against production):
1. **P0/P1 only.** If no P0/P1 candidates exist after Step 3, stop and say so plainly rather than generating anything.
2. **Happy flow and critical parallel alternatives only** — smoke tests are build-stability checks, not exhaustive coverage. Pull the happy-path (Positive) scenario from the source func-test case, and at most one critical Alternative if it represents a genuinely critical parallel path.
3. **Keep only non-obvious, test-specific preconditions**; omit universal test-environment assumptions.
4. **No shared-data writes:** since these run against production, exclude any candidate whose write is visible to or affects another real user/role (e.g. an access request) — even with a rollback step. Exception: sharing an asset with a dedicated, team-owned test/QA account (not a real colleague) is in scope, since no real user's data or visibility is affected; requires a cleanup step that removes the share afterward.
5. **Self-scoped writes OK:** a write that only affects the test user's own state, isn't visible to others, and triggers no notification (e.g. favoriting) is allowed if paired with a rollback/cleanup step. Read-only actions (view, search, filter, preview, navigate) are always fine.
6. **No notifications:** exclude any candidate that triggers a notification or access request to a real user, whether as the main action or a side effect. Exception: the notification triggered by the Rule 4 sharing exception is in scope when delivered to the dedicated test/QA account.
7. **Traceability of exclusions:** a candidate excluded solely by Rules 4 or 6 must be listed in the Out of Scope section with the specific reason — never silently dropped.
8. **Assign Test IDs** as `<Feature>-<UC-ID>-ST-00X`, referencing the source use case and its originating func-test Test ID (e.g., "Source: UC-02, POS-1") for traceability.

## Step 6 — Inline coverage & quality self-check

Before finalizing (no separate checklist file — this is a step within the run, not a persisted artifact): every in-scope P0/P1 candidate is either represented in Smoke Test Cases or explicitly listed in Out of Scope with a reason; carry-forward features are correctly retained unchanged unless Step 4 confirmed otherwise; deprecated features' smoke tests are correctly removed from the active list; every safety rule from Step 5 has been applied.

## Step 7 — Write/update the output

1. Update `outputs/smoke-tests.md` (create it, using `templates/smoke-test-template.md`, if this is the first run):
   - Update the Module (Feature) Status table for every in-scope feature.
   - Update the Smoke Test Coverage Matrix (P0/P1 counts per feature).
   - Update the full current Smoke Test Cases list — add new cases, revise updated ones, remove deprecated ones. This section always reflects the current full suite, not just this run's delta.
   - Update Out of Scope cumulatively (add this run's exclusions; don't remove prior ones unless the excluded item no longer exists).
2. Bump the version and add a Revision History row logging which feature(s) drove this update and the iteration delta (added/updated/deprecated Test IDs) — this is where the delta lives, not a separate section.

## Step 8 — Summarize

Tell the user: in-scope features and their status, P0/P1 counts, what was added/updated/deprecated this run, what's newly Out of Scope and why, and what's left open (including any use case still missing a func-test file).
