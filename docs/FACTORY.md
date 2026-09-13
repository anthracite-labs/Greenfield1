# Factory — instantiating a new application repository

App-Factory is a reusable engineering foundation, not an application. This page
is how you turn it into a new project, and — more importantly — what it
**cannot** do for you.

## The one thing to understand first

> **A template repository copies files. It does not copy GitHub configuration.**

Repository visibility, branch protection and rulesets, GitHub App
installations, Actions permissions, environments, secrets, variables, and
required-check settings are **not inherited**. A generated repository looks
fully governed on disk while being completely unprotected on the platform.

Nothing in `scripts/` changes GitHub administrative settings. Those steps are
human actions, listed below, and they are the ones that actually protect
`main`.

## Instantiation checklist

Work top to bottom. Do not skip step 6.

### 1. Create the repository from the template

Use GitHub's "Use this template" (if App-Factory is marked a template
repository) or copy the foundation files into a fresh repository. Do not fork
if you want a clean, independent history.

### 2. Set repository visibility intentionally

Decide private or public **before** the first push. Making a repository private
later does not un-publish what was already public.

### 3. Authorize the Arena GitHub App for the new repository

An App installed on one repository is not installed on another. Without this,
Arena cannot clone, push, or open pull requests.

### 4. Ensure Workflows read/write permission where required

If Arena must create or edit files under `.github/workflows/`, the GitHub App
installation needs Workflows write permission. Otherwise pushes touching
workflow files are rejected — with an error that looks like an auth failure.
Grant it deliberately, or edit workflows by hand.

### 5. Apply the branch ruleset

Apply [`../config/main-ruleset.json`](../config/main-ruleset.json) to the
default branch.

The file is the portable request body for GitHub's repository-ruleset API. It
contains no server-assigned ids, timestamps, source metadata, or explanatory
keys. The committed payload should be kept in sync with the active repository
policy, while the live GitHub ruleset remains the authoritative evidence that
protection is actually applied. `scripts/verify.sh` (check `ruleset`) parses the
portable file and validates its structure, rejecting unknown top-level keys as
well as missing policy.

Either configure it through the GitHub UI to match, or have an **explicitly
authorized** maintainer apply it with admin credentials, for example:

```bash
# Run by a human maintainer with admin rights on the new repository.
# No script in this repository does this for you.
gh api --method POST repos/<owner>/<repo>/rulesets \
  --input config/main-ruleset.json
```

Validate the file's shape first — this is read-only and safe:

```bash
bash scripts/verify.sh --only=ruleset
```

The current portable policy encodes:

- pull requests required for the default branch;
- baseline `required_approving_review_count=0` for the solo-owner workflow;
- stale approvals dismissed on new reviewable pushes;
- no required code-owner review;
- no general last-push approval requirement;
- no required-reviewer teams (`required_reviewers=[]`);
- all review threads resolved before merge;
- GitHub's `require_extra_approval_for_unattributed_changes` flag explicitly
  enabled so the portable payload matches the active ruleset;
- merge, squash, and rebase allowed;
- strict/up-to-date required status checks `Foundation gate` and
  `Independent checks`;
- required checks enforced on branch creation as well as later updates;
- no force pushes, no branch deletion, and no bypass actors.

GitHub currently documents the unattributed-change approval setting as a
public-preview Copilot rule and states that it has no effect when the baseline
required approval count is zero. It is nevertheless recorded explicitly here
because silent platform defaults are poor portable policy: a future baseline
approval change should not accidentally change the meaning of an omitted field.

> The required contexts must match the job names in
> `.github/workflows/verify.yml` exactly. If you rename a CI job, the ruleset
> silently stops requiring it. `scripts/verify.sh` (check `ci_wiring`) fails if
> the two ever disagree.

### 6. Verify that `main` reports protected

Do not trust step 5 — confirm it:

```bash
gh api repos/<owner>/<repo> --jq '.default_branch'
gh api repos/<owner>/<repo>/rules/branches/main --jq '[.[].type]'
```

The second command must list `pull_request`, `required_status_checks`,
`deletion`, and `non_fast_forward`. An empty list means `main` is unprotected
and the PR-only workflow is enforced by nothing but convention.

For a complete ruleset comparison, also inspect the active repository ruleset
and compare its reusable fields with `config/main-ruleset.json`; do not copy
server-assigned ids, timestamps, links, source metadata, or bypass-evaluation
state back into the portable payload.

