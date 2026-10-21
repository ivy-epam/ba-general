---
name: assess-candidate
description: Assess an analyst candidate's fit for a position — clarifying the role's positioning, grading analysis seniority against the competency reference, and producing interview focus areas and a 29-question interview pack (bank questions, scenario questions targeting the candidate's gaps, and leadership questions probing A3 potential). Use when the user asks to assess a candidate, evaluate a resume/CV, or prepare interview questions for an analyst or hybrid role.
---

# Assess Candidate

Assesses an analyst candidate's fit for a position from their resume and, optionally, a JD, and prepares a targeted interview. 

**Role positioning matters first.** Analyst positions are rarely pure BA any more. Each position is defined on two dimensions:

| Dimension | Options | Rule |
|---|---|---|
| **Analysis focus** | Business · System · Data | 1–2 focuses |
| **Plus responsibility** | Project Manager (PM) · Product Owner (PO) · Scrum Master (SM) · Quality Assurance (QA) | None or one |

E.g. "Business + System analyst, plus Scrum Master" or "Business + Data analyst, no plus responsibility." A candidate is assessed against the positioning the role actually needs.

**Reference:** `references/seniority-competency-definition-business-analysis.md` (in the project-root `references/` folder, as are all paths in this skill) — the analysis seniority baseline. Only **A2** (Business Analyst) and **A3** (Senior Business Analyst) are in scope. Always read the current file rather than applying competencies from memory, in case it has been edited. The file opens with a pre-generated **A2 vs A3 — Interview Calibration Summary** used by Step 3; the detailed sections below it remain the source for Step 4's evidence mapping. Focus-specific skills (system, data) and the plus responsibility aren't covered by it; those come from Step 1.

## Step 1 — Clarify role positioning (hard stop)

Before anything else, establish the position's **analysis focus(es)** — primary first, if there are two — and its **plus responsibility**, if any. Business is always the primary focus; System or Data can only be the secondary focus.

- **JD provided:** analyse the JD and propose the positioning, quoting the JD lines that support each focus and the plus responsibility — e.g. "System focus: 'define API contracts and integration specs'"; "plus SM: 'facilitate sprint ceremonies'".
- **No JD:** ask the user for the analysis focus(es) and plus responsibility.

For each System/Data focus and the plus responsibility, list the expected skills or responsibilities as concrete, assessable items. Take them from the JD or the user — if neither specifies them, ask rather than assuming a generic role profile of Business Analyst. **Wait for the user's confirmation** of the positioning before continuing.

## Step 2 — Identify job context

- **JD provided:** extract the remaining role requirements, constraints, and domain context, then research the domain/industry requirements for the position.
- **No JD:** use a general analyst context for software development, and say so explicitly.
- Do not assume a client domain, industry, or position requirement the user hasn't provided.

## Step 3 — Calibrate seniority expectations

1. Read the **A2 vs A3 — Interview Calibration Summary** section of the reference file. Don't re-derive it from the detailed sections.
2. Present it as the seniority baseline, with the confirmed focus-specific skills and plus responsibility from Step 1 added alongside it.
3. Continue straight to the assessment — no confirmation needed.

If the reference file can't be read or is empty, stop and tell the user: "The seniority reference file cannot be found." If the summary section is missing, stop and tell the user: "The seniority calibration summary is missing from the reference file — regenerate it before assessing."

The summary is regenerated manually when the competency definitions change; this skill never rewrites it.

## Step 4 — Assess the candidate

1. **Check for analysis evidence.** If the resume has none, set met seniority to **Below A2** and explain the evidence gap explicitly. Otherwise, map explicit resume evidence to the reference competencies.
2. **Determine met seniority:** the highest of A2 or A3 where at least 80% of required competencies are satisfied. If A2 isn't met, the result is **Below A2**. If the candidate clearly exceeds A3, record A3 and note that their level is beyond the reference's scope.
3. **Assess each focus and the plus responsibility** against its confirmed items, rating each **Strong** (explicit, recent evidence) / **Partial** (indirect or dated evidence) / **None**.
4. **Assess against the position** (Step 2): highlight skill or experience gaps.
5. Give the rationale with specific evidence, gaps, and risk indicators — including whether the candidate can realistically cover the full positioning together.

## Step 5 — Hard stop (interview focus confirmation)

Summarise what the interview should focus on for each aspect, drawing on the role positioning (Step 1), the JD (Step 2), and the candidate assessment (Step 4), and explain why each matters for role fit:

| Aspect | Focus |
|---|---|
| **Analysis focus** | The 1–2 confirmed focuses (Business / System / Data), primary first |
| **Plus responsibility** | The confirmed plus responsibility, if any (PM / PO / SM / QA) |
| **Agile methodology** | Agile practices the JD and positioning call for |
| **AI use in daily work** | Expected AI usage at the met seniority level |
| **Soft skills** | Soft skills the JD and positioning call for |
| **Candidate assessment** | Gaps, Partial/None ratings, and points needing clarification from Step 4 |
| **Leadership & influence** | Below A2 or A2: signs of A3 potential. A3: depth of leadership and influence. Covers shaping ways of working and BA processes, team leadership, and coaching other BAs |
**Wait for the user's review** before generating questions.

## Step 6 — Generate interview questions

Read `references/interview-question-bank.md` — always the current file, not from memory.

**Allocation — 29 questions in total:** 24 selected from the bank, plus 5 generated (3 scenario, 2 leadership):

| Focuses | Plus resp. | Primary focus | Secondary focus | Plus resp. | Agile | Soft skills | AI | Scenario | Leadership | Total |
|---|---|---|---|---|---|---|---|---|---|---|
| 1 | None | 17 | — | — | 3 | 2 | 2 | 3 | 2 | 29 |
| 1 | One | 14 | — | 3 | 3 | 2 | 2 | 3 | 2 | 29 |
| 2 | None | 11 | 6 | — | 3 | 2 | 2 | 3 | 2 | 29 |
| 2 | One | 10 | 4 | 3 | 3 | 2 | 2 | 3 | 2 | 29 |

Fixed counts: Agile 3, Soft skills 2, AI 2, plus responsibility 3 (when there is one), scenario 3, leadership 2. Analysis focus gets the rest; with two focuses, the primary gets more.
1. **Bank aspects — select.** Use only the sections for the confirmed focus(es) and plus responsibility. For each aspect:
   - **Mandatory** questions are always selected and count toward its allocation. **Mandatory (A3)** questions are treated as Mandatory when the met seniority from Step 4 is A3, and as Optional otherwise.
   - Fill the remaining places with **Optional** questions that best fit the focuses confirmed in Step 5, each with a one-line rationale tied to this candidate or JD (e.g. "probes the Partial rating on stakeholder management", "JD stresses regulatory change").

   Keep each question's ID and use the bank's wording exactly — don't reword questions to fit the JD's domain or write new questions for these aspects. Domain-specific angles belong in the Rationale column and the scenario questions. If a section's Mandatory questions exceed its allocation, keep the allocation, select the Mandatory questions in bank order, and flag the bank for correction.
2. **Candidate assessment — generate.** After selecting the bank questions, create **3 scenario-based questions** that verify the gaps, areas needing improvement, and insufficiencies identified in Step 4, calibrated to the met seniority level. They must not repeat or paraphrase any selected bank question — where a gap overlaps a selected question's topic, take a different angle, e.g. build the scenario around a type of work the candidate claims on their resume, probe how they'd handle a complication or failure rather than the standard approach, or combine the gap with another competency in one situation.

   Keep scenarios generic, because the candidate may not have the client's domain or system knowledge, and the scenarios test analysis skill, not that knowledge. Use a neutral, everyday business setting (e.g. orders, customers, partners), state within the question any rule or term the answer depends on, and don't name a specific domain, system, product, client, or the candidate's employers. Put the link to the JD's domain and the resume-specific evidence in the Rationale column instead.
3. **Leadership & influence — generate.** Create **2 questions** drawn from the A3 leadership competencies in the reference (e.g. Team Management, Mentoring, Developing Others, Leadership, Driving Change and Innovation, BA approach and SDLC improvement): one on how the candidate has influenced ways of working or BA processes beyond their own tasks, and one on leading a team or coaching other BAs. Every candidate gets both, whatever their met seniority:
   - **Below A2 or A2:** look for A3 potential — signs they have already acted beyond their level.
   - **A3:** confirm the depth and impact of their leadership and influence.

   The same rules as the scenario questions apply: don't repeat or paraphrase a selected bank question, and keep them generic. They may ask about the candidate's past experience ("Tell me about a time…") as well as hypothetical situations.
4. **Mark must-ask questions (★)** — every Mandatory bank question plus all 5 generated questions. Optional questions are backups to use as time allows.

Present all 29 questions as one table — bank questions first, then the scenario questions, then the leadership questions:

| ★ | Aspect | ID | Type | Question | Strong Answer Includes | Rationale |
|---|---|---|---|---|---|---|

- **Bank questions:** Type is "Mandatory" or "Optional", as resolved for this candidate (a Mandatory (A3) question shows as "Mandatory" for an A3 candidate and "Optional" otherwise); Strong Answer Includes is copied from the bank, including any **Perspective** note.
- **Scenario questions:** Aspect is "Candidate assessment", IDs run SC-01 to SC-03, and Type is "Scenario". Rationale names the gap or area to verify and the assessment evidence behind it.
- **Leadership questions:** Aspect is "Leadership & influence", IDs are LI-01 and LI-02, and Type is "Leadership". Rationale names the A3 competency probed and the resume evidence, or lack of it, behind the question.

## Step 7 — Interview notices

Highlight areas needing interviewer attention for fairness, depth, and decision confidence — any ambiguity, resume inconsistencies, or evidence limitations to probe live, including any focus or the plus responsibility the resume leaves unclear.

## Step 8 — Confirm and save the interview pack (hard stop)

Ask the user to confirm the question table and interview notices, or to request changes. **Wait for confirmation** before writing the file; apply any requested changes first.

Once confirmed, write the pack to `references/interview-candidate-data/interview-question-<candidate-name>.md` (candidate name in lowercase, hyphenated). If the file already exists, ask before overwriting it. The file contains:

1. A short header: candidate, position, role positioning, met seniority, interview scope, and question allocation.
2. The Step 6 question table.
3. The Step 7 interview notices.

The pack has no Document Control & Revision History section and no update mode — re-running the skill produces a new pack.
