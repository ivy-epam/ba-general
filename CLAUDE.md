# Project guidelines

Rules for how skills in `.claude/skills/` and templates in `templates/` are written, and for how every skill behaves when it runs. Skills state only what is specific to them; anything here is not repeated in each skill. **Where a skill explicitly says otherwise, the skill wins** (e.g. `generate-case-study` has no update mode or versioning; `assess-candidate` writes its interview pack to `references/interview-candidate-data/` with no versioning).

## Writing skills and templates

- **Skills hold the rules; templates hold the structure.** Each rule lives in exactly one place.
  - **Skill** (`.claude/skills/<name>/SKILL.md`): how to work — intake questions, research, confirmation gates, and every drafting rule (what to include or omit, naming, sourcing, marking, numbering).
  - **Template** (`templates/<name>-template.md`): what the output looks like — sections and their order, table columns, short `{{placeholders}}` describing what goes in each field, format examples, and text meant for the document's readers (section intros, legends, notation keys).
  - **Not in templates:** writer instructions — no guidance comments, and no rules inside placeholders or intros. When a rule is needed, add it to the skill.
- **Industry-neutral.** Skills, templates, and references must work for any client or industry. Don't build in rules, terminology, or assumptions from one industry or engagement (e.g. B2B pricing, insurance, a specific client's systems). Where an example helps, use a generic one, or several from different domains. Client- and industry-specific content belongs only in `outputs/`, `docs/`, and `case-study/`.

## Templates

- If a skill names a template under `templates/`, always read that template first to get the current section structure — do not hardcode the structure from memory, in case the template has been edited.

## Sourcing

- **No fabrication.** Every fact, flow step, rule, grant, or reference must trace to a source document or to something the user stated in the conversation (interview). Never invent, infer, or design content on the user's behalf. Anything unconfirmed goes to the document's **Open Questions** section instead of being filled in — or, where a skill tracks assumptions, is recorded as an assumption.
- **Interview only to fill gaps.** Source documents named by the skill come first; ask the user only for what they don't establish. A missing source document is not a blocker — skip it and cover that gap by interview.
- **Confirm before finalizing anything inferred.** When a skill proposes inferred content (candidate use cases, story splits, CRUD grants, NFRs, test candidates, etc.), present the proposal and wait for the user's confirmation, correction, or removal. Never add inferred content silently.

## Output

- **Write only to the skill's stated output path**, inside this project — never anywhere else (not the user's home directory, Desktop, or another project). Create the output folder if it doesn't exist.
- **Updates change only the affected sections**; leave everything else in the document unchanged.

## Versioning

- **Placement:** Document Control & Revision History is always the last section of a document.
- **Create:** set version `1.0` with a first Revision History row — "Initial draft", plus the trigger/reason where the template has a column for it (e.g. "Created from BRD").
- **Update:** bump the version — minor (1.0 → 1.1) for small changes, major (1.0 → 2.0) for a significant scope change; ask the user if unclear — and add a Revision History row with the date, a plain-language description of what changed, and the trigger/reason where the template has a column for it.
- **One row per day:** if the latest Revision History row has today's date, don't add a row or bump the version — fold the new changes into that row's description (still concise) and keep its version, unless today's change is major, in which case raise that row's version to the next major. Only a change on a different date gets a new row and a version bump. Skill steps that say "bump the version" follow this rule.
- **Keep Revision History rows concise:** one line, about 25 words or fewer, listing only the key changes as short phrases separated by semicolons. Leave out rationale, definitions, and detail that already lives in the document body. Example: "Interview follow-up: two entities added; key attribute confirmed; one rule removed".

## Summaries

- **Summaries go in chat, never in the document**, and never restate the full document.
- **Create runs:** summarize what came from which source, what was gathered via interview, and what's left as an Open Question — plus anything the skill specifically asks for.