### 7. Run `scripts/init-project.sh`

```bash
bash scripts/init-project.sh --name "<Project Name>"
```

Sets `PROJECT_NAME`, `PROJECT_SLUG`, and moves `PROJECT_PHASE` from `factory`
to `discovery` in `config/project.env`. It is non-destructive, refuses to
overwrite an already-initialized project unless `--force` is given, never
touches ECC provenance or licence files, and never commits, pushes, or changes
GitHub settings. Review the diff and commit it yourself. Use `--dry-run` first
if you want to see the change without writing it.

### 8. Run the gate and the negative tests

```bash
bash scripts/verify.sh
bash scripts/selftest.sh
```

Both must exit 0 before any product work starts. If they do not, fix that
first — a broken gate means every later claim is unverified.

### 9. Begin product discovery via a GitHub issue

In a newly generated repository, open a product-discovery issue and use that
project's `docs/PRODUCT.md` as the canonical reviewed product document. Do not
let a product definition arrive as a side effect of code.

### 10. Keep independent review before merge

The foundation uses a baseline of 0 mandatory GitHub approvals so a solo owner
is not structurally blocked from merging after the deterministic gates pass.
That does **not** make review optional: ChatGPT still reviews the real diff
independently before merge, and review findings must be addressed or recorded.
The GitHub ruleset and the ChatGPT review process are complementary controls;
neither should be described as proof that the other happened.

## Recording the application-stack decision

When a project reaches the `architecture` stage and selects its stack, the ADR
that records it must be machine-identifiable, because `scripts/verify.sh` will
not permit `ALLOW_APP_STACK=1` without it. Copy
[`decisions/0000-template.md`](decisions/0000-template.md), then ensure the
finished ADR carries **both** of these as standalone metadata lines, alongside
`**Date:**` and `**Deciders:**`:

```text
**Status:** accepted
**Decision Type:** application-stack
```

Then point `STACK_DECISION_ADR` in
[`../config/project.env`](../config/project.env) at that file.

Two rules are enforced deliberately:

- **Comments and code fences do not count.** The validator strips HTML comment
  regions and fenced blocks before matching, so instructional text, examples,
  or a quoted marker cannot satisfy the requirement. This page's fenced example
  above is itself inert for exactly that reason.
- **The match is a whole line, not a substring.** Prose that merely mentions
  the marker is not a decision.

Together these stop the most likely accident: copying the template to a new
filename, leaving its instructions in place, and inheriting a stack marker the
author never intended to assert.

## What the template does carry

| Carried | Not carried |
| :-- | :-- |
| `.ecc/` adapter: rules, skills, roles, provenance, licence | Repository visibility |
| `config/project.env`, `config/main-ruleset.json` | Applied rulesets / branch protection |
| `docs/` skeletons and ADR structure | GitHub App installations |
| `scripts/` gate, negative tests, bootstrap, init, sync | Actions permissions and secrets |
| `.github/workflows/verify.yml` and the PR template | Required status-check configuration |
| `FOUNDATION_VERSION` | Issues, projects, labels, environments |

## Versions — keep them distinct

| Version | Where | Means |
| :-- | :-- | :-- |
| Foundation version | `FOUNDATION_VERSION` | Which App-Factory release this repository was built from |
| ECC upstream version | `UPSTREAM_VERSION` in `.ecc/VERSION` | Which upstream ECC release the adapter tracks |
| AgentShield version | `AGENTSHIELD_NPM_VERSION` in `.ecc/VERSION` | Which pinned scanner build runs |

Never report one as another. Bumping the foundation is not an ECC upgrade, and
an ECC upgrade is its own issue and its own ADR.

## Factory provenance

App-Factory v0.1.0 was derived from the reviewed source foundation
`anthracite-labs/Ditto@5d9cc349d264f73e8da913da9d2cea664522237d`.

This is a record of where the *template* came from. Repositories generated from
App-Factory identify themselves by `FOUNDATION_VERSION` and do not inherit that
source project's product history, issue numbers, branch names, or decisions.

## Related

- [ROADMAP.md](ROADMAP.md) — the lifecycle a new repository moves through
- [ARCHITECTURE.md](ARCHITECTURE.md) — the engineering system being instantiated
- [SECURITY.md](SECURITY.md) — the security policy that travels with it
