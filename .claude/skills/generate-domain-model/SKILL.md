---
name: generate-domain-model
description: Create or update a project-scoped domain model (ontology) capturing business entities, their attributes, relationships, hierarchy, and structural constraints. Folded in per-feature from that project's PRD/Feature Analysis/Use Cases. Use when the user asks to model the domain, identify entities/relationships, build an ontology, or create a data dictionary/entity-relationship model for a specific project.
---

# Generate Domain Model (Ontology-Based)

Produces or updates **the project's domain model** (`outputs/domain-model.md`) — an ontology of business entities, their data properties (attributes), object properties (relationships with verb phrases and cardinality), type hierarchy (subtypes/is-a), and structural constraints. This is the authoritative, evolving reference for the project's business concepts and vocabulary; it is scoped to the project's stated business objectives and updated as understanding deepens.

**Ontology vocabulary used consistently across all runs:** 
- **Entities** (classes) = core business objects (Customer, Order, Invoice).
- **Attributes** (data properties) = typed fields on an entity (Order.orderDate).
- **Relationships** (object properties) = verb-phrase-labeled connections between two entities with cardinality (Customer *places* 1..* Order).
- **Taxonomy** (is-a hierarchy) = subtype relationships when source docs explicitly name them (CorporateCustomer is-a Customer).
- **Constraints** (axioms) = structural business rules governing entity existence/relationships (an Order must have ≥1 LineItem).
- **Individuals/instances:** explicitly out of scope (not useful at BA level).

**Sourcing discipline:** the primary source of truth for the domain ontology is **stakeholder interview** informed by business context, market research, and domain expertise — not just feature-driven documents (which may not exist yet). Every entity, attribute, relationship, taxonomy entry, and constraint must be sourced to an interview statement or documented research (market positioning, competitive analysis, known industry standards); nothing is inferred or fabricated. When discovery encounters similar-but-not-identical entity names (e.g., from different stakeholders or interviews), they are never silently merged — they are listed separately and flagged under Open Questions as a possible duplicate for confirmation.

**Independence:** this skill maintains a purely *descriptive* domain model separate from `generate-rbac`. There is no enforced consistency between this model's entity names and `generate-rbac`'s Resource column — both are authoritative within their own scope. If, in the future, both are to be linked, that linkage is explicit and described as a separate decision.

The template lives at `templates/domain-model-template.md`. Always read that file first to get the current section structure — do not hardcode the structure from memory, in case the template has been edited.

**Output location:** the project's domain model is written to a fixed path: `outputs/domain-model.md`. Never written anywhere else (not to user's home directory, Desktop, or another project).

## Step 0 — Determine mode: create or update

Check whether `outputs/domain-model.md` exists.
- **Doesn't exist** → **Create** (first run, establish the project's domain ontology).
- **Exists** → **Update** (deepen understanding, add/refine entities/attributes/relationships, bump version).

## Step 1 — Create mode

### Step 1.1 — Understand broader business context

Before diving into the project, interview the user about the business context:
- **Domain / Industry:** which industry or business domain does this project sit within (e.g., e-commerce, banking, healthcare, logistics, manufacturing)?
- **End Users:** who are the primary end users or stakeholders (customers, partners, internal teams, regulators)?
- **Business Process:** what business process, value chain, or workflow is this project part of?

This context frames the vocabulary and entity landscape that the project's domain ontology will reflect.

### Step 1.2 — Understand project scope within that context

Now ask about the specific project:
- What is the project trying to accomplish (create new product, introduce new process, enhance existing process, expand to new market)?
- What is in scope vs. out of scope for this project?

This narrows the domain ontology to focus on entities and relationships relevant to what the project is actually building.

### Step 1.3 — Build candidate entity inventory from interview

Based on the business context and project scope, interview the user to identify core business entities central to this project:
- What are the key "things" or concepts in this business that the project deals with (e.g., for order-management: Customer, Order, Product, Inventory; for compliance: Regulation, Audit, Review, Finding)?
- Extract these literally as named by the user — do NOT infer or generalize. If the user mentions the same concept under different names (e.g., "order" and "purchase order"), list both as candidates and flag the ambiguity under Open Questions.

