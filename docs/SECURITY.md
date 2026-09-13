# Security Policy

This repository is an engineering foundation. It contains no application, no
user data, and no deployed service. Its real attack surface is **an AI agent
that reads and executes repository content**, plus the CI that runs on every
pull request. This policy covers exactly that, and travels unchanged into every
repository generated from it.

A repository that later gains an application stack must extend this policy with
the threats of that stack; it must not replace what is here.

## Threat model

| Asset | Threat | Control |
| :-- | :-- | :-- |
| Agent behaviour | Prompt injection via issue bodies, fetched pages, or plan files | Instruction files treat external content as data; `.ecc/rules/security.md` requires reporting, never obeying |
| Credentials | Token committed to Git, or leaked into logs/PR bodies | `scripts/verify.sh` secrets check (CI-enforced); no real credential is ever needed locally |
| Supply chain | Malicious or typosquatted dependency; floating CI action tag | Pinned versions; allowlisted registries; `contents: read` CI permissions |
| CI runner | Workflow that executes untrusted input, or needs excess scope | Minimal permissions; no secrets required by the verify workflow |
| Engineering system | A weakened check that silently passes | Checks fail closed; negative tests assert they can fail; weakening a gate requires justification in review |
| Repository governance | Lifecycle guard disabled to slip in an unreviewed stack | `check_lifecycle` requires an accepted ADR and a matching phase; both directions are self-tested |
| Platform configuration | A generated repository that is unprotected on GitHub | `docs/FACTORY.md` checklist; verification of `main` protection is a required human step |

## Rules that are enforced automatically

`scripts/verify.sh` (run locally and by `.github/workflows/verify.yml`):

- no credential-shaped value in any tracked file;
- no secret-looking `.env*` file committed;
- ECC provenance present and intact, so adapted material stays attributable;
- the CI workflow is wired to the gate and cannot be silently decoupled;
- the required CI job names still match the branch ruleset's required contexts;
- the project lifecycle configuration is well-formed and internally consistent;
- the AgentShield static scan runs clean when the registry is reachable.

### Properties of the automated secrets sweep

Two properties are load-bearing and both are covered by committed negative
tests in `scripts/selftest.sh`:

1. **The detector cannot leak what it finds.** A finding is reported as
   `path:line [category]` only. Matched material never reaches stdout or
   stderr, so an accidentally committed credential is not echoed into CI logs
   by the check meant to catch it. Test: `secrets/redaction` asserts the gate
   fails *and* that the injected value is absent from combined output.
2. **There are no exemptions at all.** No rule skips a line because it contains
   a word such as `example`, `todo`, or `sample`, and no rule skips a value
   because it "looks like a placeholder". Every match is a finding.

   A repeated-character value is caught, because a structurally simple value
   can be a real password — an all-x or all-zero assignment is a plausible
   credential, not evidence of a documentation example. Tests:
   `secrets/repeated-char-password`, `secrets/repeated-char-token`.

   Documentation should therefore avoid credential-shaped examples entirely.
   An empty value or an angle-bracket placeholder does not match the patterns,
   so it needs no exemption; tests `secrets/angle-bracket-not-credential-shaped`
   and `secrets/empty-value-not-credential-shaped` pin that behaviour.

   Tests `secrets/bypass-*` additionally assert that real-looking credentials
   are still caught on lines containing `example`, `todo`, `sample`,
   `placeholder`, and `n/a`.

Dotenv files are enforced rather than merely documented: `check_env_files`
fails if any `.env` or `.env.*` exists in the tree, because `.gitignore` cannot
stop `git add -f`. `.env.example` is the only permitted template.
`config/project.env` is **not** a dotenv file: it is committed lifecycle state,
it is parsed line-by-line rather than sourced, and it must never contain a
secret.

These checks are a floor, not a guarantee — a credential in an unrecognised
shape will pass. Human review remains the control for the rest.

Nothing in `scripts/` executes repository content. Verification parses
(`bash -n`), lints statically (shellcheck), parses YAML and JSON with safe
loaders, and runs the pinned scanner in static mode. `curl` is used only
against `api.github.com`. There is no `curl | sh`, no remote script execution,
and no `sudo` in any repository script.

## Rules that are enforced by review

- No secret in a commit, PR body, issue comment, or log line.
- Least privilege in CI: `contents: read` unless a job proves it needs more.
- Third-party Actions pinned to a full commit SHA; packages pinned to a version.
- Dependencies from `registry.npmjs.org` or `pypi.org` only.
- Any change to `.ecc/**`, `AGENTS.md`, `config/**`, or `scripts/**` is reviewed
  as executable code, because an agent will act on it.
- No script may perform GitHub administration (rulesets, visibility, secrets,
  app installations) without explicit human authorization.
- Mandatory security review triggers are listed in
  `.ecc/rules/security.md`; the procedure is `.ecc/skills/security-review.md`.

## Scanner

