---
name: generate-case-study
description: Create a business case study documenting a problem solved, solution delivered, and measurable outcomes from the BA's perspective. One file per client (or per project, if that client had multiple distinct engagements), stored outside outputs/, created once at offboarding. Use when the user asks to write a case study or portfolio project writeup before leaving a project.
---

# Generate Case Study

Produces **a business case study** (`case-study/<client-code>[-<project-code>]-case-study.md`) — a narrative of a problem solved, solution delivered, and measurable outcomes achieved. Written from the BA's perspective, it showcases the business challenge, what was built, and the results, for the BA's professional portfolio and potential external sharing. Unlike every other skill in this project, this is **not a project deliverable**: it is not stored under `outputs/`, and it lives in a separate top-level `case-study/` folder because it's the BA's own portfolio record spanning the whole engagement, not an artifact handed to the project.

**One-time creation:** case studies are created once at offboarding. Any further edits are done manually by the user.

**One file per client, or per project if a client had multiple distinct engagements.** A single client may be worked across several separate projects over time; each gets its own case study. File naming is prefixed `<client-code>`, with an optional `-<project-code>` suffix when the case study is scoped to one specific project rather than the client generally: `case-study/<client-code>[-<project-code>]-case-study.md`.

**Content sourcing — multiple sources:**
1. **Raw project information** (`docs/<client-code>/`): read raw project/product information, market research, and product details stored in the client's documentation folder.
2. **User interview:** gather industry/business context, business problem framing, outcomes/impact, the BA's role and contributions, and lessons learned.
3. **LLM research:** supplement Industry & Business Context with market research (trends, market landscape, regulatory context) and supplement Problem Statement with competitor analysis (competitive positioning, market gaps, benchmarks) to enrich and contextualize the user's narrative.

**Confidentiality discipline — explicit, never assumed.** Early in the interview, ask the user:
- Can the real client/company name be used, or should it be anonymized (e.g., "a mid-size regional bank")?
- Can the industry/domain be named, or should it be withheld?

Record the answers in the document's **Confidentiality & Sharing Notes** section and apply them consistently through every later section.

**No fabrication — but traceability stays internal**, not printed inline in the document. **Never write literal file-path citations (e.g., `` `docs/<project-code>/role_desc.md` ``) or source links in the body prose of any section** — this is a polished portfolio narrative, not a cited deliverable. Business outcomes/metrics are the user's claims (or client-reported facts) — capture them as stated, without embellishing or inflating them.

The template lives at `templates/case-study-template.md`.

**Output location:** `case-study/<client-code>[-<project-code>]-case-study.md` — a top-level folder, a sibling of `outputs/` at the repo root, not nested inside it.

## Step 0 — Identify the client (and project, if applicable)

