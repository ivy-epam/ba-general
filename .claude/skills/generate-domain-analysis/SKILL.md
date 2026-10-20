---
name: generate-domain-analysis
description: Create or update a research-led domain analysis for a product — a domain primer, the product's data model (entities, keys, relationships, rules), its system landscape, and the decisions and assumptions behind it. Use when the user asks to model the domain, identify entities/relationships, build an ontology, or create an entity-relationship model for a project.
---

# Generate Domain Analysis (Research-Led, Ontology-Based)

Produces or updates `outputs/<client>-domain-analysis.md`, organised from broad to narrow: Domain → Product → System Landscape → Supporting Information.

**Why research-led:** the user knows scope and outcomes, not every entity and cardinality. The user sets the boundaries; the skill researches, explains, proposes, and asks only for confirmation and a few decisions.

**Vocabulary (consistent across runs):**
- **Entity** — a core business object with its own identity, lifecycle, or relationships (e.g. Customer, Policy, Invoice). Attributes alone aren't required.
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

Identify the client (from the request or project docs; ask if unknown) as a lowercase, hyphenated name (e.g. `acme-corp`), then check whether `outputs/<client>-domain-analysis.md` exists: **no** → Create (Step 1); **yes** → Update (Step 2).

## Step 1 — Create mode

### Step 1.1 — Read project docs

If project material exists (e.g. `docs/<project>/`, a PRD, a case study), read it first and prefill whatever it answers in Step 1.2, so the user only confirms or corrects.

### Step 1.2 — Scope intake (one round)

Ask, in a single round, only for:
- **Domain / industry** — the business domain the product sits in.
- **Client name** — if not already shared. If the user prefers not to disclose it, research falls back to industry and competitor sources.
- **Product and its scope** — the product or system being modelled, and the boundaries of this engagement (e.g. deployment, region, product line).
- **End users / personnel** — who uses or operates the process.
- **Journeys & use cases** — the in-scope journeys and, within each, the key things users need to accomplish (high-level, not step-by-step); record use cases grouped under their journey.
- **Inputs and outputs / ultimate outcomes** — what enters the process and what it ultimately produces. Don't ask about the steps in between — the research fills those in.
- **Out of scope** — what is explicitly excluded.
- **Constraints** — regulatory, regional, product-line, or other business boundaries.
- **Systems** — which systems take part in the in-scope journeys, which are in scope versus integration-only, which owns each kind of data, and which data flows into and out of the product. Prefill from architecture or integration docs where available. Don't ask for user flows, screens, or APIs — those belong to `generate-feature-analysis` and `generate-use-cases`.

Don't ask about entities, attributes, relationships, or cardinality yet.

### Step 1.3 — Research (live web search)

Search for how the in-scope process is modelled in practice, preferring higher tiers when sources conflict:
1. **Client official** — the client's websites, product pages, help centers, user guides, public documentation.
2. **Industry official** — standards bodies, official references, and the documentation of the systems of record the domain relies on (e.g. SAP for order-to-cash, HL7 FHIR for healthcare, FIBO for banking, GS1 for supply chain).
3. **Competitor** — official sites/docs of reputable competitors with comparable products.

Record each source's ID, title, and URL. Avoid secondary blogs or forums when a tier-1–3 source covers the point; if only weaker sources exist, say so.

### Step 1.4 — Confirmation gate (hard stop before drafting)

Present a research brief in chat and **wait for confirmation**:
- **Scope recap** — the Step 1.2 answers as understood, flagging any source conflict on which system owns or supplies what.
- **Domain primer (summary)** — core concepts, how the industry typically models them, and where implementations differ, with source IDs.
- **Candidate entities** — name, one-line description, source; possible duplicates flagged.
- **Decision points** — at most 8, only where industry practice varies *and* the choice changes the model (e.g. "Is a saved draft persisted or session-only?"). Multiple choice, industry-typical option first as the default.
- **Key sources** — the main references, by tier.

Invite the user to correct scope, add or remove entities, confirm merges, and answer decision points — including **why**, since each decision records its reason. An unanswered decision point keeps its default and is recorded as an assumption.

### Step 1.5 — Draft the model