Format as the 2. Entities Inventory table per the template.

### Step 1.4 — Propose attributes per entity

For each entity, interview the user to identify its key data properties. Examples:
- "What information do you store about each Customer?" → `Customer.name`, `Customer.email`, `Customer.accountBalance`
- "What defines an Order?" → `Order.orderDate`, `Order.totalAmount`, `Order.status`

Infer data types from context (text, date, numeric, enumerated) — use common sense. If a type is ambiguous or the user hasn't specified it, mark it with a note in Open Questions. Tag each attribute with its source (e.g., "user interview" or "stated by user").

### Step 1.5 — Propose relationships and cardinality

Interview the user to identify how entities relate to each other:
- "How do Customer and Order relate?" → Customer *places* Order.
- "Can a customer have multiple orders?" → Yes, 1..* cardinality.
- "Does an order belong to exactly one customer?" → Yes, ..1 cardinality.

Extract the relationship as a verb phrase and the cardinality. Where cardinality is ambiguous, flag it with a "?" for confirmation rather than asserting it silently. Format as the 5. Relationships table per template, with source marked as "user interview."

### Step 1.6 — Propose taxonomy (only if user identifies subtypes)

If and only if the user explicitly names subtypes of an entity (e.g., "there are two customer types: Individual and Corporate"), add those to a 3. Entity Taxonomy table. Include the distinguishing rule that separates them. Never invent a hierarchy speculatively — if the user doesn't mention subtypes, leave section 3 empty or remove it entirely.

### Step 1.7 — Propose structural constraints

Interview the user to identify constraints that govern entity structure and existence (distinct from process/workflow rules):
- "Does an order always have at least one line item?" → cardinality constraint on Order→LineItem.
- "What statuses can an invoice have, and what transitions are allowed?" → state constraint on Invoice.
- "Can a refund be issued for a cancelled order?" → mutual exclusivity constraint.

Explicitly exclude process-level rules (e.g., "the approval workflow requires manager sign-off") — those belong in Feature Analysis's To-Be Business Rules, not here. Format as 7. Business Rules / Constraints table.

### Step 1.8 — Present complete proposal for confirmation

