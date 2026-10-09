---
name: generate-case-study
description: Create or update a business case study documenting a problem solved, solution delivered, and measurable outcomes from the BA's perspective. One file per project, stored outside outputs/. Use when the user asks to write a case study, portfolio project writeup, or is offboarding/wrapping up a project.
---

# Generate Case Study

Produces or updates **a business case study** (`case-study/<project-code>-case-study.md`) — a narrative of a problem solved, solution delivered, and measurable outcomes achieved. Written from the BA's perspective, it showcases the business challenge, what was built, and the results, for the BA's professional portfolio and potential external sharing. Unlike every other skill in this project, this is **not a project deliverable**: it is not stored under `outputs/`, and it lives in a separate top-level `case-study/` folder because it's the BA's own portfolio record spanning the whole engagement, not an artifact handed to the project.

**One file per project**, prefixed with the project code so the folder can accumulate case studies from many past projects over time: `case-study/<project-code>-case-study.md`.

**Content sourcing — multiple sources:**
1. **Raw project information** (`docs/<project-code>/`): read raw project/product information, market research, and product details stored in the project's documentation folder.
2. **User interview:** gather industry/business context, business problem framing, outcomes/impact, the BA's role and contributions, and lessons learned.
3. **LLM research:** supplement Industry & Business Context with market research (trends, market landscape, regulatory context) and supplement Problem Statement with competitor analysis (competitive positioning, market gaps, benchmarks) to enrich and contextualize the user's narrative.

**Confidentiality discipline — explicit, never assumed.** Early in the interview, ask the user:
- Can the real client/company name be used, or should it be anonymized (e.g., "a mid-size regional bank")?
- Can the industry/domain be named, or should it be withheld?

Record the answers in the document's **Confidentiality & Sharing Notes** section and apply them consistently through every later section.

**No-fabrication discipline (same as every other skill in this project):** every factual business claim (problem, solution, scope) must trace to a source document (cited by file and section) or a direct interview answer. Business outcomes/metrics are the user's claims (or client-reported facts) — capture them as stated, attributed to the source (e.g., "client-reported post-launch," "team analytics"), without embellishing or inflating them. Anything unresolved (a metric pending verification, a permission question) becomes an Open Questions entry, never a guess.

The template lives at `templates/case-study-template.md`. Always read that file first to get the current section structure — do not hardcode the structure from memory, in case the template has been edited.

