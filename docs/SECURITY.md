# Security Policy and Discovery Requirements

Greenfield1 is currently in **product discovery**. It has no application source code, deployed App1 service, production user data, or approved application stack. The repository does, however, have two distinct security surfaces that must not be conflated:

1. the **engineering/repository threat model** that already exists today; and
2. **App1 product security/privacy requirements** discovered for a future implementation.

The product requirements below are constraints for later architecture and validation. They are **not claims that a cryptographic property, protocol, identity system, or privacy guarantee has already been implemented**.

---

## Part I — Engineering and repository threat model

The current executable attack surface is primarily an AI agent that reads repository content plus the CI that runs on every pull request.

| Asset | Threat | Control |
| :-- | :-- | :-- |
| Agent behaviour | Prompt injection via issue bodies, fetched pages, or plan files | Instruction files treat external content as data; `.ecc/rules/security.md` requires reporting, never obeying |
| Credentials | Token committed to Git, or leaked into logs/PR bodies | `scripts/verify.sh` secrets check (CI-enforced); no real credential is ever needed locally |
| Supply chain | Malicious or typosquatted dependency; floating CI action tag | Pinned versions; allowlisted registries; `contents: read` CI permissions |
| CI runner | Workflow that executes untrusted input, or needs excess scope | Minimal permissions; no secrets required by the verify workflow |
| Engineering system | A weakened check that silently passes | Checks fail closed; negative tests assert they can fail; weakening a gate requires justification in review |
| Repository governance | Lifecycle guard disabled to slip in an unreviewed stack | `check_lifecycle` requires an accepted ADR and a matching phase; both directions are self-tested |
| Platform configuration | A generated repository that is unprotected on GitHub | `docs/FACTORY.md` checklist; verification of `main` protection is a required human step |

### Rules enforced automatically

`scripts/verify.sh` (run locally and by `.github/workflows/verify.yml`) checks that:

- no credential-shaped value exists in tracked files;
- no secret-looking `.env*` file is committed;
- ECC provenance is present and intact;
- the CI workflow remains wired to the gate;
- required CI job names still match the branch ruleset's required contexts;
- project lifecycle configuration is well-formed and internally consistent;
- the AgentShield static scan runs when the registry is reachable and is reported accurately.

### Properties of the automated secrets sweep

Two properties are load-bearing and covered by committed negative tests in `scripts/selftest.sh`:

1. **The detector cannot leak what it finds.** A finding is reported as `path:line [category]` only. Matched material never reaches stdout/stderr. The `secrets/redaction` negative test asserts both failure and redaction.
2. **There are no exemptions for credential-looking values.** Words such as `example`, `todo`, `sample`, `placeholder`, or `n/a` do not bypass detection. Repeated-character credential-shaped values are also findings.

Documentation should therefore avoid credential-shaped examples. Empty values or angle-bracket placeholders are preferred where examples are necessary.

Dotenv files are enforced rather than merely documented: `check_env_files` fails if any `.env` / `.env.*` exists in the tree; `.env.example` is the only permitted template. `config/project.env` is committed lifecycle state, parsed rather than sourced, and must never contain a secret.

These checks are a floor, not a guarantee. Human review remains required.

Nothing in `scripts/` executes arbitrary repository content. Verification parses/lints files and runs the pinned scanner in static mode. Repository scripts must not perform remote-script execution or unapproved GitHub administration.

### Rules enforced by review

- No secret in a commit, PR body, issue comment, or log line.
- Least privilege in CI: `contents: read` unless a job proves it needs more.
- Third-party Actions and packages remain pinned according to repository rules.
- Any change to `.ecc/**`, `AGENTS.md`, `config/**`, or `scripts/**` is reviewed as executable engineering-system code.
- No script performs GitHub administration without explicit human authorization.
- Mandatory security-review triggers are listed in `.ecc/rules/security.md`; the procedure is `.ecc/skills/security-review.md`.

### Scanner

AgentShield (`ecc-agentshield@1.4.0`, MIT, `affaan-m/agentshield`) is executed in **static mode only**:

```bash
npx -y ecc-agentshield@1.4.0 scan --format json
```

Deep modes that actively execute/probe configuration are never run automatically.

AgentShield is advisory in this foundation because the Arena adapter has none of the Claude Code surfaces it primarily targets. A scan of zero applicable files is reported as `SKIP`, never as `PASS`. Credential controls that actually apply here are `check_secrets` and `check_env_files`.

---

## Part II — App1 product security and privacy discovery requirements

