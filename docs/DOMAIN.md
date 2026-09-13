# Domain — App1 discovery vocabulary

**Status:** provisional; discovery in progress  
**Lifecycle:** `PROJECT_PHASE=discovery`

This file records the current product-domain vocabulary and invariants that have emerged during App1 discovery. These definitions are **not** implementation classes, schemas, APIs, database models, or architecture decisions.

The canonical product requirements live in [PRODUCT.md](PRODUCT.md). GitHub Issue #1 preserves discovery discussion and provenance.

---

## 1. Core concepts

| Term | Meaning in current discovery | Does NOT imply |
| :-- | :-- | :-- |
| **App1** | A sovereign collaboration fabric delivered through one seamless application. | A specific framework, protocol, database, hosting provider, or implementation stack. |
| **Collaboration context** | The shared context around people, conversations, sessions, decisions, references, files/objects, and allowed actions. | That App1 must own or copy every underlying object. |
| **Conversation** | A persistent interaction context in which text, calls, media, files, screen sharing, and related communication can coexist. | Separate products for messaging vs calling. |
| **Universal Core** | The global base communication layer for ordinary users. | Community/server structure or enterprise administration. |
| **Workspace** | A persistent collaboration context that can contain people, conversations, live sessions, shared context, decisions, references, external objects, and allowed actions. | Mandatory App1-hosted persistence for all workspace bytes. |
| **Community Workspace** | A persistent shared project/interest space for informal groups, communities, clubs, study groups, gamers, creators, and similar users. | A Discord clone, social network, or full productivity suite. |
| **Hybrid / Professional Workspace** | The still-open professional collaboration layer for developers, freelancers, startups, agencies, researchers, open-source teams, and small businesses. | A finalized feature contract; discovery is still pending. |
| **Corporate / Enterprise** | The still-open organizational layer for identity, policy, audit, compliance, sovereignty, self-hosting, dedicated managed infrastructure, BYOC, and related controls. | A finalized enterprise architecture. |
| **Capability Fabric** | Cross-cutting capabilities such as integrations, storage, identity, automation, agents, AI/models, search, interoperability, federation, and managed capabilities. | That every capability is built in or enabled by default. |
| **Capability Pack / Module** | A coarse optional capability grouping that can add depth without bloating the global base app. | Hundreds of microscopic plugins. |
| **External Object** | A live or referenced object whose source system may remain authoritative, such as a Drive file, GitHub issue, Jira task, Linear issue, Figma/Miro artifact, or customer model endpoint. | Copying the object or its permissions into App1. |
| **Source System** | The external system that owns authoritative data and permissions for its own objects. | App1 having permission to override source ACLs. |
| **Direct path** | A communication/data path that avoids unnecessary App1-managed infrastructure where practical. | Any specific transport or protocol. |
| **Relay / fallback** | Bounded infrastructure used when direct communication is not practical or reliable enough. | A specific relay technology or provider. |
| **BYOC** | Customer-owned cloud/infrastructure used for applicable App1 capabilities or workloads. | A selected cloud vendor or deployment mechanism. |
| **Customer-run** | A capability executed on customer-controlled infrastructure, storage, cloud, or models. | A specific packaging/orchestration system. |
| **Paid-managed** | An App1-hosted capability whose marginal cost is explicitly covered by customer revenue. | That App1 should host all workloads. |
| **Federation** | Long-term cross-system or cross-organization interoperability where justified. | A selected federation protocol or a Universal Core MVP requirement. |

---

## 2. Product layers and progression

App1 is one product with progressive capability depth:

1. **Universal Core** — ordinary communication.
2. **Community / Personal Workspace** — richer informal persistent collaboration.
3. **Hybrid / Professional Workspace** — professional work context; still in discovery.
4. **Corporate / Enterprise** — organizational sovereignty and control; still in discovery.
5. **Cross-cutting Capability Fabric** — optional capabilities that can span layers.

A user/group should be able to move toward richer capability without being forced into a separate-product mental model.

Current UX invariant:

> **One experience. Progressive capabilities. Context-specific complexity. Modular delivery.**

---

## 3. Capability ownership classes

Every major capability must receive one of these discovery verdicts before acceptance:

| Verdict | Meaning |
| :-- | :-- |
| **CORE-NATIVE** | App1 owns it because it defines the base product experience. |
| **MODULE-NATIVE** | App1 owns it, but it is optional and activated only where needed. |
| **LIVE-INTEGRATED** | The source system stays authoritative while App1 provides context, preview, search, and/or actions. |
| **CUSTOMER-RUN** | The capability executes on customer-controlled infrastructure, storage, cloud, or models. |
| **PAID-MANAGED** | App1 hosts the workload because customer revenue covers the recurring marginal cost. |
| **DEFER / REJECT** | Complexity, cost, attack surface, app weight, operational burden, or weak user value do not justify the capability. |

These verdicts are product-discovery classifications, not architecture selections.

---

## 4. Interoperability model

Integration is layered rather than universal. The current interoperability ladder is:

1. link;
2. preview;
3. live object;
4. read connector;
5. action connector;
6. cross-organization collaboration;
7. protocol federation.

Different external systems may stop at different levels.

Potential integration methods to research include native APIs, delegated authorization, webhooks/events, MCP, open protocols, private/custom connectors, and federation standards. No method is approved as the universal mechanism.

