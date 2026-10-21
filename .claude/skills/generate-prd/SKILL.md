---
name: generate-prd
description: Create a new Product Requirements Document (PRD) or update an existing one, built from a BRD and/or other supplementary source material (Confluence pages, SharePoint/OneDrive files, local files), or purely from conversation when no source documents exist. Use when the user asks to create/draft/generate a PRD, write a PRD from existing files, or update/revise an existing PRD.
---

# Generate PRD

Produces or updates a Product Requirements Document that stays at the **product/capability level**. It is deliberately NOT a functional spec: detailed functional requirements, user stories, NFRs, data/integration specs, acceptance criteria, and BRD-traceability matrices belong to a separate, later artifact — do not add them to the PRD even if source material contains that level of detail. Summarize it up to capability level instead.

The PRD template lives at `templates/prd-template.md` in this project.

Output: `outputs/<project-code>-PRD.md`.

**Working with the domain analysis:** a domain analysis for the same project code (`outputs/*-<project-code>-domain-analysis.md`) may already exist. Its Part 1 explains the domain; its Part 2 is a provisional high-level product model. The PRD holds the product detail, and is cross-checked against Part 2 so the two agree at a high level. This skill never edits the domain analysis — `generate-domain-analysis` applies any corrections in its update mode. Don't rebuild the entity model in the PRD.

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

   Also read the domain analysis for this project code, if it exists, as one of the equal-priority sources. Use Part 1 to understand the domain and ask better-informed gap questions, without restating it; use Part 2's entity names in the PRD so the vocabulary stays consistent; and point the Glossary to the domain analysis for domain concepts instead of copying them.

   Route each source by type:
   - Local file → use `Read`, or the `docx`/`pdf` skills for those formats.
   - Confluence link → use the Atlassian Rovo MCP tools (e.g. `getConfluencePage`) to fetch content.
   - SharePoint/OneDrive link → use the `msgraph` skill to fetch the file/content.

2. **Multi-source handling — equal priority, flag every conflict.** Do not treat the BRD (or any other source) as automatically overriding another source. If two sources disagree on anything relevant to the PRD (e.g. differing scope statements, differing target users, differing goals), do not silently pick one — record the conflict verbatim as an entry under Open Questions, naming both sources and what each says. This includes the domain analysis: compare the PRD with its Part 2 field by field using the alignment map in `generate-domain-analysis` (Step 2.2), and record each mismatch the same way.

3. **Gap handling.** For any PRD section that no source material addresses (including the fully conversational, no-file case), ask the user targeted questions specific to that section:
   - Purpose & Background → "What problem or business need is driving this?"
   - Goals & Success Metrics → "What does success look like? Any target metrics/KPIs?"
   - Scope → "What's explicitly in scope vs. out of scope?"
   - Assumptions/Constraints/Dependencies → "Any known constraints, dependencies on other teams/systems, or assumptions being made?"
   - Target Users/Personas → "Who is this for?"
   - Key Features/Capabilities → "At a high level, what should this product/feature be able to do?"
   - Release/Phasing → "Is there a phased rollout, or an MVP vs. later scope?"
   - Risks & Mitigations → "Any known risks?"

4. **Draft the PRD** following the section structure in `templates/prd-template.md` exactly, in Markdown.

5. **Get the project code.** Reuse it from an existing domain analysis for this project, if any. Otherwise, if not inferable from the source material (e.g. a Jira key or internal project/product code mentioned in the BRD), ask the user for it. Use it for the document title and the output filename.

6. **Write the output** to `outputs/<project-code>-PRD.md` (trigger e.g. "Created from BRD", "Created from conversational input").

7. **Summarize for the user** — so it's easy to sanity-check before sharing with the PO. Where a domain analysis exists, add a **Domain analysis alignment** list: each mismatch with Part 2, and any new product concept the PRD introduces that Part 2 lacks. Recommend running `generate-domain-analysis` in update mode with the PRD as the trigger.

## Update mode

1. **Locate the existing PRD.** Read its full current content and note its current version number from the Revision History table.

2. **Gather what's driving the update**, using the same flexible input handling as Create mode (a revised BRD, new supplementary files, or a conversational description of the change). Apply the same equal-priority, flag-every-conflict rule — now also checking new input against the *existing PRD's* current content, not just against other new sources.

3. **Apply changes, bump the version, and write back** to the same `outputs/<project-code>-PRD.md` path.

4. **Summarize the delta for the user:** what changed, what stayed the same, and any new Open Questions — plus the Domain analysis alignment list, as in Create mode.