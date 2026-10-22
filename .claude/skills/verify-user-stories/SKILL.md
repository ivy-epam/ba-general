---
name: verify-user-stories
description: Independently review one or more user story files (outputs/features/<feature>/user-stories/<UC-ID>/<UC-ID>-<short-title>.md) against a fixed quality checklist — INVEST criteria, Gherkin AC quality, traceability/sourcing, cross-story consistency with other existing story files, and change-impact analysis when re-reviewing a previously-verified story that's since been edited. The review always runs in a fresh, isolated subagent session (and a different model than the current session, when more than one is available) so the writer is never also the reviewer. Reports findings in chat only, and — only after the user explicitly confirms — logs Verification Status into the story file. Use when the user asks to verify, review, or QA a user story, or check whether stories are ready/verified.
---

# Verify User Stories

Independently reviews one or more individual story files against a fixed checklist, and — only once the user explicitly confirms — records verification status directly in each. This skill does not write requirements; it judges ones already written by `generate-user-stories`.

**The independence requirement is the whole point of this skill.** The review must happen in a session that did not write the content, so it never reasons from "I know what I intended" — only from what the document actually says. Never perform the review inline in the current conversation. Always spawn a separate subagent for it (see Step 2), even if that means the only difference from the current session is a fresh context.

**This skill never edits story content.** It only ever writes: (a) a story's Verification Status field, and (b) a Revision History row recording that verification or a status reset from impact analysis — both only after the user's explicit go-ahead. Findings stay in chat. If a story has issues, direct the user to `generate-user-stories` (Update mode) to fix them, then re-run this skill.

**Logging verification is not a content change.** Writing a Verification Status or a reset does not bump the story's version: the status records the version that was reviewed, and the Revision History row keeps that version. If the latest row already has today's date, fold the note into it instead of adding a row.

## Step 1 — Identify what to review

1. Ask for (or infer) the feature, use case, and story/stories, and locate the target story file(s) in `outputs/features/<feature>/user-stories/<UC-ID>/`. Read each, including its current Verification Status.
2. For each story, determine whether it needs a **standard review** (never verified) or a **change-impact review** (previously verified, then its Verification Status was reset because its content changed — shown in its Revision History). A story that is `Verified` for its current version needs no review unless the user asks for one.
3. Ask the user which stories to review now if not obvious (e.g., "just the ones that changed," or "all of them").
4. Find the other existing story files for the cross-story checks (glob, excluding `*-func-test.md`):
   - **Same feature:** `outputs/features/<feature>/user-stories/*/*.md` — checked against every cross-story criterion.
   - **Other features:** `outputs/features/*/user-stories/*/*.md` — checked only for role and terminology consistency (criteria 21–22).

## Step 2 — Spawn an independent reviewer

1. **Session isolation (mandatory):** use the Agent tool to spawn a fresh general-purpose subagent for the review — not `ba-agent`, which writes the stories. A fresh session guarantees the reviewer has no memory of how the document was written, regardless of model.
2. **Model separation (when possible):** check which model is running the current session. If more than one model is available in this environment, explicitly set the subagent's `model` parameter to a different one (e.g., current session is Sonnet → request Opus for the review; current session is Opus → request Sonnet). If only one model is available, proceed with session isolation alone — that still satisfies the independence requirement.
3. **Prompt the subagent** with a self-contained brief (it has no context from this conversation) that:
   - States its role: an independent QA reviewer of a BA user-story document, with explicit instruction not to assume good faith or fill in gaps charitably — judge only what's on the page.
   - Gives it file paths to read itself (do not paste full content into the prompt):
     - The target story file(s) from Step 1.1.
     - The source use case in `outputs/features/<feature>/<feature>-use-cases.md`.
     - `outputs/features/<feature>/<feature>-feature-analysis.md` (for NFR ID validation).
     - `outputs/rbac.md` (for role validation).
     - The other story files found in Step 1.4, split into same-feature and other-feature lists.
   - Names exactly which stories are in scope for this run, and which of those (if any) are change-impact reviews — flagging that criteria 24–26 apply specifically to those.
   - Gives it the full checklist below, grouped by category.
   - Requests a structured report: per story, pass/fail per relevant criterion, specifics for any failure, a suggested fix, and — for change-impact reviews — any other story/document whose correctness may now be affected. Ends with an overall recommendation per story (ready to verify / needs revision).