**Output location:** `case-study/<project-code>-case-study.md` — a top-level folder, a sibling of `outputs/` at the repo root, not nested inside it. Never written anywhere else (not the user's home directory, Desktop, or another project).

## Step 0 — Identify the project code

Ask the user which project this case study is for, if not already clear (e.g., they just said they're offboarding from a named engagement). Reuse the same project code as `outputs/<project-code>-PRD.md` if that file exists, so the case study lines up with the project's other artifacts. Confirm the code before proceeding — it fixes both the output filename and which `outputs/` artifacts to check in Step 1/2.1.

## Step 1 — Determine mode: create or update

Check whether `case-study/<project-code>-case-study.md` already exists.
- **Doesn't exist** → **Create**.
- **Exists** → **Update**.

## Step 2 — Create mode

### 2.1 — Read existing project information, if any

Check for, and read where present:
- Raw project/product information under `docs/<project-code>/` (market research, product overviews, competitive landscape, business background, etc.)

If none exist, tell the user plainly and proceed via interview + LLM research — this is not a blocker.

Extract **factual project/market grounding** from the documentation (purpose/background, target market, key features, product positioning, market context, competitive landscape) for the business context and problem statement sections. Never pull personal-role, challenge, or achievement content from these docs — they describe the product/market, not the contractor's personal contribution.

### 2.2 — Confidentiality interview (gate before drafting)

Ask the explicit confidentiality questions listed above (client-name and industry-domain sharing). Record the answers before proceeding to content interview.

### 2.3 — Interview for business narrative & outcomes, supplemented with LLM research

Ask, section by section (skip any the user says doesn't apply yet, and flag the skip under Open Questions rather than leaving it silently blank):

- **Industry & Business Context:** 
  - Interview: client's industry, business model, market position, competitive/regulatory context (respecting confidentiality from Step 2.2).
  - Supplement: perform LLM-driven market research on the client's industry/company (trends, market size, key players, regulatory landscape, growth drivers) to enrich and contextualize the user's description.

- **Problem Statement / Business Challenge:**
  - Interview: the specific business problem the project was created to solve. What was broken, inefficient, missing? Quantify if possible (cost, time, lost revenue, bottleneck impact).
  - Supplement: perform LLM-driven competitor analysis (competitors' offerings, market gaps, positioning opportunities, industry benchmarks) to frame the user's problem statement in competitive context and inspire alternative framings if helpful.

- **Solution Delivered:** what was built/changed to address the problem. Features, capabilities, scope — draw from existing artifacts where available.

- **Outcomes & Measurable Impact:** project-level results and quantified business outcomes (adoption numbers, revenue impact, efficiency gains, cost savings, customer satisfaction, time-to-market, etc.). For each metric, ask for its source: client-reported, team-tracked, stakeholder feedback, industry benchmark, etc.

- **Engagement Context:** start/end dates or duration, team size and composition, methodology (Agile/Scrum, Waterfall, hybrid).

- **My Role & Key Contributions:** (secondary) the BA's title/role, specific responsibilities and techniques employed (stakeholder interviews, requirements modeling, RBAC design, domain modeling, backlog refinement, etc.), and how those contributed to enabling the solution/outcomes.

### 2.4 — Draft the document

Follow `templates/case-study-template.md` exactly. Populate:
- Document Control (Project Code, Author, Created date, Confidentiality Level).
- Confidentiality & Sharing Notes — the Step 2.2 decisions, verbatim.
- All remaining sections from interview + source docs + LLM research: 
  - Industry & Business Context: blend user's description with raw project info from `docs/<project-code>/` and LLM market research (trends, market context, positioning).
  - Problem Statement: blend user's problem framing with raw project info and LLM competitor analysis (market gaps, competitive positioning).
  - Solution Delivered (cite project info for scope).
  - Outcomes & Measurable Impact (cite source for each metric).
  - Engagement Context, My Role & Key Contributions (secondary).
  - Each claim attributed (docs/<project-code>, user interview, "LLM market research," "competitor analysis," etc.).

### 2.5 — Write output

Create the `case-study/` folder if it doesn't exist (top-level, sibling of `outputs/`, at the repo root). Write to `case-study/<project-code>-case-study.md`.

### 2.6 — Chat-only summary

Summarize for the user: what raw project info was read from `docs/<project-code>/`, what was gathered via interview, the market research and competitor insights added, and the confidentiality decisions applied. Invite the user to review and manually edit the file as needed.

## Step 3 — Update mode

### 3.1 — Read existing file

Read the current `case-study/<project-code>-case-study.md` in full; note its current version, Revision History, and existing Confidentiality & Sharing Notes.

### 3.2 — Ask what's driving the update

E.g., a role change, a new achievement surfaced after reflection, new stakeholder feedback received, a corrected metric, a newly-secured permission to name the client.

### 3.3 — Re-confirm confidentiality if needed

If the update includes new/changed client name or industry/domain details, confirm the confidentiality decisions still apply.

### 3.4 — Apply changes and write back

Apply changes only to the affected sections, leaving the rest unchanged. Update the Created date in Document Control if this is a significant refresh, or leave it as the original creation date if just adding details/clarifications. Write the updated file back to the same path.

### 3.5 — Chat-only delta summary

Summarize what sections were updated, what stayed the same, and any newly-applied confidentiality decisions. Invite the user to review and manually edit as needed.

## Shared discipline across all runs

- **No fabrication:** every business/problem/solution/outcome fact traces to a source document (with citation) or direct interview answer; metrics are sourced (client-reported, team-tracked, etc.), not guessed. If something cannot be verified, ask the user to clarify rather than inferring.
- **Confidentiality:** client name and industry/domain decisions are confirmed in Step 2.2 before drafting.
- **Business facts come from source docs or interview:** solution/scope/features from artifacts, problem/outcomes/business context from the user's own understanding/client reports; never inferred.
- **Chat-only summaries** — never restate the full document in chat after writing it.