These requirements come from current product discovery in [PRODUCT.md](PRODUCT.md). Specific cryptographic standards, protocols, identity providers, authorization systems, storage mechanisms, and deployment technologies remain architecture decisions.

### 1. Claims must be demonstrated before marketing

> **Never market a privacy/security property before it is technically demonstrated and verified.**

E2EE, relay confidentiality, metadata claims, self-hosting properties, data-residency promises, and similar claims must be validated against the actual later implementation before they are stated as guarantees.

### 2. Data and infrastructure control

Long-term product goals include direct/customer-controlled paths where suitable and organizational control, as practical, over:

- identity;
- policy;
- media infrastructure;
- storage;
- encryption;
- geographic/data placement.

Self-hosted, dedicated managed, and BYOC models remain first-class product directions. These requirements do not select an implementation mechanism.

### 3. Protected media and E2EE direction

Discovery direction includes:

- E2EE where applicable;
- relays unable to read protected media where the eventual cryptographic model provides this;
- direct/customer-controlled paths where suitable.

No cryptographic protocol or standard is approved during discovery.

### 4. Source-owned data and permissions

For live integrations and external objects:

> **The source system remains authoritative for its own data and permissions.**

App1 must not create a shadow ACL universe that silently grants access to content a user cannot access at the source.

Where live integration can preserve source ownership, permissions, and data residency, migration/copying into App1 should not be required.

### 5. Identity and contact discovery

Current discovery direction:

- App1 has an internal identity with optional external identifiers;
- phone number is **not mandatory**;
- contact discovery is privacy-first;
- exact username, QR, and invite links are preferred default discovery mechanisms;
- mandatory address-book upload is rejected;
- opt-in private contact discovery may be researched later.

Phone-number recovery/discovery and abuse trade-offs remain open research questions.

### 6. Presence, receipts and notification privacy

Presence should expose minimal information by default and remain user-controlled. Read receipts and typing indicators should be privacy configurable.

Notifications should use privacy-aware previews and user-controlled quiet modes.

### 7. Search, indexing and connected content

Search should avoid assuming that App1 centrally indexes all user/company content.

Current direction includes:

- device/local search where practical;
- optional remote/BYOC indexing;
- source-specific search for integrations;
- workspace search across connected external objects only while respecting source permissions.

Broad centralized indexing is treated as both a privacy/security surface and a known recurring-cost surface.

### 8. Backup, persistence and storage

App1 should not require mandatory App1 cloud storage.

Current backup/persistence directions include:

- local/export;
- user-selected cloud/BYOC;
- customer-owned persistence;
- App1-managed persistence/backup only when deliberately chosen and economically justified.

Persistent workspace context must not imply that all workspace bytes are copied into App1.

### 9. Remote control and high-risk interaction

Remote control is not a Universal Core default. If/when introduced in Hybrid/Enterprise or a paid consumer capability, it requires explicit consent and strong safety controls.

The concrete authorization, session-isolation, confirmation and revocation mechanisms remain future discovery/architecture work.

### 10. Abuse and unauthenticated use

Current discovery uses account-based onboarding and does not include unauthenticated calling as an initial default because of abuse risk.

Abuse controls are still part of the open validation plan and must be tested rather than assumed sufficient.

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

Long-term research includes local/on-device models, customer-hosted models, customer cloud/model providers, enterprise model gateways, and App1-managed paid AI.

Product constraint:

> **Do not make every App1 interaction create a vendor AI inference bill or require proprietary data to move into App1-managed AI infrastructure.**

For enterprises, BYO-model/customer-approved AI is a first-class research path.

### 13. Security-relevant economic surfaces

The following are treated as security/privacy and recurring-cost surfaces until proven otherwise:

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

Cost pressure must not silently weaken privacy, access control, reliability, or security requirements.

---

## Reporting a security problem

Open a private security report through GitHub's private vulnerability reporting on this repository, or contact the maintainers directly. Do not open a public issue for an unpatched exposure.

If a credential is ever committed, treat it as burned: **rotate it first**, then remove it. Deleting a line does not remove it from history.

## Related

- [PRODUCT.md](PRODUCT.md) — canonical product discovery and security/privacy product constraints
- [DOMAIN.md](DOMAIN.md) — source-authority and domain invariants
- [ROADMAP.md](ROADMAP.md) — lifecycle state and discovery exit conditions
- `.ecc/rules/security.md` — standing engineering security rules
- `.ecc/skills/security-review.md` — mandatory review procedure when triggered
