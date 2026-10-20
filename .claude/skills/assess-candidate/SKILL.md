---
name: assess-candidate
description: Assess an analyst candidate's fit for a position — clarifying the role's positioning, grading analysis seniority against the competency reference, and producing interview focus areas and a 26-question interview pack (bank questions plus scenario questions targeting the candidate's gaps). Use when the user asks to assess a candidate, evaluate a resume/CV, or prepare interview questions for an analyst or hybrid role.
---

# Assess Candidate

Assesses an analyst candidate's fit for a position from their resume and, optionally, a JD, and prepares a targeted interview. 

**Role positioning matters first.** Analyst positions are rarely pure BA any more. Each position is defined on two dimensions:

| Dimension | Options | Rule |
|---|---|---|
| **Analysis focus** | Business · System · Data | 1–2 focuses |
| **Plus responsibility** | Project Manager (PM) · Product Owner (PO) · Scrum Master (SM) · Quality Assurance (QA) | None or one |

E.g. "Business + System analyst, plus Scrum Master" or "Business + Data analyst, no plus responsibility." A candidate is assessed against the positioning the role actually needs.

**Reference:** `references/seniority-competency-definition-business-analysis.md` — the analysis seniority baseline. Only **A2** (Business Analyst) and **A3** (Senior Business Analyst) are in scope. Always read the current file rather than applying competencies from memory, in case it has been edited. Focus-specific skills (system, data) and the plus responsibility aren't covered by it; those come from Step 1.

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

1. Read the reference file, using both sections (General Requirements and Skill Requirements) to understand expectations for A2 and A3.
2. Summarize what distinguishes A2 from A3 in practical interview terms.
3. Add the confirmed focus-specific skills and plus responsibility from Step 1 alongside the seniority baseline.
4. Include this baseline in the output and continue straight to the assessment — no confirmation needed.

If the reference file can't be read or is empty, stop and tell the user: "The seniority reference file cannot be found."

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

**Wait for the user's review** before generating questions.

## Step 6 — Generate interview questions

Read `references/interview-question-bank.md` — always the current file, not from memory.

**Allocation — 26 questions in total:** 5 generated scenario questions, plus 21 selected from the bank:

| Focuses | Plus resp. | Primary focus | Secondary focus | Plus resp. | Agile | Soft skills | AI | Scenario | Total |
|---|---|---|---|---|---|---|---|---|---|
| 1 | None | 14 | — | — | 3 | 2 | 2 | 5 | 26 |
| 1 | One | 11 | — | 3 | 3 | 2 | 2 | 5 | 26 |
| 2 | None | 8 | 6 | — | 3 | 2 | 2 | 5 | 26 |
| 2 | One | 7 | 4 | 3 | 3 | 2 | 2 | 5 | 26 |

Fixed counts: Agile 3, Soft skills 2, AI 2, plus responsibility 3 (when there is one), scenario 5. Analysis focus gets the rest; with two focuses, the primary gets more.

1. **Bank aspects — select.** Use only the sections for the confirmed focus(es) and plus responsibility. For each aspect:
   - **Mandatory** questions are always selected and count toward its allocation.
   - Fill the remaining places with **Optional** questions that best fit the focuses confirmed in Step 5, each with a one-line rationale tied to this candidate or JD (e.g. "probes the Partial rating on stakeholder management", "JD stresses regulatory change").

   Keep each question's ID; light rewording to fit the JD's domain is fine, but don't write new questions for these aspects. If a section's Mandatory questions exceed its allocation, keep the allocation, select the Mandatory questions in bank order, and flag the bank for correction.
2. **Candidate assessment — generate.** After selecting the bank questions, create **5 scenario-based questions** that verify the gaps, areas needing improvement, and insufficiencies identified in Step 4, calibrated to the met seniority level. They must not repeat or paraphrase any selected bank question — where a gap overlaps a selected question's topic, take a different angle, e.g. anchor the scenario in the candidate's own resume claims, probe how they'd handle a complication or failure rather than the standard approach, or combine the gap with another competency in one situation.
3. **Mark must-ask questions (★)** — every Mandatory bank question plus all 5 scenario questions. Optional questions are backups to use as time allows.

Present all 26 questions as one table — bank questions first, then the scenario questions:

| ★ | Aspect | ID | Type | Question | Strong Answer Includes | Rationale |
|---|---|---|---|---|---|---|

- **Bank questions:** Type is "Mandatory" or "Optional"; Strong Answer Includes is copied from the bank, including any **Perspective** note.
- **Scenario questions:** Aspect is "Candidate assessment", IDs run SC-01 to SC-05, and Type is "Scenario". Rationale names the gap or area to verify and the assessment evidence behind it.

## Step 7 — Interview notices

Highlight areas needing interviewer attention for fairness, depth, and decision confidence — any ambiguity, resume inconsistencies, or evidence limitations to probe live, including any focus or the plus responsibility the resume leaves unclear.

## Step 8 — Confirm and save the interview pack (hard stop)

Ask the user to confirm the question table and interview notices, or to request changes. **Wait for confirmation** before writing the file; apply any requested changes first.

Once confirmed, write the pack to `references/interview-candidate-data/interview-question-<candidate-name>.md` (candidate name in lowercase, hyphenated). If the file already exists, ask before overwriting it. The file contains:

1. A short header: candidate, position, role positioning, met seniority, interview scope (including any aspects covered by another interviewer), and question allocation.
2. The Step 6 question table.
3. The Step 7 interview notices.

The pack has no Document Control & Revision History section and no update mode — re-running the skill produces a new pack.
