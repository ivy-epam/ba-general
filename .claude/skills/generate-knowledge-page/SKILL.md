---
name: generate-knowledge-page
description: Mark a user story as Delivered — physically moving its story file (and func-test file, if any) into the delivered/ sprint bucket — and create or update that feature's plain-language knowledge page for dev/product/ops. One knowledge page per feature (outputs/feature-<feature>/<feature>-knowledge.md), created on the first delivery and updated incrementally as more of that feature's stories ship. Use when the user says a story/use case has been delivered, shipped, or released, or asks to update a feature's knowledge page.
---

# Generate Knowledge Page

Does three things in one run: marks a specific user story as **Delivered**, physically relocates its file(s) into the `delivered/` sprint bucket, and rolls that delivery into a feature-level knowledge page written in plain language for a broad dev/product/ops audience — not another formal BA artifact.

**Delivery is independent of verification.** Marking a story Delivered never checks or requires its Verification Status — the two track different things ("is this correct" vs. "is this live"). Don't block or warn based on Verification Status.

**Why this skill moves files.** Stories live in sprint-bucket folders (`future-sprint/`, `current-sprint/`, `delivered/`) so the team can browse what's currently relevant. If marking a story Delivered didn't also relocate it out of whichever bucket it was in, the folder structure would immediately go stale — defeating the reason it exists. No other skill moves files between buckets; this is the one place it happens, and only into `delivered/`.

**Audience-appropriate writing.** Unlike the other six artifacts in this project (formal BA register), this page must read as plain, scannable prose for people who just need to understand the feature — no BA-document jargon, no Gherkin syntax, no raw CRUD matrices. Translate source content into plain language; don't copy formal phrasing verbatim.

**Sources:** the PRD, Feature Analysis (To-Be process + NFRs), Use Cases, RBAC, and delivered User Stories documents — this skill summarizes/translates them. Interview mainly covers ops-specific operational notes the NFR section doesn't.

The template lives at `templates/knowledge-page-template.md` in this project.

The knowledge page is written to `outputs/feature-<feature>/<feature>-knowledge.md` — one page per **feature**, not per use case or story.

## Workflow

1. **Identify what was delivered.** Ask which use case and story ID just shipped, if not already clear from context. Locate its current file by globbing `outputs/*/US-<use-case-name>/<use-case-name>-US-0X.md` across all three sprint buckets — don't assume which bucket it's currently in.

2. **Mark delivery and relocate the file(s).**
   - In the story file, set Delivery Status to `Delivered — {{today's date}}` and Sprint Bucket to `delivered`. Add a Revision History row noting the delivery.
   - **Move** the story file from its current bucket to `outputs/delivered/US-<use-case-name>/<use-case-name>-US-0X.md`.
   - If a matching `<use-case-name>-func-test-0X.md` exists alongside it, move that too, to the same new location.
   - Do all of this regardless of the story's current Verification Status — no gate.

3. **Determine the feature and locate its knowledge page.** Find the feature name via the story's own Feature field (or the use case's parent `outputs/feature-<feature>/<feature>-use-cases.md`). Check whether `outputs/feature-<feature>/<feature>-knowledge.md` already exists.
   - **Doesn't exist** → this is the first delivery for the feature; build the page from scratch (go to step 4 with a full first draft in mind).
   - **Exists** → this is an incremental update (go to step 4 planning to touch only what's affected).

4. **Gather source content:**
   - `outputs/<project-code>-PRD.md` — Purpose & Background (Overview), Key Features/Capabilities (Key Capabilities).
   - `outputs/feature-<feature>/<feature>-feature-analysis.md` — To-Be: Process Description (How It Works, including its Mermaid diagram, reusable as-is), Non-Functional Requirements (Operational Notes), and any still-open, still-relevant Open Questions (Known Limitations).
   - `outputs/feature-<feature>/<feature>-use-cases.md` — for use case names/IDs to cross-reference delivered stories against.
   - `outputs/rbac.md` — Roles Inventory and RBAC Matrix rows relevant to this feature's resources (Roles & Access, translated to plain language).
   - Every story file under `outputs/delivered/US-*/` belonging to this feature (found via the feature's use cases) — these define what's actually live for "Delivered Scope So Far" and for scoping Key Capabilities/How It Works to what's shipped, not just planned.

5. **Plain-language framing must not change the actual meaning** of a requirement.

6. **Draft or update the page** per `templates/knowledge-page-template.md`:
   - **First run:** write every section from the gathered sources and seed "Delivered Scope So Far" with just this delivery.
   - **Later runs:** only refresh Key Capabilities / How It Works / Roles & Access if this newly delivered story actually changes what's true there (a delivery that doesn't add new capability shouldn't cause a rewrite). Always add a new row to "Delivered Scope So Far." The Revision History row references the specific use case/story that triggered it (e.g., "v1.2 — added refund capability per US-04 (UC-03) delivery").

7. **Write the output** to `outputs/feature-<feature>/<feature>-knowledge.md`.

8. **Summarize for the user**, also covering which story was marked delivered and moved (and to where).
