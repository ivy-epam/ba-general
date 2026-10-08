---
name: generate-domain-model
description: Create or update a single, cumulative, product-wide domain model (ontology) capturing business entities, their attributes, relationships, hierarchy, and structural constraints. Folded in per-feature from PRD/Feature Analysis/Use Cases, never per-feature scoped. Use when the user asks to model the domain, identify entities/relationships, build an ontology, or create a data dictionary/entity-relationship model.
---

# Generate Domain Model (Ontology-Based)

Produces or updates **a single cumulative product-wide domain model** (`outputs/domain-model.md`) — an ontology of business entities, their data properties (attributes), object properties (relationships with verb phrases and cardinality), type hierarchy (subtypes/is-a), and structural constraints. This is the authoritative, evolving reference for business concepts; it is updated incrementally as each feature's PRD, Feature Analysis, and Use Cases are produced or analyzed.

**Ontology vocabulary used consistently across all runs:** 
- **Entities** (classes) = core business objects (Customer, Order, Invoice).
- **Attributes** (data properties) = typed fields on an entity (Order.orderDate).
- **Relationships** (object properties) = verb-phrase-labeled connections between two entities with cardinality (Customer *places* 1..* Order).
- **Taxonomy** (is-a hierarchy) = subtype relationships when source docs explicitly name them (CorporateCustomer is-a Customer).
- **Constraints** (axioms) = structural business rules governing entity existence/relationships (an Order must have ≥1 LineItem).
- **Individuals/instances:** explicitly out of scope (not useful at BA level).

**Sourcing discipline:** the PRD, Feature Analysis, and Use Cases documents are primary sources of truth for entity/attribute/relationship information. Stakeholder interview only fills what those documents do not establish — mainly tacit knowledge about entity states, undocumented relationships, or clarification of ambiguous flow wording. Every inventory row must cite its source (document section, Use Case ID, flow step, or "stated by [stakeholder] during interview"); nothing is inferred without sourcing. When multiple documents name similar-but-not-identical entities, they are never silently merged — they are listed separately and flagged under Open Questions as a possible duplicate for confirmation.

**Independence:** this skill maintains a purely *descriptive* domain model separate from `generate-rbac`. There is no enforced consistency between this model's entity names and `generate-rbac`'s Resource column — both are authoritative within their own scope. If, in the future, both are to be linked, that linkage is explicit and described as a separate decision.

The template lives at `templates/domain-model-template.md`. Always read that file first to get the current section structure — do not hardcode the structure from memory, in case the template has been edited.

