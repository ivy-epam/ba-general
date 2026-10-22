---
name: generate-knowledge-page
description: Mark a user story as Delivered — setting its Delivery Status — and create or update that feature's plain-language knowledge page for dev/product/ops. One knowledge page per feature (outputs/features/<feature>/<feature>-knowledge.md), created on the first delivery and updated incrementally as more of that feature's stories ship. Use when the user says a story/use case has been delivered, shipped, or released, or asks to update a feature's knowledge page.
---

# Generate Knowledge Page

Does two things in one run: marks a specific user story as **Delivered**, and rolls that delivery into a feature-level knowledge page written in plain language for a broad dev/product/ops audience — not another formal BA artifact.

**Delivery is independent of verification.** Marking a story Delivered never checks or requires its Verification Status — the two track different things ("is this correct" vs. "is this live"). Don't block or warn based on Verification Status.

**Audience-appropriate writing.** Unlike the other six artifacts in this project (formal BA register), this page must read as plain, scannable prose for people who just need to understand the feature — no BA-document jargon, no Gherkin syntax, no raw CRUD matrices. Translate source content into plain language; don't copy formal phrasing verbatim.

**Sources:** the PRD, Feature Analysis (To-Be process + NFRs), Use Cases, RBAC, and delivered User Stories documents — this skill summarizes/translates them. Interview mainly covers ops-specific operational notes the NFR section doesn't.

The template lives at `templates/knowledge-page-template.md` in this project.

The knowledge page is written to `outputs/features/<feature>/<feature>-knowledge.md` — one page per **feature**, not per use case or story.

## Workflow

1. **Identify what was delivered.** Ask which feature, use case, and story just shipped, if not already clear from context. Locate its file in `outputs/features/<feature>/user-stories/<UC-ID>/`.

2. **Mark delivery.**
   - In the story file, set Delivery Status to `Delivered — {{today's date}}`. Add a Revision History row noting the delivery. The file stays where it is.
   - Do this regardless of the story's current Verification Status — no gate.

3. **Determine the feature and locate its knowledge page.** The feature is the `<feature>` folder the story file sits in. Check whether `outputs/features/<feature>/<feature>-knowledge.md` already exists.
   - **Doesn't exist** → this is the first delivery for the feature; build the page from scratch (go to step 4 with a full first draft in mind).
   - **Exists** → this is an incremental update (go to step 4 planning to touch only what's affected).

4. **Gather source content:**
   - `outputs/<project-code>-PRD.md` — Problem Statement & Business Context (Overview), Product Scope & Key Features (Key Capabilities).
   - `outputs/features/<feature>/<feature>-feature-analysis.md` — To-Be: Process Description (How It Works, including its Mermaid diagram, reusable as-is), Non-Functional Requirements (Operational Notes), and any still-open, still-relevant Open Questions (Known Limitations).
   - `outputs/features/<feature>/<feature>-use-cases.md` — for use case names/IDs to cross-reference delivered stories against.
   - `outputs/rbac.md` — Roles Inventory and RBAC Matrix rows relevant to this feature's resources (Roles & Access, translated to plain language).
   - Every story file under `outputs/features/<feature>/user-stories/` with Delivery Status `Delivered` — these define what's actually live for "Delivered Scope So Far" and for scoping Key Capabilities/How It Works to what's shipped, not just planned.

5. **Plain-language framing must not change the actual meaning** of a requirement.

6. **Draft or update the page** per `templates/knowledge-page-template.md`:
   - **First run:** write every section from the gathered sources and seed "Delivered Scope So Far" with just this delivery.
   - **Later runs:** only refresh Key Capabilities / How It Works / Roles & Access if this newly delivered story actually changes what's true there (a delivery that doesn't add new capability shouldn't cause a rewrite). Always add a new row to "Delivered Scope So Far." The Revision History row references the specific use case/story that triggered it (e.g., "v1.2 — added refund capability per US-04 (UC-03) delivery").

7. **Write the output** to `outputs/features/<feature>/<feature>-knowledge.md`.

8. **Summarize for the user**, also covering which story was marked delivered.
