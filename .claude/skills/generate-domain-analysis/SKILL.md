---
name: generate-domain-analysis
description: Create or update a research-led domain analysis for a product — a primer on the specific sector of the domain the product sits in (e.g. wealth management within banking), the product's data model (entities, keys, relationships, rules), its system landscape, and the decisions and assumptions behind it. Use when the user asks to model the domain, identify entities/relationships, build an ontology, or create an entity-relationship model for a project.
---

# Generate Domain Analysis (Research-Led, Ontology-Based)

Produces or updates `outputs/<client>-<project-code>-domain-analysis.md`, organised from broad to narrow: Sector → Product → System Landscape → Supporting Information. Keyed by project code, shared with the PRD (`outputs/<project-code>-PRD.md`).

**Sector, not domain:** the analysis covers one specific sector of a domain, never the domain as a whole, and the document says so wherever it frames its subject. The **domain** is the industry the client operates in; the **sector** is the line of business within it that the product serves (e.g. Banking → wealth management / retail investment; Electrical equipment manufacturing → B2B sales). A channel such as e-commerce is how that business is done, not the domain or sector — unless commerce is the client's own business (e.g. a marketplace operator).

**Division of labour with the PRD:** Part 1 (Sector) educates the reader about the sector and stays product-agnostic. Part 2 (Product) is a provisional, high-level product model — often written before the PRD exists and before the user has complete or correct product information. Feature detail, requirements, and phasing belong in the PRD, never in Part 2. The PRD is cross-checked against Part 2 (see the alignment map in Step 2.2), and Part 2 is corrected through this skill's update mode.

**Why research-led:** the user knows scope and outcomes, not every entity and cardinality. The user sets the boundaries; the skill researches, explains, proposes, and asks only for confirmation and a few decisions.

