# claude-ba-general

A set of Claude Code skills for business analysis. At its core is a chain of artifacts, from a Business Requirements Document (BRD) all the way through to a delivered feature's knowledge page. Each skill in the chain builds on the ones before it, cites where its content came from, and never invents facts — anything a skill can't establish from a source document or a direct answer from you gets logged as an **Open Question** instead of guessed at. Shared rules for all skills live in [CLAUDE.md](CLAUDE.md).

## Skills by group

Claude Code only discovers skills placed directly at `.claude/skills/<skill-name>/SKILL.md` — group folders aren't supported — so skills are grouped here rather than on disk.

### SDLC — artifact chain

Run in order, per feature (see the chain below).

| Skill | Produces |
|---|---|
| `generate-prd` | Product Requirements Document |
| `generate-feature-analysis` | As-is / to-be process, gap analysis, NFRs |
| `generate-use-cases` | Use case specifications |
| `generate-user-stories` | One story file per story, with Gherkin ACs |
| `verify-user-stories` | Independent QA review of a story |
| `generate-test-cases` | Functional test suite per story |
| `generate-knowledge-page` | Marks a story delivered; plain-language feature page |

### SDLC — product-wide

Cumulative documents that run alongside the chain and grow as the product evolves.

| Skill | Produces |
|---|---|
| `generate-domain-analysis` | Research-led domain model — created at project inception and refined as understanding deepens |
| `generate-rbac` | Role-based access control matrix — updated as each feature is added or changes |
| `generate-smoke-test` | Module-based smoke test scope analysis and suite — updated as each feature is added or changes |

### Career & talent

Personal or people-related work, not project deliverables.

| Skill | Produces |
|---|---|
| `generate-case-study` | The contractor's portfolio case study, stored outside `outputs/` — run once when offboarding |
| `assess-candidate` | Candidate assessment and interview questions — chat only, no file written |

## The artifact chain

```
BRD
 ▼
generate-prd
 ▼
generate-feature-analysis
 ▼
generate-use-cases
 ▼
generate-user-stories
 ▼
verify-user-stories
 ▼
generate-test-cases
 ▼
generate-knowledge-page
```

## Key concepts

```
Project
 └── Module        (technical)
      └── Feature  (business)
           └── Use case
                └── User story
```

- **Module** — a technical term: how the application is separated into parts (e.g. Homepage, Data Catalog).
- **Feature** — a business term: a capability the business asks for. Each feature sits within exactly one module; a module can contain multiple features.
- **Use case** — a distinct actor-goal interaction within a feature; a feature can have several.
- **User story** — an agile-ready slice of a use case; a use case can split into several.

Most of the chain works per feature. Modules matter where a product-wide view is needed — e.g. `generate-smoke-test` organises its scope analysis and smoke suite by module and rolls each new or changed feature up to its module.

## Directory structure

Example after running the chain on project `ABC`, feature `checkout` (use cases `place-order`, `apply-discount`):

```
outputs/
├── ABC-PRD.md
├── rbac.md
├── <client>-domain-analysis.md
├── smoke-tests/
│   ├── scope-analysis.md
│   └── smoke-tests.md
├── feature-checkout/
│   ├── checkout-feature-analysis.md
│   ├── checkout-use-cases.md
│   └── checkout-knowledge.md
├── future-sprint/
│   └── US-place-order/
│       └── place-order-US-02.md
├── current-sprint/
│   └── US-place-order/
│       ├── place-order-US-01.md
│       └── place-order-func-test-01.md
└── delivered/
    └── US-apply-discount/
        ├── apply-discount-US-01.md
        └── apply-discount-func-test-01.md

case-study/
└── ABC-case-study.md
```

## Sprint buckets

Stories (and their func-test files) live under `future-sprint/`, `current-sprint/`, or `delivered/` so the team can see what's active at a glance. Status is tracked per story, not per use case, so a use case's stories can be split across buckets.

- New stories start in `future-sprint/`.
- Moving to `current-sprint/` is a manual team action.
- `generate-knowledge-page` is the only skill that moves files — into `delivered/` — when marking a story shipped.
- Skills that need to find a story glob across all three buckets rather than assuming a fixed location.

## Naming conventions

| Scope | Path | Used by |
|---|---|---|
| Project | `outputs/<project-code>-PRD.md`, `outputs/<client>-domain-analysis.md` | `generate-prd`, `generate-domain-analysis` |
| Feature | `outputs/feature-<feature>/...` | `generate-feature-analysis`, `generate-use-cases`, `generate-knowledge-page` |
| Story | `outputs/<bucket>/US-<use-case>/...` | `generate-user-stories`, `verify-user-stories`, `generate-test-cases` |
| Product-wide | `outputs/rbac.md`, `outputs/smoke-tests/...` | `generate-rbac`, `generate-smoke-test` |
| Portfolio (personal, outside `outputs/`) | `case-study/<project-code>-case-study.md` | `generate-case-study` |

`case-study/` is a sibling of `outputs/` at the repo root, not nested inside it — it's the contractor's own portfolio record, not a project deliverable.