### Review checklist

**Story-level (INVEST + clarity)**
1. Independent — understandable/valuable on its own; any real dependency is stated explicitly.
2. Negotiable — describes what/why, not a rigid technical how.
3. Valuable — the "so that" clause states genuine, specific value, not filler.
4. Estimable — enough detail that a dev team could size it.
5. Small — one coherent capability, not secretly bundling multiple unrelated goals.
6. Testable — has at least one concrete, verifiable acceptance criterion.

**Identity & role**
7. The UC ID in the title matches the `<UC-ID>` folder the file sits in, and the use case name matches the source use case.
8. The "As a `<role>`" is the source use case's primary actor.
9. That role matches an existing entry in `outputs/rbac.md`'s Roles Inventory where that file exists; a mismatch is a finding, not silently ignored.

**Acceptance Criteria (Gherkin) quality**
10. Given/When/Then is unambiguous — no vague terms ("works correctly," "as expected") without a concrete, observable outcome.
11. A happy-path scenario is present and matches the source use case's Basic Flow.
12. Relevant Alternate/Exception flows from the source use case appear as additional scenarios, or their omission is clearly justified.
13. Business rules the source use case references are reflected in the relevant scenarios.
14. ACs describe observable behavior/outcome, not implementation mechanics.

**Priority**
15. The headline Priority matches the applied method's mapped priority, and exactly one method row is marked applied.
16. Each method's inputs are stated, not blank or unexplained.
17. A `TBD` priority has a matching Open Question.

**Traceability & sourcing discipline**
18. This story's "Covers Flow(s)" reference actually exists in the cited use case.
19. Its "Related NFR" ID actually exists in `outputs/features/<feature>/<feature>-feature-analysis.md`'s NFR section — no dangling/invented IDs.
20. Any AC introducing a flow/condition not traceable to the source use case is flagged for the user to confirm its source.

**Cross-story consistency**
21. *(Same feature and other features)* This story's role/permission assumptions are consistent with how that role is treated in other existing stories.
22. *(Same feature and other features)* Terminology (role/feature names) stays consistent with upstream documents and other stories.
23. *(Same feature only)* No contradiction between this story's scenarios/assumptions and any other story's, and no unflagged duplication/overlap with a story covering the same behavior — surface overlap as a finding, not necessarily an error.

**Change impact analysis (only for stories flagged in Step 1.2 as change-impact reviews)**
24. Read the story's Revision History to identify what the most recent logged change actually was — the diff signal, since there's no version control to diff against directly.
25. Based on that specific change, identify any other story file whose own correctness assumed the *old* behavior, and flag it as needing re-verification.
26. Check whether the change affects the RBAC matrix, the source Use Case/Feature Analysis (a flow or NFR that no longer matches), the story's own `-func-test.md` file, or the smoke test suite — flag each as a follow-up rather than ignoring the drift.

## Step 3 — Relay findings

Present the subagent's report to the user in chat, organized per story. No file is written at this point — this is a report, not a commitment.

## Step 4 — Get confirmation, then log verification

1. Ask the user which stories (if any) to mark `Verified` now, and — if impact analysis flagged other stories (criterion 25) — whether to reset those to `Not Verified`. A clean report does not auto-verify anything — this confirmation step is always required.
2. For each confirmed story, update its file directly (this skill does this, not the reviewer subagent):
   - Set its Verification Status field to `Verified — v{{version reviewed}}, {{today's date}}, reviewed by {{reviewer model used}}`.
   - Add a Revision History row noting the verification.
3. Stories with unresolved findings stay `Not Verified`; their findings stay in chat.
4. For each confirmed reset, set that story's Verification Status to `Not Verified`, with a Revision History row explaining why (e.g., "flagged by impact analysis of `<changed story>`").

## Step 5 — Summarize

Tell the user: what passed, what didn't, what's now marked verified, what's still open, and — for any story reset by impact analysis — which one and why. Remind them that fixing a finding means rerunning `generate-user-stories` (Update mode) and then this skill again.
