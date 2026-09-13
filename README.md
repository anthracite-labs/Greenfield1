# Greenfield1 — App1

Greenfield1 is the repository for **App1**, instantiated from the reusable
**App-Factory** engineering foundation. The foundation supplies the engineering
protocol and lifecycle guards; App1 supplies the product work as it advances
through the repository-controlled lifecycle.

> **ECC is repository-owned, Arena-executed, ChatGPT-supervised.**

## Current project state

The authoritative lifecycle state is [`config/project.env`](config/project.env).
At present this repository is in **discovery**:

- `PROJECT_NAME=App1`
- `PROJECT_SLUG=app1`
- `PROJECT_PHASE=discovery`
- `ALLOW_APP_STACK=0`
- `STACK_DECISION_ADR=`

That means product discovery and foundation work are in scope, while application
frameworks, databases, auth schemes, hosting targets, UI stacks, and other
application-stack decisions remain gated until the reviewed lifecycle transition
and accepted stack ADR required by `config/project.env`.

The active product-discovery record is GitHub Issue #1. Repository documentation
must not silently substitute an implementation decision for that discovery work.

**Foundation version:** see [`FOUNDATION_VERSION`](FOUNDATION_VERSION) — `0.1.0`.

## What the foundation provides

| | |
| :-- | :-- |
| **ECC-on-Arena adapter** | Engineering rules, 10 on-demand workflows, 3 review personas, adapted from ECC v2.2.0 (MIT), fully attributed. Not native ECC. |
| **Deterministic gate** | `scripts/verify.sh` — 17 committed checks, non-zero on failure, re-run independently in CI. |
| **Negative tests** | `scripts/selftest.sh` — injects faults into a throwaway copy and asserts the gate rejects each one. A gate that only ever passes proves nothing. |
| **Lifecycle state** | `config/project.env` — factory → discovery → architecture → implementation, with a no-stack guard that stands down only via a reviewed, ADR-backed transition. |
| **Portable governance** | `config/main-ruleset.json` — a branch-protection payload with no instance ids, applicable to a repository by a human administrator. |
| **Documentation set** | Product, domain, roadmap, architecture, security, memory, and factory docs that are filled as the project lifecycle advances. |

## Operating model

```text
Human product owner
        ↓
ChatGPT — planning / architecture / independent PR review
        ↓
GitHub — durable source of truth
        ↓
Arena Agent Mode — developer / executor
        ↓
ECC-on-Arena repository adapter
        ↓
branch → tests → PR → CI → ChatGPT review → merge
```

## Starting a session

Arena auto-loads nothing. One short instruction is enough:

> Read `.ecc/BOOTSTRAP.md`, initialize the project engineering protocol,
> inspect project memory and the skill index, then work GitHub Issue #X. Load
> only skills relevant to that issue.

Or print the same briefing:

```bash
bash scripts/bootstrap.sh
```

Startup context is deliberately small: the bootstrap protocol, the standing
engineering rules, the skill index, project memory, and the lifecycle config.
Workflows are loaded one or two at a time, only when the task calls for them.

## Foundation provenance

This repository retains the App-Factory machinery and documentation needed to
operate the project safely. [`docs/FACTORY.md`](docs/FACTORY.md) documents the
source foundation and how new repositories are instantiated; it is provenance
and operational reference here, not evidence that Greenfield1 itself is the
reusable template source.

A template repository copies files, not GitHub configuration. Visibility,
branch rulesets, GitHub App installations, Actions permissions, secrets, and
required checks are administrative state and are not proven merely by committed
files.

## Repository map

```text
AGENTS.md                  engineering entry point for agents and humans
FOUNDATION_VERSION         App-Factory foundation version (0.1.0)
.ecc/                      the ECC-on-Arena adapter (rules, skills, roles, provenance)
config/project.env         authoritative lifecycle phase and application-stack guard
config/main-ruleset.json   portable branch-protection template
docs/                      product, domain, architecture, roadmap, security, memory, factory
docs/decisions/            architecture decision records
scripts/                   verify, selftest, bootstrap, init-project, sync-ecc
.github/workflows/verify.yml   independent CI execution of the same gate
```

## Quality gate

```bash
bash scripts/verify.sh     # authoritative — exits non-zero on failure
bash scripts/selftest.sh   # proves the gate still rejects faults
```

GitHub Actions runs both on every push and pull request, as the jobs
**`Foundation gate`** and **`Independent checks`**. Those exact names are the
required status contexts in `config/main-ruleset.json`, and the gate fails if
the workflow and the ruleset ever disagree.

## Provenance and licensing

- The `.ecc/` adapter is derived from
  [Everything Claude Code (ECC)](https://github.com/affaan-m/ECC) v2.2.0, MIT
  licensed. The full upstream notice is committed at
  [`.ecc/LICENSE-ECC`](.ecc/LICENSE-ECC) and verified by sha256; every adapted
  file carries an attribution header. Details:
  [`.ecc/UPSTREAM.md`](.ecc/UPSTREAM.md).
- This is an **adaptation, not native ECC**. Arena has no plugin runtime, no
  slash commands, no lifecycle hooks, and no subagents; no compatibility with
  the ECC runtime is claimed.
- **Factory provenance:** App-Factory v0.1.0 was derived from the reviewed
  source foundation
  `anthracite-labs/Ditto@5d9cc349d264f73e8da913da9d2cea664522237d`. Greenfield1
  identifies its inherited foundation through `FOUNDATION_VERSION`; the source
  project's product history is not part of this repository.
