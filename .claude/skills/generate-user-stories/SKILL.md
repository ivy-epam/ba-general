---
name: generate-user-stories
description: Create a new user story (one file per story) or update an existing one, scoped to a single use case. A use case can split into one or more agile-ready stories, each with its own Gherkin (Given/When/Then) acceptance criteria derived from that use case's flows, plus references to relevant Non-Functional Requirements. New stories are placed in the future-sprint bucket by default. Use when the user asks to write/create user stories or acceptance criteria for a use case.
---

# Generate User Stories (one file per story)

Produces or updates **individual story files**, one per confirmed story, scoped to a single use case at a time — not a whole feature. A single use case can split into multiple stories when its flows represent independently shippable chunks; each gets its own file so it can move independently through the sprint-bucket folders as its status changes. This is the last generation step in the artifact chain: BRD → PRD → Feature Analysis (as-is/to-be/gaps/NFRs) → Use Cases → RBAC → **User Stories/ACs**.

**Sourcing discipline:** the specific use case's Basic/Alternate/Exception flows are the primary driver of its stories and acceptance criteria. The PRD, Feature Analysis (including its Non-Functional Requirements section), and RBAC documents are supporting context. Interview only fills what none of these establish — mainly concrete detail the use case's flows don't cover. Every story, AC scenario, and NFR reference must be traceable to a source; nothing is invented.

**NFRs are not owned here.** Non-Functional Requirements live in `outputs/feature-<feature>/<feature>-feature-analysis.md`'s Non-Functional Requirements section (added by `generate-feature-analysis`) — this skill only references NFR IDs from there. If a story surfaces an NFR need that section doesn't yet cover, flag it as an Open Question suggesting it be added there; do not invent a new NFR in this document.

The template lives at `templates/user-stories-template.md` in this project. Always read that file first to get the current section structure — do not hardcode the structure from memory, in case the template has been edited.

**Output location and the sprint-bucket model:** each story is its own file at `outputs/<bucket>/US-<use-case-name>/<use-case-name>-US-0X.md`, where `<bucket>` is one of `future-sprint`, `current-sprint`, or `delivered`. **New stories always start in `future-sprint/`** — moving a story to `current-sprint/` is a manual, team-driven action outside this skill (no skill does sprint planning), and moving it to `delivered/` is done by `generate-knowledge-page`, not here. A single use case's stories can legitimately be split across different buckets at once. Never write these documents anywhere else (not the user's home directory, Desktop, or another project).

## Step 0 — Determine mode: create or update

Ask (or infer from the user's request) which use case and story this is for. To check whether a specific story already exists, glob `outputs/*/US-<use-case-name>/<use-case-name>-US-0X.md` across all three buckets (its status may have moved it out of `future-sprint/`).
- **Doesn't exist anywhere** → **Create**.
- **Exists in some bucket** → **Update** (edit it in place, wherever it currently lives — do not move it back to `future-sprint/`).

## Create mode

1. **Locate the use case.** Ask for the feature name to find `outputs/feature-<feature>/<feature>-use-cases.md`, and which use case within it (by ID or name) this run covers. Read that use case's full block: actors, trigger, preconditions, postconditions, Basic/Alternate/Exception flows, and business rules referenced.

2. **Gather supporting context** where available:
   - `outputs/<project-code>-PRD.md` — goals, for framing the story's "so that" benefit.
   - `outputs/feature-<feature>/<feature>-feature-analysis.md` — its Non-Functional Requirements section, for NFR IDs this use case's stories might reference.
   - `outputs/rbac.md` — the Roles Inventory, to keep story roles consistent with what's already documented there.
   Skip any that don't exist and rely on interview for that gap instead of blocking.

3. **Propose a story-split candidate list for this one use case.** Default to a single story; propose more when distinct alternate/exception flows represent independently shippable value. Present the candidates (tentative ID, title, role, one-line goal, which flow(s) it covers) to the user for confirmation, merge, split, rename, addition, or removal — do not finalize the split unilaterally.

4. **Draft each confirmed story, as its own document:**
   - **"As a / I want / so that":** use a role that matches an entry in the RBAC Roles Inventory where possible; if it doesn't match anything there, flag the mismatch as an Open Question rather than silently reconciling it.
   - **Acceptance Criteria (Gherkin):** one scenario from the Basic Flow (happy path), plus additional scenarios from the Alternate Flow(s)/Exception Flow(s) relevant to this story. Interview to fill a scenario the use case's flows don't cover clearly enough to write a Given/When/Then for.
   - **Related NFRs:** reference NFR IDs from the feature analysis document's NFR section only where genuinely applicable to this story — don't force a reference. If this story clearly needs an NFR that section doesn't have, add it to Open Questions instead of inventing one here.
   - **Sprint Bucket:** set to `future-sprint`.
   - **Verification Status:** set to `Not Verified` — this skill never marks a story verified; only `verify-user-stories` does, after an independent review.
   - **Delivery Status:** set to `Not Delivered` — only `generate-knowledge-page` marks a story delivered.

5. **No fabrication.** Every AC scenario and NFR reference must trace to the use case's flows, a supporting document, or something a stakeholder actually said. Unconfirmed items go to Open Questions.

6. **Draft each story file** following `templates/user-stories-template.md` exactly.

7. **Get the use case's name** (lowercase, hyphenated) and each story's ID (`US-01`, `US-02`, ...) for the output filenames.

8. **Write each confirmed story** to its own file: `outputs/future-sprint/US-<use-case-name>/<use-case-name>-US-0X.md` (create the folders if they don't exist). Version `1.0` per file, first Revision History row "Initial draft."

9. **Summarize for the user** (in chat, not in the documents): the stories derived from this use case (including any splits) and where each file was written, which ACs/NFR references were inferred vs. interview-confirmed, and what's left open.

## Update mode

1. **Locate the existing story file** by globbing `outputs/*/US-<use-case-name>/<use-case-name>-US-0X.md` across all three buckets. Read its full current content, current bucket, and current version.

2. **Gather what's driving the update** — the source use case changed upstream, this story's ACs need revising, or a new NFR reference is needed. Apply the same sourcing discipline, checked against the existing document's content too.

3. **Apply changes only to this story's content** — this skill edits one story file per run.

4. **Reset Verification Status.** If the story's content actually changed (goal, flow coverage, ACs, or NFR references), reset Verification Status to `Not Verified` — a prior verification no longer applies once the content it verified has changed. A cosmetic/no-op touch keeps its existing status. This reset happens automatically; it is not something this skill asks the user about.

5. **Do not move the file between buckets.** This skill only edits content in place, wherever the file currently lives — bucket moves are either manual (future-sprint→current-sprint) or handled by `generate-knowledge-page` (→delivered).

6. **Bump the version and log the change** in the Revision History table: increment the version, record the date, a plain-language description of what changed (including noting "Verification Status reset" if applicable), and the trigger/reason.

7. **Write the updated file back** to its current path (same bucket it was already in).

8. **Summarize the delta for the user**: what changed, any Verification Status reset, and any new open questions raised.
