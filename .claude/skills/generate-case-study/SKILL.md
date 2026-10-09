---
name: generate-case-study
description: Create or update a personal case study document capturing the BA contractor's own project experience, role, challenges, achievements, and lessons learned for their portfolio/professional record — not a project deliverable. One file per project, stored outside outputs/. Use when the user asks to write/create a case study or portfolio write-up, or is offboarding/wrapping up from a project and wants to document their experience and achievements.
---

# Generate Case Study

Produces or updates **a personal case study** (`case-study/<project-code>-case-study.md`) — a write-up of the BA contractor's own project experience, achievements, and lessons learned, for their personal portfolio and professional record. Unlike every other skill in this project, this is **not a project deliverable**: it is not stored under `outputs/`, and the rest of the project team never sees it. It lives in a separate top-level `case-study/` folder because it's the contractor's own record spanning the whole engagement, not an artifact handed to the project.

**One file per project**, prefixed with the project code so the folder can accumulate case studies from many past projects over time: `case-study/<project-code>-case-study.md`.

**Content sourcing — both, in sequence:**
1. **First**, read whatever generated project artifacts already exist under `outputs/` for this project code, to establish factual project scope, features, and delivered work: `outputs/<project-code>-PRD.md`, any `outputs/feature-*/*-feature-analysis.md` and `outputs/feature-*/*-knowledge.md` files, and delivered stories under `outputs/delivered/`. These may not all exist (the project may predate this tool, or this skill may be run standalone) — that's fine, proceed with whatever is found.
2. **Then**, interview the user directly for everything those documents can't capture: their personal role/responsibilities, challenges they personally overcame, measurable impact/metrics, stakeholder feedback, skills/techniques demonstrated, lessons learned, engagement duration, and team size/context. Source documents are written in third-person, product-level language — never attribute personal-contribution content (role, challenges, achievements, feedback) to a source document; that content only ever comes from the user.

**Confidentiality discipline — explicit, never assumed.** This document may end up in an external-facing portfolio (shared with future clients or employers), so never assume what's safe to share. Early in the interview, explicitly ask the user:
- Can the real client/company name be used, or should it be anonymized (e.g., "a Fortune 500 healthcare payer" instead of the real name)?
- Can the industry/domain be named even if the client can't?
- For any stakeholder feedback/testimonial: is it OK to attribute by name/title, should it be anonymized (e.g., "the Product Owner"), or should it be omitted entirely?
- Are there any specific facts, metrics, or details to exclude regardless of general confidentiality (e.g., internal financials, unreleased roadmap items)?

Record the answers in the document's **Confidentiality & Sharing Notes** section and apply them consistently through every later section — if the client name is to be anonymized, it must not leak into Project Context, Achievements, or Related Artifacts. **Default to NOT shareable** for anything the user hasn't explicitly cleared; log it under Open Questions instead of publishing it.

**No-fabrication discipline (same as every other skill in this project):** every factual project claim must trace to a source document (cited by file and section) or a direct interview answer. Personal achievements/metrics/feedback are the user's own claims — capture them as stated, attributed to the user, without embellishing or inflating them. Anything unresolved (a metric pending verification, a testimonial pending permission) becomes an Open Questions entry, never a guess.

The template lives at `templates/case-study-template.md`. Always read that file first to get the current section structure — do not hardcode the structure from memory, in case the template has been edited.

