# Architecture Decision Records

Durable technical and architectural trade-offs, recorded so future sessions can
reconstruct *why* instead of re-litigating them. Procedure:
[`.ecc/skills/decisions.md`](../../.ecc/skills/decisions.md).

Founder-approved product-discovery decisions do **not** belong here. During
`PROJECT_PHASE=discovery`, current product requirements live in
[`../PRODUCT.md`](../PRODUCT.md), domain rules in [`../DOMAIN.md`](../DOMAIN.md),
and discovery discussion/provenance in the approved product-discovery issue.
ADRs are reserved for foundation, architecture, implementation, security,
testing, process, and other durable technical trade-offs when the relevant
lifecycle stage permits them.

## Rules

- One decision per file: `NNNN-<kebab-title>.md`, numbered sequentially.
- Accepted ADRs are never edited to change the decision — supersede them with a
  new ADR and mark the old one `superseded by ADR-NNNN`.
- Alternatives must be real, and the "why not" must be specific.
- Consequences must include the costs.

## Index

The records below are the **foundation** decisions, inherited from App-Factory.
They explain how this repository is engineered, not what App1 is. This
instantiated repository appends later technical/architecture decisions after
them; product-discovery requirements remain in the canonical product docs.

| ADR | Title | Status | Date |
| :-- | :-- | :-- | :-- |
| [0001](0001-ecc-on-arena-adapter.md) | Adopt an ECC-on-Arena adapter instead of native ECC | accepted | 2026-09-06 |
| [0002](0002-verification-gate.md) | `scripts/verify.sh` + GitHub Actions as the sole quality gate | accepted | 2026-09-06 |
| [0003](0003-flat-skill-files.md) | Flat per-task workflow files instead of upstream `SKILL.md` directories | accepted | 2026-09-06 |
| [0004](0004-lifecycle-config-stack-guard.md) | Project lifecycle config replaces the hard-coded no-app-stack guard | accepted | 2026-09-06 |

The ADR that records a project's **implementation stack** is referenced by
`STACK_DECISION_ADR` in [`../../config/project.env`](../../config/project.env),
and `scripts/verify.sh` fails if that reference does not resolve.

## Template

Copy [`0000-template.md`](0000-template.md) to start a new record.
