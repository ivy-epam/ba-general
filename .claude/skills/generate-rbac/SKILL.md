---
name: generate-rbac
description: Create or update the product's cumulative Role-Based Access Control (RBAC) matrix — a single, growing document (not per-feature) tracking which roles can Create/Read/Update/Delete which features/resources. Driven primarily by the PRD, Feature Analysis, and Use Cases documents for a feature, supplemented by stakeholder interview only where those docs don't establish access detail. Use when the user asks to create/update the RBAC matrix, access control document, roles and permissions, or who-can-do-what for the product.
---

# Generate RBAC

Produces or updates `outputs/rbac.md` — a **single cumulative, product-wide** access control matrix, not a per-feature artifact. Every time a feature's PRD, Feature Analysis, or Use Cases document is produced or updated, this skill folds that feature's roles, resources, and access grants into the existing matrix rather than creating a new file.

**Sourcing discipline:** the PRD, Feature Analysis, and Use Cases documents for the feature in question are the primary sources. Every row added to the matrix must cite where it came from (a specific document section, a Use Case ID, or "stated by [stakeholder] during interview").

The template lives at `templates/rbac-template.md` in this project.

The output is always `outputs/rbac.md` — never parameterized by project code or feature name.

## Step 0 — Determine mode: first run or update

Check whether `outputs/rbac.md` already exists in this project.
- **Doesn't exist** → this is the **first run** (effectively Create).
- **Exists** → this is an **Update** — fold in the new feature's content rather than overwriting.

## First run (file doesn't exist yet)

1. **Ask which feature(s)/project code(s) to incorporate.** Can be more than one if catching up on several features at once.

2. **Read the available source documents for each**, where they exist:
   - `outputs/<project-code>-PRD.md` — Target Users/Personas (candidate roles), Key Features/Capabilities Overview (candidate features/resources).
   - `outputs/feature-<feature>/<feature>-feature-analysis.md` — Stakeholders/Roles Involved (candidate roles), Systems Involved (candidate resources), To-Be: Business Rules (possible access-relevant rules — flag hints of approval, role hierarchy, or segregation of duties as Open Questions rather than modeling them).
   - `outputs/feature-<feature>/<feature>-use-cases.md` — Primary/Secondary Actors per use case (roles tied to specific actions), Basic Flow steps (source for inferring CRUD-level grants).

3. **Build the Roles Inventory and Features/Resources Inventory** directly from what's literally named in these sources. Do NOT merge roles that appear under different names or descriptions across documents, even if they look like the same role — list each as its own row and flag the suspected duplication under Open Questions instead.

4. **Propose CRUD grants inferred from Use Case Basic Flow wording.** For each actor-action → system-response step, infer the likely CRUD operation (e.g., "system creates a record" → Create, "user views X" → Read), tag it with the source Use Case ID, and present the full proposed list to the user in one pass for confirmation or correction.

5. **Interview for gaps** — e.g., a role clearly involved per Feature Analysis but with no corresponding Use Case to infer CRUD detail from. Ask directly what that role can do on which resource.

6. **Draft the document** following `templates/rbac-template.md` exactly. In the matrix, leave a CRUD column blank when a grant isn't evidenced or doesn't apply — never mark "N" speculatively.

7. **Write the output** to `outputs/rbac.md`; the first Revision History row notes which feature(s)/project code(s) seeded it.

8. **Summarize for the user**, also covering roles/resources found per source, which grants were inferred (and confirmed), and any suspected duplicate roles across documents.

## Update (file already exists)

1. **Read the existing `outputs/rbac.md`** in full, noting its current version.

2. **Ask which feature/project code is driving this update**, and read its PRD/Feature Analysis/Use Cases the same way as the first-run flow (steps 2–5 above), including proposing inferred CRUD grants for confirmation and interviewing only for gaps.

3. **Reconcile against what's already in the matrix:**
   - New roles/resources → add new inventory rows.
   - A role/resource that already exists → add new RBAC Matrix grant rows for it; do not duplicate its inventory entry.
   - A role name from the new feature that might match an existing role but isn't an exact match → do NOT merge; add it as its own row and flag the possible duplication as a new Open Question.

4. **Bump the version** (the Revision History row records which feature/project code drove the update) **and write back** to `outputs/rbac.md`.

5. **Summarize the delta for the user:** what changed, what stayed the same, and any new Open Questions.