Ask the user which client this case study is for, if not already clear (e.g., they just said they're offboarding from a named engagement). Then ask whether that client involved multiple distinct projects/engagements:
- If there's just one project for this client (the common case), the case study is scoped to the client generally — use `<client-code>` alone.
- If the BA worked multiple separate projects for the same client, ask which project this case study covers and get a short project code/slug — the filename becomes `<client-code>-<project-code>`.

Reuse the same identifier(s) as any existing `outputs/<project-code>-PRD.md` for this engagement, so the case study lines up with the project's other artifacts. Confirm the client code (and project code, if applicable) before proceeding — it fixes both the output filename and which `outputs/`/`docs/` artifacts to check in Step 1/2.1.

## Step 1 — Check if case study already exists

Check whether `case-study/<client-code>[-<project-code>]-case-study.md` already exists. If it does, let the user know the file already exists; they can review it and edit manually if needed. Otherwise, proceed to create mode.

## Step 2 — Create mode

### 2.1 — Read existing project information, if any

Check for, and read where present:
- Raw project/product information under `docs/<client-code>/` (market research, product overviews, competitive landscape, business background, etc.)

If none exist, tell the user plainly and proceed via interview + LLM research.

Extract **factual project/market grounding** from the documentation (purpose/background, target market, key features, product positioning, market context, competitive landscape) for the business context and problem statement sections. Never pull personal-role, challenge, or achievement content from these docs — they describe the product/market, not the contractor's personal contribution.

### 2.2 — Confidentiality interview (gate before drafting)

Ask the explicit confidentiality questions listed above (client-name and industry-domain sharing). Record the answers before proceeding to content interview.

### 2.3 — Interview for business narrative & outcomes, supplemented with LLM research

Ask, section by section (skip any the user says doesn't apply yet, and flag the skip under Open Questions rather than leaving it silently blank):

- **Industry & Business Context:** 
  - Interview: client's industry, business model, market position, competitive/regulatory context (respecting confidentiality from Step 2.2).
  - Supplement: perform LLM-driven market research on the client's industry/company (trends, market size, key players, regulatory landscape, growth drivers) to enrich and contextualize the user's description.
  - Write-up: keep this section to **2-3 sentences** — a tight synthesis, not a market report. Let the research inform the framing (e.g., "a fast-growing but high-friction market," "a high-stakes region given its scale") without naming specific competitors or other companies, and without inline source links/citations in the prose.

- **Problem Statement / Business Challenge:**
  - Interview: the specific business problem the project was created to solve. What was broken, inefficient, missing? Quantify if possible (cost, time, lost revenue, bottleneck impact).
  - Supplement: perform LLM-driven competitor analysis (competitors' offerings, market gaps, positioning opportunities, industry benchmarks) to frame the user's problem statement in competitive context and inspire alternative framings if helpful.
  - Write-up: open with a **1-2 sentence** framing of the core risk/challenge, then list the concrete pain points as a short bulleted/numbered list (each bullet a short bolded phrase, not a full paragraph). Let competitor analysis sharpen the framing without naming specific competitors or other companies, and without inline source links/citations in the prose.

- **Solution Delivered:** first ask which one applies to this engagement — it is either role onboarding or project delivery, never both:
  - **Project delivery:** what was built/changed to address the problem, and what the BA owned for it. Features, capabilities, scope — draw from existing artifacts where available.
  - **Role onboarding:** the BA was onboarded into a dedicated role to close a manpower and/or skills gap in the client's team. Ask which role, which capabilities/areas it owned for the client, and what was explicitly out of scope (e.g., the platform itself, owned by another team).

- **My Role & Responsibilities:** the BA's title/role, where it sat in the team/program, its scope (what it owned and what it did not), and the responsibility areas it covered, with the techniques employed in each (stakeholder interviews, requirements modeling, RBAC design, domain modeling, backlog refinement, etc.). This section describes the job, not the results.

- **Key Achievements & Contributions:** what the BA personally accomplished. For each achievement, ask what the BA specifically did (actions taken, artifacts produced, decisions driven) and what result it produced (adoption numbers, efficiency gains, incident reduction, stakeholder satisfaction, time-to-market, etc.), quantified where possible. Ask how each result is known (client-reported, team-tracked, stakeholder feedback, etc.) so it can be stated accurately, and flag unquantified results under Open Questions.

### 2.4 — Draft the document

Follow `templates/case-study-template.md` exactly. Populate:
- Confidentiality & Sharing Notes — just the client/company name and the industry/domain itself (real or anonymized per the Step 2.2 decision), with no extra labels like "Real name OK to use —" or "Shareable —" prefixed to the value; the sharing decision itself already lives in the Document Control "Confidentiality Level" field.
- All remaining sections from interview + source docs + LLM research — written as plain narrative/tables with **no inline file-path citations or source links anywhere in the body** :
  - Industry & Business Context: blend user's description with raw project info and LLM market research (trends, market context, positioning), per the 2-3 sentence limit above.
  - Problem Statement: blend user's problem framing with raw project info and LLM competitor analysis (market gaps, competitive positioning), per the short intro + bullet list format above.
  - Solution Delivered: open with a one-sentence italic *Scope note* that frames the single dimension that applies, then one `Feature / Capability | Description` table (one row per capability, one-sentence descriptions).
    - Role onboarding: the note says the solution was to onboard a dedicated <role> to own <areas> — and what it was *not* (e.g., not rebuilding the platform, which remained owned by another team). Rows are the capabilities the role brought to the client (e.g., incident management, local SME function, release planning).
    - Project delivery: the note states the BA's role and ownership over the capabilities listed (e.g., requirement engineering and validation, working with the PO/PM). Rows are the product features/capabilities delivered.
    - No Impact/outcome column (that belongs in Key Achievements & Contributions) and no file-path citations.
  - My Role & Responsibilities: title, a 1-2 sentence scope statement, then a bulleted list of responsibility areas (each a short bolded phrase plus what it covered). No achievements or results here.
  - Key Achievements & Contributions: one table row per achievement — a short Dimension label (e.g., Delivery, Stakeholder Engagement, Quality, Process Improvement) and a single Achievement statement combining what the BA personally did with the result it produced. Keep the statement specific to the BA's own actions, not the wider team's.
- Document Control, last (Client, Project — only if this case study is scoped to one specific project rather than the client generally, Created date, Confidentiality Level).

### 2.5 — Write output

Write to `case-study/<client-code>[-<project-code>]-case-study.md`.

### 2.6 — Summary

Summarize for the user: what raw project info was read from `docs/<client-code>/`, what was gathered via interview, the market research and competitor insights added, and the confidentiality decisions applied. Invite the user to review and manually edit the file as needed.

## Shared discipline

The case study is created once at offboarding. Any further edits are done manually by the user.

- **Metrics are sourced** (client-reported, team-tracked, etc.), not guessed.
- **Confidentiality:** client name and industry/domain decisions are confirmed in Step 2.2 before drafting.
- **Where facts come from:** solution/scope/features from artifacts; problem/outcomes/business context from the user's own understanding/client reports.
