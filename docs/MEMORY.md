# Project Memory

Append-only ledger. Newest entry at the bottom. The sandbox is destroyed
between sessions, so memory that is not committed does not exist.

Procedure: [`../.ecc/skills/project-memory.md`](../.ecc/skills/project-memory.md).

## How to use this file

- Append one entry per working session. Never rewrite or delete an old entry;
  correct it with a new one that says what changed and why.
- Record what was **verified**, with the command and its actual result — not
  what was intended.
- Record surprises and dead ends. A failed approach that is not written down
  gets retried by the next session.
- Durable product-discovery decisions belong in reviewed canonical product/domain
  docs and their approved issue provenance. Durable technical/architecture
  trade-offs go in [decisions/](decisions/README.md) as ADRs; this file points
  at the authoritative artifact rather than duplicating it.

Entry template:

```text
## YYYY-MM-DD — <short title>

**Context:** <issue / branch>
**Did:** <what changed>
**Verified:** <command> → <actual result>
**Learned:** <surprises, dead ends, constraints discovered>
**Next:** <what the following session should know or do>
```

---

## Template provenance (carried by App-Factory, not project history)

This repository's engineering foundation is App-Factory (see
[`../FOUNDATION_VERSION`](../FOUNDATION_VERSION)). App-Factory v0.1.0 was
derived from the reviewed Ditto Foundation source commit
`anthracite-labs/Ditto@5d9cc349d264f73e8da913da9d2cea664522237d`. That is
factory provenance only: none of the source project's product history,
debugging chronology, issue numbers, or branch names is carried here, and none
of it applies to this repository.

## Operating conventions inherited from the foundation

These are the conventions every session is expected to follow. They are
recorded here because they are the durable context a new session needs before
it has read anything else.

| Convention | Where it is enforced |
| :-- | :-- |
| Read `.ecc/BOOTSTRAP.md` first; load 1–2 skills on demand. | `bootstrap`, `skill_index` checks |
| `scripts/verify.sh` is the only accepted evidence of quality. | CI job `Foundation gate` |
| The gate is proven by negative tests, not by passing. | `scripts/selftest.sh` |
| Product discovery belongs in canonical product/domain docs; implementation-stack choices require an approved architecture issue, accepted ADR, and lifecycle transition. | `.ecc/BOOTSTRAP.md`, `no_app_stack`, `lifecycle` checks |
| Lifecycle changes are config diffs, never edits to the gate. | `config/project.env` + `lifecycle` check |
| Never commit credentials; findings are reported redacted. | `secrets`, `env_files` checks |
| Work on the session branch; never push to `main`; never self-merge. | `.ecc/rules/git.md`, branch ruleset |
| ECC is adapted, not vendored, and never silently upgraded. | `provenance`, `attribution` checks |

---

## Session entries

<!-- Append below this line. Do not edit entries above it. -->

## 2026-09-06 — App-Factory v0.1.0 foundation created

**Context:** Issue #1, branch `arena/01a076c9-app-factory`
**Did:** Created the generic reusable foundation from the reviewed Ditto
source commit: genericized `.ecc/` adapter, added `FOUNDATION_VERSION`,
`config/project.env` lifecycle state, portable `config/main-ruleset.json`,
`scripts/init-project.sh`, lifecycle-aware no-stack guard, clean
product/domain/roadmap/memory docs, and `docs/FACTORY.md`.
**Verified:** `bash scripts/verify.sh` and `bash scripts/selftest.sh` — see the
PR body for the recorded output of both runs.
**Learned:** The source foundation's permanent `ALLOW_APP_STACK=0` constant
inside `verify.sh` could not survive in a reusable template: a generated
repository must be able to graduate to an application stack without editing the
gate. Moving the state into `config/project.env` and adding a `lifecycle` check
that requires phase + ADR consistency keeps the transition explicit and
reviewable. ECC stays pinned at v2.2.0; upgrading it is a separate version bump.
**Next:** This template is `PROJECT_PHASE=factory`. A generated repository
should run `scripts/init-project.sh` first, then complete the GitHub-admin
checklist in [FACTORY.md](FACTORY.md), which the template cannot do for it.

## 2026-09-10 — Greenfield preflight documentation audit

**Context:** Issue #3, branch `chore/greenfield-preflight-cleanup`.
**Did:** Aligned the README lifecycle summary with the committed lifecycle by
including the `factory` phase, and clarified that GitHub's **Template repository**
setting is administrative state rather than something committed repository files
can prove or enable.
**Verified:** Read-only GitHub repository metadata reported `is_template=false`;
the repository rulesets endpoint returned no live rulesets at the time of this
audit. The repository content itself still carries `config/main-ruleset.json`
as the portable policy definition. No GitHub administrative setting was changed
by this documentation task. CI on the exact PR head is the acceptance evidence
for the repository edits.
**Learned:** Calling App-Factory a template source and GitHub marking it as a
template repository are separate states. The greenfield workflow must verify
both repository contents and live GitHub configuration instead of inferring one
from the other.
**Next:** A maintainer should enable GitHub's **Template repository** setting
before relying on **Use this template**, and separately decide whether to apply
the portable Main ruleset to App-Factory itself. Generated repositories must
still receive their own live governance because GitHub administrative settings
are not inherited.

