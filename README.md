# claude-ba-general

A set of Claude Code skills that generate and maintain a chain of business-analysis artifacts, from a Business Requirements Document (BRD) all the way through to a delivered feature's knowledge page. Each skill in the chain builds on the ones before it, cites where its content came from, and never invents facts — anything a skill can't establish from a source document or a direct answer from you gets logged as an **Open Question** instead of guessed at.

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

`generate-rbac` and `generate-smoke-test` run alongside the chain — cumulative, product-wide, updated as each feature is added or changes. `generate-domain-model` is project-scoped, created at project inception and refined as understanding deepens. `generate-case-study` is standalone and personal — it produces the contractor's own portfolio record for a project, stored outside `outputs/` entirely, and is typically run once when offboarding from that project.


## Directory structure

Example after running the chain on project `ABC`, feature `checkout` (use cases `place-order`, `apply-discount`):

```
outputs/
├── ABC-PRD.md
├── rbac.md
├── domain-model.md
├── smoke-tests.md
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
| Project | `outputs/<project-code>-PRD.md`, `outputs/domain-model.md` | `generate-prd`, `generate-domain-model` |
| Feature | `outputs/feature-<feature>/...` | `generate-feature-analysis`, `generate-use-cases`, `generate-knowledge-page` |
| Story | `outputs/<bucket>/US-<use-case>/...` | `generate-user-stories`, `verify-user-stories`, `generate-test-cases` |
| Product-wide | `outputs/rbac.md`, `outputs/smoke-tests.md` | `generate-rbac`, `generate-smoke-test` |
| Portfolio (personal, outside `outputs/`) | `case-study/<project-code>-case-study.md` | `generate-case-study` |

`case-study/` is a sibling of `outputs/` at the repo root, not nested inside it — it's the contractor's own portfolio record, not a project deliverable.