**Output location:** each model is written to a fixed, non-parameterized path: `outputs/domain-model.md`. Never written anywhere else (not to user's home directory, Desktop, or another project).

## Step 0 — Determine mode: create or update

Check whether `outputs/domain-model.md` exists.
- **Doesn't exist** → **Create** (first run, seed the model from one or more features).
- **Exists** → **Update** (fold in new feature analysis, reconcile with existing entities/attributes/relationships, bump version).

## Step 1 — Create mode

### Step 1.1 — Gather scope

Ask which feature(s) and/or project code(s) should be incorporated into this initial domain model. Accept one or more; if unsure, ask to confirm.

### Step 1.2 — Locate and read source documents

For each feature, attempt to read:
- **PRD** (`outputs/<project-code>-PRD.md` or `outputs/feature-<feature>/<feature>-PRD.md`): harvest Key Features Overview section and any Glossary/Appendix terms already listed.
- **Feature Analysis** (`outputs/feature-<feature>/<feature>-feature-analysis.md`): harvest Stakeholders/Roles, As-Is/To-Be Business Rules tables, Systems Involved table.
- **Use Cases** (`outputs/feature-<feature>/<feature>-use-cases.md`): harvest Primary/Secondary Actors per use case and Basic/Alternate/Exception Flow prose (this is the richest source for entity/attribute/relationship candidates).

If a document doesn't exist for the selected feature(s), skip it — it's not a blocker. Rely more on interview to fill the gap.

### Step 1.3 — Build candidate entity inventory

Extract all business nouns/concepts literally named in the source documents — do NOT infer or generalize. List them exactly as named. If the same concept is named differently in different sections (e.g., "order" in one place, "purchase order" in another), list both as separate candidates and flag the ambiguity under Open Questions. Format as the 2. Entities Inventory table per the template.

### Step 1.4 — Propose attributes per entity

For each entity, scan the flow prose and business rules for evidence of data properties. Examples:
- "system records the order date" → `Order.orderDate`
- "customer's contact email" → `Customer.email`
- "invoice total must be calculated from line items" → `Invoice.total` (derived)

Tag each attribute with its source (e.g., "UC-03 Basic Flow step 2", "Feature Analysis: To-Be Business Rules row 5"). Cardinality/type of attributes can be inferred as text type, date, numeric, or enumerated — use common sense but mark ambiguous types with a note in Open Questions.

### Step 1.5 — Propose relationships and cardinality

From flow prose (actor-action/system-response pairs) and business rules, extract relationships:
- Verb phrases in system responses ("system creates order") suggest object properties (e.g., Customer → *places* → Order).
- Cardinality: extract from explicit wording ("each customer can place multiple orders" → 1..*, "an order belongs to exactly one customer" → ..1). Where cardinality is not explicit in source text, flag it with a "?" for confirmation rather than asserting it silently.

Format as the 5. Relationships table per template.

### Step 1.6 — Propose taxonomy (only if explicitly named in sources)

If and only if source documents explicitly mention subtypes (e.g., "there are two customer types: Individual and Corporate"), add those to a 3. Entity Taxonomy table. Never invent a hierarchy speculatively — if sources don't name subtypes, leave section 3 empty or remove it entirely.

### Step 1.7 — Propose structural constraints

From business rules and flow postconditions, extract constraints that govern entity structure/existence:
- "an order must have at least one line item" → cardinality constraint on the relationship Order→LineItem.
- "invoice status can be Draft, Submitted, or Paid; Paid invoices cannot be modified" → state constraint on Invoice.
- "a refund cannot be issued for a cancelled order" → mutual exclusivity constraint.

Explicitly exclude process-level rules (e.g., "the approval flow requires manager sign-off") — those belong in Feature Analysis's To-Be Business Rules section, not here. Format as 7. Business Rules / Constraints table.

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

### Step 2.2 — Gather scope

Ask which feature is driving this update (i.e., its PRD/Feature Analysis/Use Cases was just produced or significantly revised). Single feature only (don't fold in multiple features at once in Update mode).

### Step 2.3 — Locate and read that feature's source documents

Repeat Step 1.2 logic for the single triggering feature.

### Step 2.4 — Extract candidates from that feature

Repeat Steps 1.3–1.7 (entity/attribute/relationship/taxonomy/constraint extraction) scoped to the triggering feature's documents only.

### Step 2.5 — Reconcile with existing model

Apply the following reconciliation logic:
- **Brand-new entity** (not in existing Entities Inventory): add a new row to the Entities Inventory table. Add any of its attributes to the Attributes table. Add any of its relationships to the Relationships table.
- **Existing entity** (already in inventory): append *new* attributes/relationships discovered in this feature to their respective tables. Do NOT duplicate the entity's inventory row.
- **Similar-but-not-identical entity names across this feature and the existing model:** treat as possible duplicates — do NOT silently merge. Add as a new inventory row if it's not already there, and flag under Open Questions (e.g., "Feature XYZ mentions 'PurchaseOrder' but model has 'Order' — are these the same?").
- **New taxonomy entries:** if this feature's sources explicitly name subtypes of an entity already in the model, add rows to the Entity Taxonomy table.
- **New constraints:** add rows to the Business Rules / Constraints table.

### Step 2.6 — Update the Mermaid diagram

Revise the Domain Model Diagram (6. Domain Model Diagram) to include any newly added entities, relationships, and taxonomy entries. Existing entities/relationships do not change — the diagram grows to accommodate the new model content.

### Step 2.7 — Hard-stop confirmation gate (same as Create mode)

Present the delta (new entities, new attributes, new relationships, new constraints, any flagged duplicates) and wait for user confirmation before writing.

### Step 2.8 — Interview for gaps (if needed)

Same as Create mode Step 1.9.

### Step 2.9 — Bump version and update Revision History

Increment version (e.g., 1.0 → 1.1 for minor updates; 1.0 → 2.0 for major structural changes — use judgment). Add a new Revision History row: version, today's date, triggering feature/project code, and a plain-language description (e.g., "v1.2 — added Customer.loyaltyStatus and Refund entity, plus 0..1 Refund→Order relationship, from Refunds feature analysis").

### Step 2.10 — Write back to same path

Overwrite `outputs/domain-model.md` with the updated model, preserving all prior entries + new ones.

### Step 2.11 — Chat-only delta summary

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