## 2026-09-13 — App1 discovery state aligned

**Context:** Issue #4, branch `docs/issue-4-repository-state-alignment`.
**Did:** Corrected the root README so Greenfield1 is described as the App1
project repository instantiated from App-Factory rather than as the reusable
factory source. Recorded the current lifecycle and added this durable pointer to
GitHub Issue #1, which remains the active product-discovery record. Issue #1
contains the current founder-approved discovery direction, including the
Universal Core and Community / Personal Workspace contracts; later approved
entries supersede conflicting earlier discovery assumptions.
**Verified:** GitHub file reads in this session showed
`config/project.env` with `PROJECT_NAME=App1`, `PROJECT_PHASE=discovery`,
`ALLOW_APP_STACK=0`, and an empty `STACK_DECISION_ADR`; GitHub Issue #1 remained
open as `Product discovery: define App1`; the branch reads of `README.md` and
`docs/MEMORY.md` were used as the source for this documentation-only update.
No shell verification is claimed here; PR CI is the acceptance evidence for
these repository edits.
**Learned:** Repository instantiation and later lifecycle transitions can leave
human-facing factory wording stale even when `config/project.env` is correct.
Future sessions should treat `config/project.env` as authoritative for lifecycle
state and Issue #1 as the current discovery source until discovery is formally
closed or superseded.
**Next:** After this documentation alignment is reviewed and merged, continue
App1 discovery from the next unresolved product layer; do not select an
application stack while `ALLOW_APP_STACK=0`.

## 2026-09-13 — Discovery register normalized into canonical docs

**Context:** Issue #6, branch `docs/issue-6-normalize-discovery-docs`.
**Did:** Moved the founder-approved working discovery state out of the temporary
root discovery register and into the canonical repository surfaces:
`docs/PRODUCT.md`, `docs/DOMAIN.md`, `docs/ROADMAP.md`, and `docs/SECURITY.md`.
Updated the repository/bootstrap guidance so `discovery` means product definition
is in progress and founder-approved working requirements may exist, while
application architecture/stack remains prohibited. The temporary root discovery
register is retired after content/reference review confirms its accepted
discovery material is preserved.
**Verified:** In this connector session, the source discovery register was read
in full in line-range chunks; branch writes were made only on the Issue #6
branch; the canonical documents were re-read during review; `config/project.env`
was not edited and remains `PROJECT_PHASE=discovery`, `ALLOW_APP_STACK=0`, with
an empty `STACK_DECISION_ADR`. Local shell verification is not claimed here; the
exact PR head and GitHub Actions are the independent acceptance evidence.
**Learned:** The foundation's original shorthand "discovery = no product
definition" was too absolute once founder-approved discovery existed. The
correct distinction is: discovery may contain an approved **working** product
definition, but architecture begins only when that definition is accepted enough
to choose implementation approaches. Also, the older operating-conventions row
above that groups "stack/product choice" under ADRs is historical foundation
wording; this entry supersedes that interpretation for Greenfield1 product
discovery. Product decisions belong in reviewed canonical product docs;
application-stack decisions belong in ADRs during the later lifecycle.
**Next:** Continue product discovery from Hybrid / Professional Workspace using
`docs/PRODUCT.md` as the canonical discovery source, Issue #1 as provenance, and
the Research → Planning workflow. Do not advance to architecture until the
remaining discovery and validation exit conditions are explicitly satisfied.

## 2026-09-13 — Live ruleset and stale-data audit

**Context:** Issue #8, branch `docs/issue-8-ruleset-stale-audit`.
**Did:** Verified the active `main-protection` repository ruleset, synchronized
`config/main-ruleset.json` with its reusable pull-request fields, and corrected
current-state wording that still treated discovery as product-undefined or
routed product decisions into ADRs. Added a canonical-source note to Issue #1
without rewriting its historical discovery content.
**Verified:** GitHub reported `main` as the default branch and an active
repository ruleset targeting `~DEFAULT_BRANCH` with deletion and non-fast-forward
protection, pull-request enforcement, review-thread resolution, and strict
required status checks `Foundation gate` and `Independent checks`. The live
ruleset also reports `required_reviewers=[]` and
`require_extra_approval_for_unattributed_changes=true`; those fields are now
explicit in the portable JSON. Lifecycle values remain
`PROJECT_PHASE=discovery`, `ALLOW_APP_STACK=0`, `STACK_DECISION_ADR=`.
**Learned:** Stale data was concentrated at boundaries between inherited factory
guidance and the now-populated discovery docs: `config/project.env` comments,
architecture/security identity text, ADR/memory/research routing, the PR
checklist, and factory ruleset documentation. Historical memory and superseded
Issue #1 discussion should remain preserved but clearly non-canonical. Upstream
ECC v2.2.1 and AgentShield v1.6.0 are now newer than the intentionally pinned
v2.2.0 / v1.4.0; upgrading either remains separate reviewed work.
**Next:** Verify the Issue #8 branch with the repository gate and exact-head CI,
then merge the cleanup before resuming Hybrid / Professional Workspace research.