---

## 5. Domain invariants

### 5.1 Source authority

> **The source system remains authoritative for its own data and permissions.**

App1 must not create a shadow ACL universe that grants access to content a user cannot access at the source.

### 5.2 No-migration-by-default

> **No migration required where live integration can preserve source ownership, permissions, and data residency.**

A workspace may be persistent context without becoming persistent App1-owned bytes.

### 5.3 Experience ownership vs workload ownership

> **App1 owns the collaboration experience and context — not necessarily every workload, dataset, model, file, or external system underneath it.**

Integration is preferred over duplication when another authoritative system already solves the workload well.

### 5.4 Capability-state separation

The following are distinct states and must remain separable in later design:

- capability available;
- capability installed;
- capability permitted;
- capability licensed.

### 5.5 Cost discipline

Near-zero/very-low vendor marginal cost is a product constraint. Where user experience and reliability allow, prefer:

1. direct/local;
2. customer-owned/customer-funded;
3. BYOC;
4. fixed/predictable dedicated infrastructure;
5. bounded App1-managed fallback;
6. externally metered services only when strategically justified.

### 5.6 Privacy and trust

Privacy-sensitive state such as presence, receipts, typing, contact discovery, external-object access, and workspace visibility is user/context controlled rather than globally exposed by default.

No privacy/security property may be marketed before it is technically demonstrated and verified.

### 5.7 Progressive complexity

Universal Core should remain simple for ordinary users. Rich structure, roles, policies, modules, integrations, and administration appear only when the context needs them.

### 5.8 No implicit implementation

Terms such as direct, relay, E2EE, BYOC, identity, federation, workspace, module, integration, and external object describe product intent. They do **not** approve transports, cryptographic standards, frameworks, auth providers, databases, hosting providers, APIs, or data models.

---

## 6. Provisional relationship/state rules

These are discovery-level behavior rules, not implementation state machines.

| From / context | Event / need | Resulting product state |
| :-- | :-- | :-- |
| Small conversation/group | Group needs persistent shared structure | It may evolve into a Community Workspace without a hard migration. |
| Universal/Core context | Professional capability is required | Hybrid/Professional capability may be enabled once that contract is defined. |
| Workspace | User references an external object | Object may remain source-owned while App1 stores only the reference/context needed. |
| External object | User attempts an action | Source permissions remain authoritative; App1 must not silently elevate access. |
| Direct communication | Direct path is unavailable/insufficient | Bounded fallback may be used automatically; ordinary users should not manually choose paths. |
| Capability | Context does not need it | It need not be installed, permitted, licensed, or shown. |
| Cost-bearing capability | Recurring App1 cost is material | Prefer customer-run/BYOC or explicit paid-managed treatment rather than hiding the cost in a free baseline. |

---

## 7. Known product-domain rules by layer

### Universal Core

- one seamless conversation model;
- small groups, not server/community-scale structure;
- direct-first file transfer is a first-class differentiator;
- screen sharing is Core; remote control is not;
- phone number is not mandatory;
- contact discovery is privacy-first;
- AI is not a mandatory Core capability;
- lightweight integrations must not turn Core into another email/document/productivity suite.

### Community / Personal Workspace

- any group can evolve naturally into a persistent space;
- structure is adaptive rather than channel-heavy by default;
- App1 is not the mandatory file host;
- notes/checklists/events may be lightweight and native, while rich document/project/whiteboard/calendar systems are generally integrated;
- invite-first/private-first discoverability;
- strong manual moderation before costly automated moderation;
- Community is an optional capability pack;
- no ads.

### Hybrid / Professional, Enterprise, Capability Fabric

These remain open discovery areas. Do not infer detailed entities, permissions, workflows, or state transitions until their capability harvests are founder-approved and recorded in [PRODUCT.md](PRODUCT.md).

---

## 8. Engineering foundation terms

These continue to describe repository engineering rather than the product domain:

| Term | Meaning here |
| :-- | :-- |
| **Foundation** | The generic engineering system shipped by App-Factory. |
| **Adapter** | `.ecc/` — the ECC-on-Arena adaptation. Not native ECC. |
| **Skill / workflow** | An on-demand Markdown procedure under `.ecc/skills/`. |
| **Rule** | A standing, always-in-force constraint under `.ecc/rules/`. |
| **Role** | A sequential review persona under `.ecc/roles/` (not a subagent). |
| **Gate** | `scripts/verify.sh` — deterministic, non-zero on failure. |
| **Lifecycle phase** | `PROJECT_PHASE` in `config/project.env`. |
| **No-stack guard** | The `no_app_stack` check, driven by `ALLOW_APP_STACK`. |
| **Project memory** | `docs/MEMORY.md` — append-only, Git-tracked. |
| **ADR** | A record under `docs/decisions/` for a durable technical trade-off. |

## Related

- [PRODUCT.md](PRODUCT.md) — canonical product discovery
- [ROADMAP.md](ROADMAP.md) — lifecycle sequencing and discovery progress
- [SECURITY.md](SECURITY.md) — foundation security controls plus product security/privacy discovery requirements
- [ARCHITECTURE.md](ARCHITECTURE.md) — engineering foundation; application architecture is not authorized yet
- [decisions/](decisions/README.md) — technical decision records when the lifecycle later permits them
