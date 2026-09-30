---
name: generate-prd
description: Create a new Product Requirements Document (PRD) or update an existing one, built from a BRD and/or other supplementary source material (Confluence pages, SharePoint/OneDrive files, local files), or purely from conversation when no source documents exist. Use when the user asks to create/draft/generate a PRD, write a PRD from existing files, or update/revise an existing PRD.
---

# Generate PRD

Produces or updates a Product Requirements Document that stays at the **product/capability level**. It is deliberately NOT a functional spec: detailed functional requirements, user stories, NFRs, data/integration specs, acceptance criteria, and BRD-traceability matrices belong to a separate, later artifact — do not add them to the PRD even if source material contains that level of detail. Summarize it up to capability level instead.

The PRD template lives at `templates/prd-template.md` in this project. Always read that file first to get the current section structure — do not hardcode the structure from memory, in case the template has been edited.

All output files are written inside this project, under `outputs/<project-code>-PRD.md`. Never write PRDs anywhere else (not to the user's home directory, Desktop, or another project).

## Step 0 — Determine mode: create or update

Ask (or infer from the user's request) whether this is:
- **Create**: a new PRD, no existing PRD file yet.
- **Update**: an existing PRD file already exists and needs to be revised.

If the user references an existing `outputs/*-PRD.md` file, or an existing PRD is otherwise supplied/linked, treat it as **Update**. Otherwise treat it as **Create**.

## Create mode

1. **Gather source material.** Ask the user what's available if not already provided or attached. Any combination of the following is valid, including none at all:
   - A BRD — local file (.docx/.pdf/.md/.txt), a Confluence page link, or a SharePoint/OneDrive link.
   - Additional supplementary files (meeting notes, research, existing specs, emails, etc.) in any of the same formats.
   - Nothing at all — pure conversational input.

   Route each source by type:
   - Local file → use `Read`, or the `docx`/`pdf` skills for those formats.
   - Confluence link → use the Atlassian Rovo MCP tools (e.g. `getConfluencePage`) to fetch content.
   - SharePoint/OneDrive link → use the `msgraph` skill to fetch the file/content.

2. **Multi-source handling — equal priority, flag every conflict.** Do not treat the BRD (or any other source) as automatically overriding another source. If two sources disagree on anything relevant to the PRD (e.g. differing scope statements, differing target users, differing goals), do not silently pick one — record the conflict verbatim as an entry under Open Questions, naming both sources and what each says.

3. **Gap handling — interview, don't guess.** For any PRD section that no source material addresses (including the fully conversational, no-file case), ask the user targeted questions specific to that section rather than fabricating or inferring content:
   - Purpose & Background → "What problem or business need is driving this?"
   - Goals & Success Metrics → "What does success look like? Any target metrics/KPIs?"
   - Scope → "What's explicitly in scope vs. out of scope?"
   - Assumptions/Constraints/Dependencies → "Any known constraints, dependencies on other teams/systems, or assumptions being made?"
   - Target Users/Personas → "Who is this for?"
   - Key Features/Capabilities → "At a high level, what should this product/feature be able to do?"
   - Release/Phasing → "Is there a phased rollout, or an MVP vs. later scope?"
   - Risks & Mitigations → "Any known risks?"
   Do not invent answers to these. If the user doesn't know or declines to answer, leave the section noted as an Open Question rather than filling it in.

4. **Draft the PRD** following the section structure in `templates/prd-template.md` exactly, in Markdown.

5. **Get the project code.** If not inferable from the source material (e.g. a Jira key or internal project/product code mentioned in the BRD), ask the user for it. Use it for the document title and the output filename.

6. **Write the output** to `outputs/<project-code>-PRD.md` in this project (create the `outputs/` folder if it doesn't exist). Set Document Control version to `1.0` with a first Revision History row: "Initial draft" and an appropriate trigger/reason (e.g. "Created from BRD", "Created from conversational input").

7. **Summarize for the user** (in chat, not in the document itself): what content came from which source, what was gathered via interview, and what's left as an open question — so it's easy to sanity-check before sharing with the PO.

## Update mode

1. **Locate the existing PRD.** Read its full current content and note its current version number from the Revision History table.

2. **Gather what's driving the update**, using the same flexible input handling as Create mode (a revised BRD, new supplementary files, or a conversational description of the change). Apply the same equal-priority, flag-every-conflict rule — now also checking new input against the *existing PRD's* current content, not just against other new sources.

3. **Apply changes only to the affected sections**, leaving everything else in the document unchanged.

4. **Bump the version and log the change** in the Revision History table: increment the version (e.g. 1.0 → 1.1 for a minor update, or 1.0 → 2.0 for a major scope change — use judgment, ask the user if unclear), add a row with the date, a plain-language description of what changed, and the trigger/reason.

5. **Write the updated file back** to the same `outputs/<project-code>-PRD.md` path.

6. **Summarize the delta for the user**: what changed, what stayed the same, and any new open questions the update raised.
