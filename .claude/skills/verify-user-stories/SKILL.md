---
name: verify-user-stories
description: Independently review a single user story file (outputs/<bucket>/US-<use-case-name>/<use-case-name>-US-0X.md) against a fixed quality checklist — INVEST criteria, Gherkin AC quality, traceability/sourcing, cross-story consistency with every other existing story file across all use cases and sprint buckets, and change-impact analysis when re-reviewing a previously-verified story that's since been edited. The review always runs in a fresh, isolated subagent session (and a different model than the current session, when more than one is available) so the writer is never also the reviewer. Reports findings in chat only, and — only after the user explicitly confirms — logs Verification Status into the story file. Use when the user asks to verify, review, or QA a user story, or check whether stories are ready/verified.
---

# Verify User Stories

Independently reviews one or more individual story files against a fixed checklist, and — only once the user explicitly confirms — records verification status directly in each. This skill does not write requirements; it judges ones already written by `generate-user-stories`.

**The independence requirement is the whole point of this skill.** The review must happen in a session that did not write the content, so it never reasons from "I know what I intended" — only from what the document actually says. Never perform the review inline in the current conversation. Always spawn a separate subagent for it (see Step 2), even if that means the only difference from the current session is a fresh context.

**This skill never edits story content.** It only ever writes: (a) a story's Verification Status field, and (b) a Revision History row recording that verification (or a status reset from impact analysis) — both only after the user's explicit go-ahead. If a story has issues, direct the user to `generate-user-stories` (Update mode) to fix them, then re-run this skill.

## Step 1 — Identify what to review

1. Ask for (or infer) the use case name and story ID(s), and locate the target story file(s) by globbing `outputs/*/US-<use-case-name>/<use-case-name>-US-0X.md` across all three sprint buckets (a story's current bucket isn't assumed). Read each, including its current Verification Status.
2. For each story, determine whether it needs a **standard review** (never verified, or verified against an older version with no changes since) or a **change-impact review**: it was previously `Verified` but its Revision History shows a content change logged after that verification (including a reset already applied by `generate-user-stories`).
3. Ask the user which stories to review now if not obvious (e.g., "just the ones that changed," or "all of them").
4. Glob `outputs/*/US-*/*-US-*.md` to find every other existing story file — across every use case and every sprint bucket — in the project. These feed the cross-story consistency checks, regardless of which story is under review.

## Step 2 — Spawn an independent reviewer

1. **Session isolation (mandatory):** use the Agent tool to spawn a fresh subagent for the review. This alone guarantees the reviewer has no memory of how the document was written, regardless of model.
2. **Model separation (when possible):** check which model is running the current session. If more than one model is available in this environment, explicitly set the subagent's `model` parameter to a different one (e.g., current session is Sonnet → request Opus for the review; current session is Opus → request Sonnet). If only one model is available, proceed with session isolation alone — that still satisfies the independence requirement.
3. **Prompt the subagent** with a self-contained brief (it has no context from this conversation) that:
   - States its role: an independent QA reviewer of a BA user-story document, with explicit instruction not to assume good faith or fill in gaps charitably — judge only what's on the page.
   - Gives it file paths to read itself (do not paste full content into the prompt):
     - The target story file(s) from Step 1.1.
     - The source use case in `outputs/feature-<feature>/<feature>-use-cases.md`.
     - `outputs/feature-<feature>/<feature>-feature-analysis.md` (for NFR ID validation).
     - `outputs/rbac.md` (for role validation).
     - Every other story file found in Step 1.4 (for cross-story consistency).
   - Names exactly which stories are in scope for this run, and which of those (if any) are change-impact reviews — flagging that criteria 21–23 apply specifically to those.
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

**Role/Actor correctness**
7. The "As a `<role>`" matches an existing entry in `outputs/rbac.md`'s Roles Inventory where that file exists; a mismatch is a finding, not silently ignored.

**Acceptance Criteria (Gherkin) quality**
8. Given/When/Then is unambiguous — no vague terms ("works correctly," "as expected") without a concrete, observable outcome.
9. A happy-path scenario is present and matches the source use case's Basic Flow.
10. Relevant Alternate/Exception flows from the source use case appear as additional scenarios, or their omission is clearly justified.
11. No scenario contradicts another in this story or in a sibling story file from the same use case.
12. ACs describe observable behavior/outcome, not implementation mechanics.

**Traceability & sourcing discipline**
13. This story's "Covers Flow(s)" reference actually exists in the cited use case.
14. Its "Related NFR" ID actually exists in `outputs/feature-<feature>/<feature>-feature-analysis.md`'s NFR section — no dangling/invented IDs.
15. No AC appears to introduce a flow/condition absent from the source use case and not attributable to a stated interview answer.

**Cross-story consistency (checked against every other existing story file found in Step 1.4, across all use cases and buckets)**
16. No contradiction between this story's ACs/assumptions and any other existing story's ACs/assumptions.
17. No unflagged duplication/overlap with an existing story covering the same behavior — surface it as a finding, not necessarily an error.
18. This story's role/permission assumptions are consistent with how that role is treated in other existing stories.
19. Terminology (role/feature names) stays consistent with upstream documents and sibling stories.

**Change impact analysis (only for stories flagged in Step 1.2 as previously verified and since edited)**
20. Read the story's Revision History to identify what the most recent logged change actually was — the diff signal, since there's no version control to diff against directly.
21. Based on that specific change, identify any other story file — for this use case or another — whose own correctness assumed the *old* behavior, and flag it as needing re-verification.
22. Check whether the change affects the RBAC matrix or the source Use Case/Feature Analysis (a flow or NFR that no longer matches) — flag as a follow-up rather than ignoring the drift.

## Step 3 — Relay findings

Present the subagent's report to the user in chat, organized per story. No file is written at this point — this is a report, not a commitment.

## Step 4 — Get confirmation, then log verification

1. Ask the user which stories (if any) to mark `Verified` now. A clean report does not auto-verify anything — this confirmation step is always required.
2. For each confirmed story, update its file directly at its current path (this skill does this, not the reviewer subagent):
   - Set its Verification Status field to `Verified — v{{current document version}}, {{today's date}}, reviewed by {{reviewer model used}}`.
   - Add a Revision History row noting the verification.
3. For any story left with unresolved findings, keep it `Not Verified` and add its open issues to that story's own Open Questions section.
4. For any other story flagged by change-impact analysis (Step 2, criterion 21) as needing re-verification, reset *that* story's Verification Status to `Not Verified` too — wherever its file currently lives — with a Revision History row explaining why (e.g., "flagged by impact analysis of `<changed story>`").
5. Bump the version for whichever file(s) were touched.

## Step 5 — Summarize

Tell the user: what passed, what didn't, what's now marked verified, what's still open, and — for any story reset by impact analysis — which one and why. Remind them that fixing a finding means rerunning `generate-user-stories` (Update mode) and then this skill again.