**Output location:** `case-study/<project-code>-case-study.md` — a top-level folder, a sibling of `outputs/` at the repo root, not nested inside it. Never written anywhere else (not the user's home directory, Desktop, or another project).

## Step 0 — Identify the project code

Ask the user which project this case study is for, if not already clear (e.g., they just said they're offboarding from a named engagement). Reuse the same project code as `outputs/<project-code>-PRD.md` if that file exists, so the case study lines up with the project's other artifacts. Confirm the code before proceeding — it fixes both the output filename and which `outputs/` artifacts to check in Step 1/2.1.

## Step 1 — Determine mode: create or update

Check whether `case-study/<project-code>-case-study.md` already exists.
- **Doesn't exist** → **Create**.
- **Exists** → **Update**.

## Step 2 — Create mode

### 2.1 — Read existing project artifacts, if any

Check for, and read where present:
- `outputs/<project-code>-PRD.md`
- `outputs/feature-*/*-feature-analysis.md`
- `outputs/feature-*/*-knowledge.md`
- Delivered stories under `outputs/delivered/**` belonging to this project (cross-reference via the feature names found in the PRD's Key Features/Capabilities; if ambiguous which features belong to this project code, ask the user)

If none exist, tell the user plainly and proceed entirely via interview — this is not a blocker.

Extract only **factual project/feature grounding** from these sources (purpose/background, target users, key features, what was delivered and when) for Section 4 (Project Scope & Key Deliverables). Never pull personal-role, challenge, or achievement content from these docs — they describe the product, not the contractor's personal contribution.

### 2.2 — Confidentiality interview (gate before drafting)

Ask the explicit confidentiality questions listed above (client-name sharing, industry naming, feedback attribution, specific exclusions). At minimum, resolve the client-name and feedback-attribution questions before drafting Project Context, Achievements, or Stakeholder Feedback — item-specific confidentiality calls (e.g., a particular metric) can be resolved as they come up in Step 2.3.

### 2.3 — Interview for personal content

Ask, section by section (skip any the user says doesn't apply yet, and flag the skip under Open Questions rather than leaving it silently blank):
- **Project Context:** client/industry (respecting the confidentiality decision), the business problem/objective in the user's own words.
- **Engagement Duration & Team:** start/end dates or duration, team size and composition, methodology.
- **My Role & Responsibilities:** title/role held, day-to-day responsibilities.
- **Key Challenges & How They Were Solved:** hardest problems personally worked through, and how they were solved.
- **Achievements & Measurable Impact:** measurable outcomes (time saved, defects reduced, adoption numbers, cost/revenue impact, stakeholder satisfaction) — ask for a number and its source (e.g., "client-reported," "my own tracking," "team retro") rather than accepting a vague claim.
- **Skills & Techniques Demonstrated:** BA techniques, tools, soft skills used or grown.
- **Stakeholder Feedback:** direct quotes/praise/testimonials received, with attribution confirmed per the Step 2.2 decision.
- **Lessons Learned:** what the user would do differently, what they learned.

### 2.4 — Draft the document

Follow `templates/case-study-template.md` exactly. Populate:
- Document Control (Confidentiality Level field, Status: Draft) + Revision History v1.0, first row "Initial draft."
- Confidentiality & Sharing Notes — the Step 2.2 decisions, verbatim.
- All remaining sections from interview + source docs, each claim attributed (source doc + section, or "stated by user in interview").
- Related Internal Artifacts — links to the `outputs/` files found in 2.1, explicitly marked internal-only.
- Open Questions — anything unresolved, unconfirmed, or pending permission.

### 2.5 — Hard-stop confirmation gate

Before writing the file, present the full draft (or a structured section-by-section summary) in chat and ask the user to confirm it's accurate and that they're comfortable with what's currently marked shareable. **Wait for explicit confirmation before writing anything** — this gate exists because the document may be used in an external-facing portfolio, so the stakes of a mistaken disclosure are higher than for an internal deliverable.

### 2.6 — Write output

Create the `case-study/` folder if it doesn't exist (top-level, sibling of `outputs/`, at the repo root). Write to `case-study/<project-code>-case-study.md`.

### 2.7 — Chat-only summary

Summarize for the user: which `outputs/` sources were used (or that none existed), what was gathered via interview, the confidentiality decisions applied, and any Open Questions — not a restatement of the full document.

## Step 3 — Update mode

### 3.1 — Read existing file

Read the current `case-study/<project-code>-case-study.md` in full; note its current version, Revision History, and existing Confidentiality & Sharing Notes.

### 3.2 — Ask what's driving the update

E.g., a role change, a new achievement surfaced after reflection, new stakeholder feedback received, a corrected metric, a newly-secured permission to name the client.

### 3.3 — Re-confirm confidentiality for any new content

Any new quote, metric, or client-identifying detail introduced in this update gets the same confidentiality questions as Step 2.2 — prior answers do not automatically extend to new content.

### 3.4 — Apply changes, hard-stop confirm, write back

Apply changes only to the affected sections, leaving the rest unchanged. Present the delta and **wait for explicit confirmation** before writing (same external-facing-stakes rationale as 2.5). Bump the version (minor for additions/corrections, major for a significant reframing — use judgment, ask if unclear) and add a Revision History row describing what changed and why. Write the updated file back to the same path.

### 3.5 — Chat-only delta summary

Summarize what changed, what stayed the same, any newly-applied confidentiality decisions, and any new Open Questions.

## Shared discipline across all runs

- **No fabrication:** every project fact traces to a source document or a direct interview answer; every personal claim is attributed to the user as stated.
- **Confidentiality defaults to NOT shareable** until the user explicitly confirms otherwise; unresolved confidentiality calls go to Open Questions, never guessed.
- **Personal content never comes from source docs** — only from the user, even when a source doc happens to mention something adjacent.
- **Chat-only summaries** — never restate the full document in chat after writing it.
