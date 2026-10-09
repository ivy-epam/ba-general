---
name: generate-case-study
description: Create or update a business case study documenting a problem solved, solution delivered, and measurable outcomes — written from the BA's perspective for their professional portfolio/external sharing. Showcases industry context, business challenge, delivered solution, and quantified results; the BA's role is secondary context. One file per project, stored outside outputs/. Use when the user asks to write a case study, portfolio project writeup, or is offboarding/wrapping up and wants to document the project's problem, solution, and outcomes.
---

# Generate Case Study

Produces or updates **a business case study** (`case-study/<project-code>-case-study.md`) — a narrative of a problem solved, solution delivered, and measurable outcomes achieved. Written from the BA's perspective, it showcases the business challenge, what was built, and the results, for the contractor's professional portfolio and potential external sharing. Unlike every other skill in this project, this is **not a project deliverable**: it is not stored under `outputs/`, and the rest of the project team never sees it. It lives in a separate top-level `case-study/` folder because it's the contractor's own portfolio record spanning the whole engagement, not an artifact handed to the project.

**One file per project**, prefixed with the project code so the folder can accumulate case studies from many past projects over time: `case-study/<project-code>-case-study.md`.

**Content sourcing — both, in sequence:**
1. **First**, read whatever generated project artifacts already exist under `outputs/` for this project code, to establish factual problem/solution/scope: `outputs/<project-code>-PRD.md`, any `outputs/feature-*/*-feature-analysis.md` and `outputs/feature-*/*-knowledge.md` files, and delivered stories under `outputs/delivered/`. These may not all exist (the project may predate this tool, or this skill may be run standalone) — that's fine, proceed with whatever is found.
2. **Then**, interview the user directly for everything the documents can't fully capture: industry/business context, the underlying business problem, quantified outcomes and results (client-reported, team-tracked, or stakeholder-validated), the BA's role and contributions, and lessons learned. Source documents describe the solution and scope; the user provides the business problem/challenge framing, outcomes/impact, and what they learned.

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

### 2.1 — Read existing project artifacts, if any

Check for, and read where present:
- `outputs/<project-code>-PRD.md`
- `outputs/feature-*/*-feature-analysis.md`
- `outputs/feature-*/*-knowledge.md`
- Delivered stories under `outputs/delivered/**` belonging to this project (cross-reference via the feature names found in the PRD's Key Features/Capabilities; if ambiguous which features belong to this project code, ask the user)

If none exist, tell the user plainly and proceed entirely via interview — this is not a blocker.

Extract only **factual project/feature grounding** from these sources (purpose/background, target users, key features, what was delivered and when) for Section 4 (Project Scope & Key Deliverables). Never pull personal-role, challenge, or achievement content from these docs — they describe the product, not the contractor's personal contribution.

### 2.2 — Confidentiality interview (gate before drafting)

Ask the explicit confidentiality questions listed above (client-name and industry-domain sharing). Record the answers before proceeding to content interview.

### 2.3 — Interview for business narrative & outcomes

Ask, section by section (skip any the user says doesn't apply yet, and flag the skip under Open Questions rather than leaving it silently blank):
- **Industry & Business Context:** client's industry, business model, market position, competitive/regulatory context (respecting the confidentiality decision from Step 2.2).
- **Problem Statement / Business Challenge:** the specific business problem the project was created to solve. What was broken, inefficient, missing? Quantify if possible (cost, time, lost revenue, bottleneck impact).
- **Solution Delivered:** what was built/changed to address the problem. Features, capabilities, scope — draw from existing artifacts where available.
- **Outcomes & Measurable Impact:** project-level results and quantified business outcomes (adoption numbers, revenue impact, efficiency gains, cost savings, customer satisfaction, time-to-market, etc.). For each metric, ask for its source: client-reported, team-tracked, stakeholder feedback, industry benchmark, etc.
- **Engagement Context:** start/end dates or duration, team size and composition, methodology (Agile/Scrum, Waterfall, hybrid).
- **My Role & Key Contributions:** (secondary) the BA's title/role, specific responsibilities and techniques employed (stakeholder interviews, requirements modeling, RBAC design, domain modeling, backlog refinement, etc.), and how those contributed to enabling the solution/outcomes.
- **Key Insights & Lessons Learned:** what the BA/team learned from this engagement. What worked well? What would be done differently? Challenges overcome.

### 2.4 — Draft the document

Follow `templates/case-study-template.md` exactly. Populate:
- Document Control (Project Code, Author, Created date, Confidentiality Level).
- Confidentiality & Sharing Notes — the Step 2.2 decisions, verbatim.
- All remaining sections from interview + source docs: Industry & Business Context, Problem Statement, Solution Delivered (cite source artifacts for scope), Outcomes & Measurable Impact (cite source for each metric), Engagement Context, My Role & Key Contributions (secondary), Key Insights & Lessons Learned. Each claim attributed (source doc + section, or "stated by user in interview," or "client-reported," etc.).
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

### 3.3 — Re-confirm confidentiality if needed

If the update includes new/changed client name or industry/domain details, confirm the confidentiality decisions still apply.

### 3.4 — Apply changes, hard-stop confirm, write back

Apply changes only to the affected sections, leaving the rest unchanged. Present the delta and **wait for explicit confirmation** before writing (same external-facing-stakes rationale as 2.5). Update the Created date in Document Control if this is a significant refresh, or leave it as the original creation date if just adding details/clarifications. Write the updated file back to the same path.

### 3.5 — Chat-only delta summary

Summarize what sections were updated, what stayed the same, any newly-applied confidentiality decisions, and any new Open Questions.

## Shared discipline across all runs

- **No fabrication:** every business/problem/solution/outcome fact traces to a source document (with citation) or direct interview answer; metrics are sourced (client-reported, team-tracked, etc.), not guessed.
- **Confidentiality defaults to NOT shareable** until the user explicitly confirms otherwise; unresolved confidentiality calls go to Open Questions, never guessed.
- **Business facts come from source docs or interview:** solution/scope/features from artifacts, problem/outcomes/business context from the user's own understanding/client reports; never inferred.
- **Chat-only summaries** — never restate the full document in chat after writing it.