AgentShield (`ecc-agentshield@1.4.0`, MIT,
[`affaan-m/agentshield`](https://github.com/affaan-m/agentshield)) is executed
from npm in **static mode only**:

```bash
npx -y ecc-agentshield@1.4.0 scan --format json
```

The deep modes (`--injection`, `--sandbox`, `--taint`, `--deep`) actively
execute or probe configuration and are never run automatically.

**AgentShield is advisory in this foundation, not a security gate.** It targets
Claude Code configuration surfaces (`.claude/`, hooks, MCP config), and an
Arena adapter has none, so it scans zero files. `scripts/verify.sh` therefore
reports it as `SKIP` rather than `PASS` whenever `filesScanned == 0` — a scan
that examined nothing proves nothing, and reporting it as a pass would
advertise coverage that does not exist. The credential controls that actually
apply here are `check_secrets` and `check_env_files`, described above.

## Reporting a security problem

Open a private security report through GitHub's private vulnerability
reporting on this repository, or contact the maintainers directly. Do not open
a public issue for an unpatched exposure.

If a credential is ever committed, treat it as burned: **rotate it first**,
then remove it. Deleting a line does not remove it from history.

---

## App1 product security and privacy discovery requirements

**Status:** discovery requirements, not implementation claims.  
**Lifecycle:** `PROJECT_PHASE=discovery`.

The foundation policy above remains in force unchanged. The requirements below
come from current product discovery in [PRODUCT.md](PRODUCT.md) and constrain
later architecture and validation. Specific cryptographic standards, protocols,
identity providers, authorization systems, storage mechanisms, and deployment
technologies remain architecture decisions.

### 1. Claims must be demonstrated before marketing

> **Never market a privacy/security property before it is technically demonstrated and verified.**

E2EE, relay confidentiality, metadata claims, self-hosting properties,
data-residency promises, and similar claims must be validated against the actual
later implementation before they are stated as guarantees.

### 2. Data and infrastructure control

Long-term product goals include direct/customer-controlled paths where suitable
and organizational control, as practical, over:

- identity;
- policy;
- media infrastructure;
- storage;
- encryption;
- geographic/data placement.

Self-hosted, dedicated managed, and BYOC models remain first-class product
directions. These requirements do not select an implementation mechanism.

### 3. Protected media and E2EE direction

Discovery direction includes:

- E2EE where applicable;
- relays unable to read protected media where the eventual cryptographic model
  provides this;
- direct/customer-controlled paths where suitable.

No cryptographic protocol or standard is approved during discovery.

### 4. Source-owned data and permissions

For live integrations and external objects:

> **The source system remains authoritative for its own data and permissions.**

App1 must not create a shadow ACL universe that silently grants access to
content a user cannot access at the source.

Where live integration can preserve source ownership, permissions, and data
residency, migration/copying into App1 should not be required.

### 5. Identity and contact discovery

Current discovery direction:

- App1 has an internal identity with optional external identifiers;
- phone number is **not mandatory**;
- contact discovery is privacy-first;
- exact username, QR, and invite links are preferred default discovery
  mechanisms;
- mandatory address-book upload is rejected;
- opt-in private contact discovery may be researched later.

Phone-number recovery/discovery and abuse trade-offs remain open research
questions.

### 6. Presence, receipts and notification privacy

Presence should expose minimal information by default and remain
user-controlled. Read receipts and typing indicators should be privacy
configurable.

Notifications should use privacy-aware previews and user-controlled quiet
modes.

### 7. Search, indexing and connected content

Search should avoid assuming that App1 centrally indexes all user/company
content.

Current direction includes:

- device/local search where practical;
- optional remote/BYOC indexing;
- source-specific search for integrations;
- workspace search across connected external objects only while respecting
  source permissions.

Broad centralized indexing is treated as both a privacy/security surface and a
known recurring-cost surface.

### 8. Backup, persistence and storage

App1 should not require mandatory App1 cloud storage.

Current backup/persistence directions include:

- local/export;
- user-selected cloud/BYOC;
- customer-owned persistence;
- App1-managed persistence/backup only when deliberately chosen and
  economically justified.

Persistent workspace context must not imply that all workspace bytes are copied
into App1.

### 9. Remote control and high-risk interaction

Remote control is not a Universal Core default. If/when introduced in
Hybrid/Enterprise or a paid consumer capability, it requires explicit consent
and strong safety controls.

The concrete authorization, session-isolation, confirmation and revocation
mechanisms remain future discovery/architecture work.

### 10. Abuse and unauthenticated use

Current discovery uses account-based onboarding and does not include
unauthenticated calling as an initial default because of abuse risk.

Abuse controls are still part of the open validation plan and must be tested
rather than assumed sufficient.

### 11. Enterprise security direction

Enterprise discovery still needs detailed definition for:

- identity integration;
- SSO/SCIM;
- policy controls;
- audit controls;
- retention;
- compliance;
- data residency;
- federation;
- self-hosting;
- dedicated managed infrastructure;
- BYOC;
- customer AI/models;
- admin UX;
- multi-region/HA requirements.

None of these are implementation-approved yet.

### 12. AI/model data boundaries

AI is not mandatory in Universal Core.

Long-term research includes local/on-device models, customer-hosted models,
customer cloud/model providers, enterprise model gateways, and App1-managed
paid AI.

Product constraint:

> **Do not make every App1 interaction create a vendor AI inference bill or require proprietary data to move into App1-managed AI infrastructure.**

For enterprises, BYO-model/customer-approved AI is a first-class research path.

### 13. Security-relevant economic surfaces

The following are treated as security/privacy and recurring-cost surfaces until
proven otherwise:

- centralized media;
- persistent vendor storage;
- broad indexing;
- recording/transcoding;
- transcription;
- AI inference;
- PSTN/SMS/phone verification;
- continuous synchronization;
- large-scale automated moderation;
- managed infrastructure.

Cost pressure must not silently weaken privacy, access control, reliability, or
security requirements.

## Related product-discovery documents

- [PRODUCT.md](PRODUCT.md) — canonical product discovery and product constraints
- [DOMAIN.md](DOMAIN.md) — source-authority and domain invariants
- [ROADMAP.md](ROADMAP.md) — lifecycle state and discovery exit conditions