**Vocabulary (consistent across runs):**
- **Entity** — a business object that passes two tests (e.g. Customer, Policy, Invoice; attributes alone aren't required):
  1. **Relevant to the core journey** — the user acts on or views it, or the journey can't complete without it.
  2. **Independent** — it has its own identity (what tells one instance from another, giving it a key), its own lifecycle (created, changes, ends), and relationships an attribute can't express.

  Relevant and independent → entity. Relevant but not independent (a value, type, status, lifecycle stage, or reference value such as a price) → attribute of the entity it describes. Not relevant → excluded, whether independent or not. Every relevant item must land as an entity or an attribute; none is dropped.
- **Sub-entity** — an entity that has its own identity and lifecycle but can't exist without one parent entity (e.g. an order line within an order, a saved list within a user profile). Its key includes or borrows the parent's key, and it is deleted with the parent. Entities are tier 1 and sub-entities tier 2 in Entities Inventory; omit the tier-2 table when there are none. Tier-1 IDs run E01, E02, …; a sub-entity takes its parent's ID plus its own sequence (E01.1, E01.2), so the ID shows which entity it belongs to.
- **Attribute** — a typed field on an entity.
- **Relationship** — a verb-phrase connection between two entities, with cardinality.
- **Taxonomy** — subtypes, only when a source names them *and* each adds attributes or relationships of its own; otherwise the distinction is an attribute of the parent.
- **Constraint** — a structural rule on entity existence or relationships. Process/workflow rules belong in Feature Analysis. Individuals/instances are out of scope.

**Sourcing discipline:**
- **Tag rows** with Source Type and Status (`Confirmed` by the user / `Proposed`). Source Types:
  - `Doc: <file §>` — read from existing documents or files in the repo.
  - `Interview` — stated or confirmed by the user, whatever source they gathered it from.
  - `Research [R#]` — found by the skill's own web search, cited in Reference Sources.

  Attributes, Relationships, and System Landscape omit these columns; mark unconfirmed items there with † and list each as an assumption (A#).
- **Cite research** only from live web search, never unstated model knowledge.
- **No silent merging:** list similar names from different sources separately and flag them in Open Questions unless the user confirms they match.
- **Client terminology wins:** name entities as the client does, not as research sources do; note the industry equivalent in the description.
- **Cardinality without evidence:** give the likely value and record it as an assumption.

**Rules:** independent of `generate-rbac` (no enforced naming consistency). Template: `templates/domain-analysis-template.md`.

## Step 0 — Determine mode

Identify the client (from the request or project docs; ask if unknown) as a lowercase, hyphenated name (e.g. `acme-corp`), and the project code — reuse it from an existing `outputs/<project-code>-PRD.md` when there is one, otherwise ask. Then check whether `outputs/*-<project-code>-domain-analysis.md` exists: **no** → Create (Step 1); **yes** → Update (Step 2).

## Step 1 — Create mode

### Step 1.1 — Read project docs

If project material exists (e.g. `docs/<project>/`, a case study), read it first and prefill whatever it answers in Step 1.2, so the user only confirms or corrects. If `outputs/<project-code>-PRD.md` exists, prefill Scope & Context, Constraints, and Systems from it per the alignment map (Step 2.2), tagged `Doc: PRD §n`.

### Step 1.2 — Scope intake (one round)

Ask, in a single round, only for:
- **Domain and sector** — as defined under *Sector, not domain* above. Propose the pair from project docs and research, and ask only to confirm.
- **Client name** — only if Step 0 didn't establish it. If the user prefers not to disclose it, research falls back to industry and competitor sources.
- **Product and its scope** — the product or system being modelled, and the boundaries of this engagement (e.g. deployment, region, product line).
- **End users / personnel** — who uses or operates the process.
- **Journeys & use cases** — the in-scope journeys and, within each, the key things users need to accomplish (high-level, not step-by-step); record use cases grouped under their journey.
- **Inputs and outputs / ultimate outcomes** — what enters the process and what it ultimately produces. Don't ask about the steps in between — the research fills those in.
- **Out of scope** — the product's boundary: the neighbouring capabilities, processes, and systems that sit outside the product (e.g. handled by another system or team). Don't list features the product could include but this release defers — out of scope draws the product's edge, not a feature cut.
- **Constraints** — regulatory, regional, product-line, or other business boundaries.
- **Systems** — which systems take part in the in-scope journeys, which are in scope versus integration-only, which owns each kind of data, and which data flows into and out of the product. Prefill from architecture or integration docs where available. Don't ask for user flows, screens, or APIs — those belong to `generate-feature-analysis` and `generate-use-cases`.

Don't ask about entities, attributes, relationships, or cardinality yet.

### Step 1.3 — Research (live web search)

Research in two passes, sector first.

**1.3a — Sector.** Before any product research, build a sector map covering:
1. **Scope** — what the sector covers within its domain, and the adjacent sectors.
2. **Participants** — the businesses involved and their roles (e.g. providers, customer segments, intermediaries, infrastructure, regulators).
3. **Offerings** — the core product or service categories the sector trades.
4. **Transactions** — what passes between participants, how value and money flow, and the core lifecycle.
5. **Risk and regulation** — the main risks and the regulatory frame governing the sector.

Derive the core concepts from the map (rules in Step 1.5).

**1.3b — Product.** Search for how the in-scope process is modelled in practice.

For both passes, prefer higher tiers when sources conflict:
1. **Client official** — the client's websites, product pages, help centers, user guides, public documentation.
2. **Industry official** — sector regulators, industry associations, standards bodies, official references, and the documentation of the systems of record the sector relies on (e.g. SAP for order-to-cash, HL7 FHIR for healthcare, FIBO for banking, GS1 for supply chain).
3. **Competitor** — official sites/docs of reputable competitors with comparable products.

Record each source's ID, title, and URL. Avoid secondary blogs or forums when a tier-1–3 source covers the point; if only weaker sources exist, say so.

### Step 1.4 — Confirmation gate (hard stop before drafting)

Present a research brief in chat and **wait for confirmation**:
- **Scope recap** — the Step 1.2 answers as understood, flagging any source conflict on which system owns or supplies what.
- **Sector map** — scope, participants, offerings, transactions, and risk and regulation, as short bullets with source IDs.
- **Proposed core concepts** — grouped and ordered as they will appear, one line each, with source IDs.
- **Modelling summary** — how the sector typically models the in-scope process, and where implementations differ, with source IDs.
- **Candidate entities** — only those passing both entity tests, each with name, one-line description, source, and parent if it's a sub-entity; possible duplicates flagged. Relevant items that aren't independent are listed as attributes of their entity.
- **Decision points** — at most 8, only where industry practice varies *and* the choice changes the model (e.g. "Is a saved draft persisted or session-only?"). Multiple choice, industry-typical option first as the default.
- **Key sources** — the main references, by tier.

Invite the user to correct scope and the sector map, add or remove core concepts and entities, confirm merges, and answer decision points — including **why**, since each decision records its reason. An unanswered decision point keeps its default and is recorded as an assumption.

### Step 1.5 — Draft the model

Follow the template's structure, applying these rules:
- **Structure:** four parts, broad to narrow — **Sector** (Sector Primer), **Product** (Scope & Context through Business Rules), **System Landscape**, **Supporting Information** (Decisions & Assumptions, Open Questions, Reference Sources, Document Control & Revision History last). Domain, sector, client, product with its scope, and project code with its PRD link go in the header table — the Domain and Sector rows name the domain and the sector only, never the product or its offerings; the Client row gives the client's name only, with no business unit or division; and the Product row defines in brackets any short name used later. The title is "{Client} {Product} ({scope}) — {Sector}", with the sector qualified by its domain when the sector alone doesn't say whose business it is (e.g. "Electrical Equipment B2B Sales", not "B2B Sales"). Omit Entity Taxonomy, Business Rules, or Open Questions when they have no content. Number sections sequentially and cross-reference them by name, not number. Keep each section's content to its part's layer.
- **Sector Primer — sector-level only:** no client or product names or choices; reusable for any client in the same sector. Never name competitors or brands in the prose; cite them by source ID only (e.g. "comparable platforms track shipments [R3]") — names appear only in Reference Sources.
  - **Plain language** throughout the Sector Primer, for a reader new to the sector: everyday words, short sentences, abbreviations spelled out, and every term the reader needs explained in a few words where it first appears (in italics). Use the trade term only when the reader will meet it again in the document or at work.
  - *Sector overview* condenses the sector map into Scope, Participants, and Core transactions — one bullet each, with short sub-bullets where a list reads better (e.g. one per participant, saying what it does); offerings and regulation are left to the core concepts.
  - *Core concepts* are the sector's foundational, critical concepts, derived from the sector map — what a newcomer must grasp to understand how the sector works. Each is business-focused and high level: what it is and why it matters in the sector, in 2–3 short sentences; about 8–12 in total. Group labels and concept names are plain too (e.g. "From order to payment", not "Order-to-cash").
    - **Include** a concept that is foundational to the sector even if the product doesn't touch it; leave out what only one product or player does. **Exclude** product features and UI (e.g. saved lists, dashboards) and system mechanics (e.g. holds, status codes, calculations) — both belong under *How the sector typically models this*, or in Business Rules.
    - **Group** as nested bullets in sector-map order — sector & participants → offerings → transactions & lifecycle → risk & regulation — each group label worded for the sector (e.g. "Investment offerings"); omit an empty group. Within a group, run broad to specific; transactions follow lifecycle order.
    - **Jurisdiction:** state concepts in market-neutral terms; where the scope names a market, add a short "In <market>: …" note to the concept it affects.
  - *How the sector typically models this* is short bullets, each led by a bold summary — no diagram.
  - *Common variations* lists the options only, ending with a pointer to Decisions & Assumptions.
  - Check that every Input and Constraint in Scope & Context is reflected in the primer — as a core concept only if it is foundational to the sector, otherwise under modelling or variations — and, where it shapes structure, in the model.
- **Scope & Context — business-level only:** which system supplies each input, and which owns what, belong in System Landscape.
- **Domain Model Diagram:** Mermaid `classDiagram` with keys only — `PK <attribute>`, `FK <Entity>` or `FK <Entity>.<key>`, `PK identifier TBD` when not captured; no other attributes and no parentheses inside classes. Verb- and cardinality-labelled edges (e.g. `Customer "1" -- "0..*" Invoice : receives`), `<|--` for subtypes, `*--` from parent to sub-entity, dashed links (`..`) for assumed relationships, a one-line legend above. Space-free class names.
- **Attributes:** one line per entity, in Entities Inventory order (entities with identical attributes may share a line) — attributes separated by " · ", PK marked inline, types and notes only where not obvious, citing C#/D#/OQ # instead of explaining. No foreign keys (they follow from Relationships). Never invent an identifier: list entities without one once in the section intro and raise an Open Question.
- **Relationships:** a level-1 bullet per area, relationships as level-2 bullets — `Entity A → **verb phrase** → Entity B` followed by its `A : B` cardinality (`1`, `0..1`, `1..*`, `0..*`) and a short qualifier if needed. Label relationships that follow from others "derived, not stored".
- **Business Rules:** where an entity has alternative optional parents, add a rule that it belongs to exactly one of them.
- **System Landscape:** only systems in the in-scope journeys. A Systems table (role, in scope, system of record) and Data flows grouped as Upstream, Downstream, and — if needed — Unclear, naming the entities each flow carries. State the source of integration types and that they're unconfirmed until the technical team checks them. Inferred flows get † and an assumption; unknown ones get an Open Question.
- **Decisions & Assumptions:** under *Decided*, one bold line per decision naming the rejected alternative, then *Why* — never invent a reason; a missing one is "to be confirmed" with an Open Question, where a proposed reason can be offered. Under *Assumptions*, anything the model relies on without confirmation (every † item, Proposed rules, working answers), each with what would confirm it.
- **Open Questions:** only items with no working answer at all; remove each once answered.
- **Reference Sources:** one bullet per source in ID order — the ID and the linked title only.
- **IDs** (E#, C#, D#, A#, OQ #): sequential. When an item is removed, renumber the rest and update every reference — no "retired" placeholders.

### Step 1.6 — Write output

Write to `outputs/<client>-<project-code>-domain-analysis.md` with Status: Draft. The first Revision History row summarises the scope (e.g. "Initial research-led domain analysis for <journeys>").

### Step 1.7 — Summary

Also cover: entity, attribute, relationship, and constraint counts (Confirmed vs Proposed) and the number of assumptions; which sources carried the most weight; pending decisions and the highest-impact open questions.

## Step 2 — Update mode

### Step 2.1 — Read the existing file

Note its version, last Revision History row, and current Scope & Context and System Landscape. If the file predates the sector structure (e.g. "Part 1 — Domain" with a Domain Primer), propose rebuilding Part 1 — domain and sector per *Sector, not domain*, sector research, Sector overview, and grouped core concepts — at the Step 2.4 gate; this is a major change.

### Step 2.2 — Understand what's driving the update

Ask what changed: new journeys or scope, new or changed systems or data flows, answers to pending decisions, assumptions, or open questions, new constraints, a request to deepen research, or a PRD created or updated. Use the Step 1.2 questions only for what's new.

**PRD created or updated:** read `outputs/<project-code>-PRD.md` and compare it with Part 2 using the alignment map below — high-level fields only; the PRD's detail stays in the PRD. Present each mismatch at the Step 2.4 gate. Neither document wins automatically: a mismatch the user resolves is applied with Source Type `Doc: PRD §n` and Status `Confirmed`; an unresolved one becomes an Open Question naming both sources and what each says.

**Alignment map** (also used by `generate-prd` for its cross-check):

| Domain analysis | PRD |
|---|---|
| Scope & Context — End Users / Personnel | Target Users / Personas |
| Scope & Context — Journeys & Use Cases | Key Features / Capabilities Overview |
| Scope & Context — Out of Scope (product boundary) | Scope — Out of scope |
| Scope & Context — Constraints | Assumptions, Constraints & Dependencies — Constraints |
| System Landscape — Systems | Assumptions, Constraints & Dependencies — Dependencies |
| Entity names (Entities Inventory) | Glossary terms |

### Step 2.3 — Targeted research

Run Step 1.3 only for what's new: the sector pass (1.3a) when the sector or market changes or Part 1 is being rebuilt, and the product pass (1.3b) for new or changed product scope. Reuse existing source IDs; append new ones.

### Step 2.4 — Confirmation gate (hard stop before drafting)

Present the delta brief per Step 1.4: scope change, sector map and core concept changes, primer additions, new or changed candidate entities, new decision points, and items moving to `Confirmed`. Flag possible duplicates against existing entities. Wait for confirmation.

### Step 2.5 — Reconcile and draft

Apply the Step 1.5 rules, and:
- **New entity:** add it to Entities Inventory, the diagram (keys), Attributes, and Relationships.
- **Existing entity:** extend its attributes and relationships; never duplicate it.
- **Similar-but-not-identical names:** add separately and flag under Open Questions unless the user confirmed the merge.
- **Validated items:** change Status to `Confirmed` and add `Interview` to Source Type.
- **Decisions:** record each under *Decided* with its reason.
- **Assumptions confirmed:** remove the assumption, drop its †, and update the model; answered open questions are removed. Renumber per the IDs rule.
- **Extend** the Sector Primer and System Landscape to cover new content; a new core concept goes into its group per the Step 1.5 rules.

### Step 2.6 — Bump version and write back

Refinements and validations are minor; a structural change is major. Overwrite `outputs/<client>-<project-code>-domain-analysis.md`.