**Hard-stop confirmation gate.** Compile the full candidate entity/attribute/relationship/taxonomy/constraint set and present it in chat, grouped clearly (Entities, Attributes per entity, Relationships, Taxonomy if any, Constraints if any). Explain the sources for each grouping (e.g., "Entities extracted from UC-03 Basic Flow and Feature Analysis Stakeholders"). Ask the user to review and confirm before proceeding. Invite them to:
- Remove spurious candidates (false positives from prose misreading).
- Merge explicitly-similar names if they are indeed the same concept (opposite of our earlier "no silent merge" rule — this is the user's explicit moment to confirm merges).
- Add missing entities/attributes/relationships if the sources didn't capture something the user knows.
- Clarify ambiguous cardinalities (replace "?" with confirmed cardinality).

**Wait for confirmation before writing anything.**

### Step 1.9 — Interview for gaps (if needed)

After confirmation, if any relationship cardinalities, attributes, or constraints remain marked as "?" or "unconfirmed," interview the user to resolve them. Anything still unresolved → Open Questions section (never fabricated).

### Step 1.10 — Draft the document

Using the confirmed entity/attribute/relationship/taxonomy/constraint list and per the current `templates/domain-model-template.md` structure, draft the output document. Include:
- Document Control table (Status: Draft) and Revision History (version 1.0, first row noting the seeding feature(s)).
- All eight sections (Entities Inventory, Entity Taxonomy if any, Attributes, Relationships, Domain Model Diagram in Mermaid classDiagram syntax, Business Rules / Constraints if any, Open Questions).
- A Mermaid `classDiagram` that accurately depicts:
  - Entities as classes with brief attribute lists (full descriptions are in the Attributes table, not cluttering the diagram).
  - Relationships drawn with verb-labeled, cardinality-labeled edges (e.g., `Customer "1..*" -- "1" Order : places`).
  - Subtype arrows (`<|--`) for any taxonomy entries.

### Step 1.11 — Write output

Write to `outputs/domain-model.md` (create the `outputs/` folder if needed). Version `1.0`. First Revision History row: version, today's date, feature(s) that seeded it, and a plain-language summary (e.g., "Initial domain model seeded from Checkout feature (UC-01, UC-02)").

### Step 1.12 — Chat-only summary

Summarize for the user in chat (not in the document):
- What came from where (which features, which sections of each source doc).
- How many entities/attributes/relationships were identified.
- What was explicitly confirmed vs. inferred vs. filled in by interview.
- Any Open Questions or flagged duplicates.

## Step 2 — Update mode

### Step 2.1 — Read existing file and version

Read the current `outputs/domain-model.md`, note its current version and last Revision History row.

### Step 2.2 — Understand what's driving the update

Ask the user why they're updating the domain model: is understanding of the business domain deepening, have new entities/relationships been discovered, has the project scope changed, etc.?

### Step 2.3 — Interview to identify new/refined entities and relationships

Based on the reason for update, interview the user to discover:
- New entities or entity types not yet in the model?
- Attributes to add to existing entities or clarify previously ambiguous ones?
- New or refined relationships between entities?
- New or refined taxonomy (subtypes)?
- New or refined constraints?

### Step 2.4 — Interview for gaps (if needed)

If anything remains unconfirmed or unclear after the interview, ask follow-up questions. Anything still unresolved → Open Questions (never fabricated).

### Step 2.5 — Reconcile with existing model

Apply the following reconciliation logic:
- **Brand-new entity** (not in existing Entities Inventory): add a new row to the Entities Inventory table. Add any of its attributes to the Attributes table. Add any of its relationships to the Relationships table.
- **Existing entity** (already in inventory): append *new* attributes/relationships discovered in this update to their respective tables. Do NOT duplicate the entity's inventory row.
- **Similar-but-not-identical entity names** (new discovery vs. existing model): treat as possible duplicates — do NOT silently merge. Add as a new inventory row if it's not already there, and flag under Open Questions (e.g., "New discovery mentions 'PurchaseOrder' but model has 'Order' — are these the same?").
- **New taxonomy entries:** if the user explicitly names subtypes of an existing entity, add rows to the Entity Taxonomy table.
- **New constraints:** add rows to the Business Rules / Constraints table.

### Step 2.6 — Update the Mermaid diagram

Revise the Domain Model Diagram (6. Domain Model Diagram) to include any newly added entities, relationships, and taxonomy entries. Existing entities/relationships do not change — the diagram grows to accommodate the new model content.

### Step 2.6 — Hard-stop confirmation gate

Present the delta (new entities, new attributes, new relationships, new constraints, any flagged duplicates) and wait for user confirmation before writing.

### Step 2.7 — Bump version and update Revision History

Increment version (e.g., 1.0 → 1.1 for minor refinements; 1.0 → 2.0 for major structural changes — use judgment). Add a new Revision History row: version, today's date, plain-language description of what changed and why (e.g., "v1.2 — added Refund entity and 0..1 Refund→Order relationship; clarified Customer.status enumeration values").

### Step 2.8 — Write back to same path

Overwrite `outputs/domain-model.md` with the updated model, preserving all prior entries + new ones.

### Step 2.9 — Chat-only delta summary

Summarize for the user:
- What new entities/attributes/relationships/constraints were added.
- What came from the triggering feature's sources.
- Any Open Questions or flagged duplicates introduced by this update.
- Version bump explanation.

---

## Shared discipline across all updates

- **No fabrication:** every entity, attribute, relationship, taxonomy entry, and constraint must be sourced to a document section or interview; anything without source evidence → Open Questions.
- **No silent merging:** entities with similar names are never merged automatically; flag and confirm.
- **Exact naming from sources:** preserve the exact terminology used in source documents, even if redundant across features.
- **Cardinality: explicit or flagged:** never assert cardinality without explicit source or user confirmation; use "?" to mark uncertain cardinalities.
- **Structural constraints only:** business rules that constrain entity/relationship structure go here; operational/workflow rules belong in Feature Analysis's To-Be Business Rules.