Follow the template's structure, applying these rules:
- **Structure:** four parts, broad to narrow — **Domain** (Domain Primer), **Product** (Scope & Context through Business Rules), **System Landscape**, **Supporting Information** (Decisions & Assumptions, Open Questions, Reference Sources, Document Control & Revision History last). Domain, client, and product with its scope go in the header table — the Domain row names the domain only, not the product, and the Product row defines in brackets any short name used later. The title is "{Client} {Product} ({scope}) — {Domain}". Omit Entity Taxonomy, Business Rules, or Open Questions when they have no content. Number sections sequentially and cross-reference them by name, not number. Keep each section's content to its part's layer.
- **Domain Primer — industry-level only:** no client or product names or choices. *Core concepts* cover the practices, business rules, and standards any player in the domain follows, not only the system mechanisms behind them. *How the industry typically models this* is short bullets, each led by a bold summary — no diagram. *Common variations* lists the options only, ending with a pointer to Decisions & Assumptions. Never name competitors or brands in the prose; cite them by source ID only (e.g. "comparable platforms track shipments [R3]") — names appear only in Reference Sources. Check that every Input and Constraint in Scope & Context is reflected in the primer and, where it shapes structure, in the model.
- **Scope & Context — business-level only:** which system supplies each input, and which owns what, belong in System Landscape.
- **Domain Model Diagram:** Mermaid `classDiagram` with keys only — `PK <attribute>`, `FK <Entity>` or `FK <Entity>.<key>`, `PK identifier TBD` when not captured; no other attributes and no parentheses inside classes. Verb- and cardinality-labelled edges (e.g. `Customer "1" -- "0..*" Invoice : receives`), `<|--` for subtypes, dashed links (`..`) for assumed relationships, a one-line legend above. Space-free class names.
- **Attributes:** one line per entity, in Entities Inventory order (entities with identical attributes may share a line) — attributes separated by " · ", PK marked inline, types and notes only where not obvious, citing C#/D#/OQ # instead of explaining. No foreign keys (they follow from Relationships). Never invent an identifier: list entities without one once in the section intro and raise an Open Question.
- **Relationships:** a level-1 bullet per area, relationships as level-2 bullets — `Entity A → **verb phrase** → Entity B` followed by its `A : B` cardinality (`1`, `0..1`, `1..*`, `0..*`) and a short qualifier if needed. Label relationships that follow from others "derived, not stored".
- **Business Rules:** where an entity has alternative optional parents, add a rule that it belongs to exactly one of them.
- **System Landscape:** only systems in the in-scope journeys. A Systems table (role, in scope, system of record) and Data flows grouped as Upstream, Downstream, and — if needed — Unclear, naming the entities each flow carries. State the source of integration types and that they're unconfirmed until the technical team checks them. Inferred flows get † and an assumption; unknown ones get an Open Question.
- **Decisions & Assumptions:** under *Decided*, one bold line per decision naming the rejected alternative, then *Why* — never invent a reason; a missing one is "to be confirmed" with an Open Question, where a proposed reason can be offered. Under *Assumptions*, anything the model relies on without confirmation (every † item, Proposed rules, working answers), each with what would confirm it.
- **Open Questions:** only items with no working answer at all; remove each once answered.
- **Reference Sources:** one bullet per source in ID order — the ID and the linked title only.
- **IDs** (E#, C#, D#, A#, OQ #): sequential. When an item is removed, renumber the rest and update every reference — no "retired" placeholders.

### Step 1.6 — Write output

Write to `outputs/<client>-domain-analysis.md` with Status: Draft. The first Revision History row summarises the scope (e.g. "Initial research-led domain analysis for <journeys>").

### Step 1.7 — Summary

Also cover: entity, attribute, relationship, and constraint counts (Confirmed vs Proposed) and the number of assumptions; which sources carried the most weight; pending decisions and the highest-impact open questions.

## Step 2 — Update mode

### Step 2.1 — Read the existing file

Note its version, last Revision History row, and current Scope & Context and System Landscape.

### Step 2.2 — Understand what's driving the update

Ask what changed: new journeys or scope, new or changed systems or data flows, answers to pending decisions, assumptions, or open questions, new constraints, or a request to deepen research. Use the Step 1.2 questions only for what's new.

### Step 2.3 — Targeted research

Run Step 1.3 only for the new or changed scope. Reuse existing source IDs; append new ones.

### Step 2.4 — Confirmation gate (hard stop before drafting)

Present the delta brief per Step 1.4: scope change, primer additions, new or changed candidate entities, new decision points, and items moving to `Confirmed`. Flag possible duplicates against existing entities. Wait for confirmation.

### Step 2.5 — Reconcile and draft

Apply the Step 1.5 rules, and:
- **New entity:** add it to Entities Inventory, the diagram (keys), Attributes, and Relationships.
- **Existing entity:** extend its attributes and relationships; never duplicate it.
- **Similar-but-not-identical names:** add separately and flag under Open Questions unless the user confirmed the merge.
- **Validated items:** change Status to `Confirmed` and add `Stakeholder` to Source Type.
- **Decisions:** record each under *Decided* with its reason.
- **Assumptions confirmed:** remove the assumption, drop its †, and update the model; answered open questions are removed. Renumber per the IDs rule.
- **Extend** the Domain Primer and System Landscape to cover new content.

### Step 2.6 — Bump version and write back

Refinements and validations are minor; a structural change is major. Overwrite `outputs/<client>-domain-analysis.md`.
