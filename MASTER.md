# App1 Master Discovery Register

**Status:** active discovery source of truth  
**Repository:** `anthracite-labs/Greenfield1`  
**Product:** App1  
**Lifecycle intent:** discovery  
**Architecture/stack authorization:** none  

> This document consolidates founder-approved discovery decisions, research findings, explicit supersessions, open hypotheses, economic constraints, capability boundaries, and next research questions discussed through 2026-09-13.
>
> It is a discovery artifact, not an architecture ADR and not implementation authorization.

---

## 1. Current working definition

App1 is a **sovereign collaboration fabric delivered through one seamless application**.

It combines a lightweight universal communications core with progressively richer workspaces and organization capabilities, while allowing users and organizations to keep their existing data, infrastructure, storage, tools, and intelligence where appropriate.

The key product principle is:

> **App1 owns the collaboration experience and context — not necessarily every workload, dataset, model, file, or external system underneath it.**

The original infrastructure/economic principle remains:

> **Direct when possible. Dedicated when necessary. Yours when you want it.**

App1 is therefore **not** merely:

- a WhatsApp clone;
- a Signal clone;
- a Zoom clone;
- a Teams clone;
- a Discord clone;
- a Slack clone;
- a Notion clone;
- an IDE;
- an AI agent platform;
- a productivity suite;
- a social network;
- a giant centralized media cloud.

It is intended to be the collaboration layer that makes communication, workspaces, and external systems feel coherent without requiring App1 to rebuild or own all of them.

---

## 2. Product layers

App1 is currently modeled as one product with progressive capability depth.

### 2.1 Universal Core — average user

Primary audience:

- ordinary consumers;
- friends;
- families;
- privacy-conscious users;
- anyone needing daily communication.

Reference class:

- WhatsApp;
- Signal;
- Telegram;
- Zoom/Teams call controls where relevant.

The Universal Core is the global base app. It should feel immediately familiar and exceptionally clean while supporting richer communication than a basic messenger.

### 2.2 Community / Personal Workspace

Primary audience:

- students;
- study groups;
- gamers;
- clubs;
- hobby groups;
- creators;
- friend groups;
- communities;
- informal projects.

Reference class:

- Discord;
- Telegram communities;
- Slack interaction patterns;
- Miro/FigJam where lightweight collaboration helps.

A normal group should be able to **grow naturally into a persistent shared space** without forcing users through a migration or new-product mental model.

### 2.3 Hybrid / Professional Workspace

Primary audience:

- developers;
- freelancers;
- consultants;
- startups;
- agencies;
- researchers;
- open-source teams;
- small businesses;
- small professional teams.

Reference class to research next:

- Slack;
- Notion;
- Linear;
- GitHub/GitLab;
- Jira;
- Figma;
- Miro;
- Google Workspace;
- Microsoft 365;
- developer/productivity tools.

This layer is not yet fully defined.

### 2.4 Corporate / Enterprise

Primary audience:

- corporations;
- regulated organizations;
- security-sensitive organizations;
- infrastructure-sovereign organizations;
- enterprises requiring self-hosting, dedicated infrastructure, BYOC, policy, audit, and identity controls.

Reference class to research later:

- Teams;
- Zoom Workplace;
- Slack Enterprise;
- Microsoft 365;
- Matrix/Element;
- enterprise identity, compliance, BYOC, and federated collaboration systems.

This layer is not yet fully defined.

### 2.5 Cross-cutting Capability Fabric

Capabilities that may span layers:

- integrations;
- external storage;
- customer-owned cloud;
- customer-owned AI/models;
- automation;
- agents;
- identity;
- search;
- interoperability;
- federation;
- MCP/API/webhook connectors;
- paid managed capabilities.

These are not automatically part of the base app.

---

## 3. One seamless app, modular underneath

The product should present itself as **one App1** rather than separate consumer/business/enterprise applications.

However, installed capability should not equal total platform capability.

The current product principle is:

> **One experience. Progressive capabilities. Context-specific complexity. Modular delivery.**

The base application should remain lightweight enough for the global average user.

Richer capability can be delivered through coarse optional modules/capability packs such as:

- Community;
- Hybrid/Professional;
- Enterprise;
- heavyweight collaboration capabilities;
- selected integrations;
- specialized tools.

Avoid hundreds of microscopic plugins. Modularization should reduce app size, attack surface, permissions, startup cost, and cognitive load rather than becoming another complexity source.

Important distinctions:

- capability available;
- capability installed;
- capability permitted;
- capability licensed.

These are different states and should remain separable in later product/architecture work.

---

## 4. Capability ownership classification

Every future capability must receive an explicit ownership verdict before acceptance.

### CORE-NATIVE

App1 must own it because it defines the product experience.

### MODULE-NATIVE

App1 owns it, but it should be optional/downloadable/activated only where needed.

### LIVE-INTEGRATED

The external system remains authoritative. App1 provides native-feeling context, preview, search, and/or actions without unnecessarily copying or replacing the source system.

### CUSTOMER-RUN

The capability executes on customer infrastructure, storage, cloud, or models.

### PAID-MANAGED

App1 hosts the workload because customer revenue explicitly covers the associated marginal cost.

### DEFER / REJECT

The capability does not justify its product complexity, operational burden, app weight, security surface, or recurring cost.

---

## 5. Universal Core contract

### 5.1 Core interaction model

Universal Core should use **one seamless conversation model**.

Text, voice, video, files, media, screen sharing, and calls are capabilities of the same relationship/context rather than separate products.

The experience should remain **WhatsApp-simple** even when deeper capability exists.

### 5.2 Core communication capabilities

Founder-approved Core direction includes:

- text messaging;
- voice calls;
- video calls;
- small-group chat;
- small-group calls;
- screen sharing;
- direct-first file transfer;
- media sharing;
- voice messages;
- video messages;
- conversation history/context;
- message replies;
- reactions;
- privacy controls;
- search;
- multi-device continuity;
- notifications;
- optional lightweight integrations.

Calls should remain part of conversation context/history without flooding the message timeline with noisy call metadata.

### 5.3 Group behavior

Core starts with **small groups**, not server/community-scale structures.

Community structure belongs to the Community capability layer.

### 5.4 Async media

Voice and video messages are first-class communication objects.

Do not turn this into Stories/Reels/social-feed behavior.

### 5.5 Photos and video

Default should optimize sharing sensibly while preserving an original-quality option.

Avoid artificial quality degradation where the transport/cost model does not require it.

### 5.6 Direct file transfer

Direct file transfer is a core differentiator.

Desired behavior:

- direct-first where practical;
- resumable;
- no arbitrary App1 size cap when a transfer is truly direct and device/network limits permit it;
- optional persistence only when needed;
- configured cloud/BYOC can be used for persistence;
- when recipient is offline, queue where practical and optionally offer temporary or configured persistent storage.

The product should exploit cases where a better user experience is also cheaper for App1.

### 5.7 Screen sharing

Screen sharing belongs in Core.

It should be available from an active conversation and easy to escalate from a call.

Remote control is **not** a default Core capability.

Current direction:

- first belongs in Hybrid/Enterprise;
- may later become a paid consumer capability;
- always requires explicit consent and strong safety controls.

### 5.8 Identity

Target direction:

- internal App1 identity;
- optional external identifiers;
- long-term vendor-neutral identity direction.

Phone number should **not be mandatory**.

Phone-number recovery/discovery trade-offs still require research.

### 5.9 Contact discovery

Privacy-first default.

Preferred direction:

- exact username;
- QR;
- invite links;
- potentially opt-in private contact discovery later;
- no mandatory address-book upload.

### 5.10 Presence, receipts, typing

Presence should expose minimal information by default and be user-controlled.

Read receipts and typing indicators should be privacy configurable.

### 5.11 Message editing/deletion

Consumer Core should support visible editing state.

Enterprise contexts may require richer edit history/policy later.

Deletion and disappearing-message behavior should be policy/context aware rather than hard-coded globally.

### 5.12 Search

Direction:

- device/local search by default where practical;
- optional remote/BYOC index;
- source-specific search for integrations;
- do not assume App1 must centrally index all user/company content.

### 5.13 Multi-device and backup

Multi-device continuity is essential.

The security model must preserve appropriate encryption and offline continuity.

Backup direction:

- local/export;
- user-selected cloud/BYOC;
- App1-managed backup only as an optional paid service where justified.

### 5.14 Notifications

Desired experience combines:

- smart bundling;
- privacy-aware previews;
- context-aware priority;
- user-controlled quiet modes.

### 5.15 Call UX

Minimal by default.

Advanced controls appear progressively based on context/device/user need.

### 5.16 Connection transparency

Use a subtle trust/path indicator in normal UX and detailed diagnostics on demand.

Do not require ordinary users to choose P2P vs relay manually.

### 5.17 AI in Core

**No built-in AI in Universal Core.**

AI belongs to an optional future capability layer, not the product's mandatory brain.

### 5.18 Consumer integrations

Lightweight integrations are allowed if they stay optional and do not bloat Core.

Examples worth studying:

- Gmail/Calendar;
- Google Drive;
- Dropbox;
- OneDrive.

But:

- Gmail integration must not turn App1 into an email client;
- Drive-style integration should prefer references/live objects rather than copying files into App1;
- external systems should remain authoritative where possible.

### 5.19 Explicit Core non-goals

Core should reject:

- advertising;
- algorithmic engagement feeds;
- Stories/social-feed direction;
- wallet/payments/commerce as a core product category;
- mandatory App1 cloud storage;
- mandatory AI;
- mini-app clutter;
- unnecessary enterprise complexity.

### 5.20 Core economic rule

> **Free where App1 marginal cost is negligible; charge where App1 incurs genuine recurring cost; preserve customer-run/BYOC alternatives wherever practical.**

### 5.21 Core success condition

Core succeeds when:

- users willingly move valuable conversations into App1;
- users repeatedly invite others;
- those conversation pairs/groups continue using App1;
- App1 becomes useful for ordinary communication rather than one-off novelty;
- economics remain sustainable.

Consumer headline positioning remains unresolved and needs further invention/research.

---

## 6. Community / Personal Workspace contract

### 6.1 Product identity

A Community Workspace is a **persistent shared project/interest space containing people, conversation, voice/video, files, and shared context**.

Any group should be able to evolve naturally into one without a hard migration step.

UX rule:

> Start simple. Expose structure only when the group actually needs it.

### 6.2 Structure

Channels are acceptable, but they must not force Discord/Slack-style configuration complexity onto every group.

Preferred direction:

- main conversation;
- channels/topics/threads where useful;
- adaptive structure as groups grow.

### 6.3 Voice and video

Desired behavior:

- instant contextual voice spaces;
- small/group video;
- screen sharing;
- presentation/watch-style modes where useful;
- optional scheduling for events;
- live collaboration should not feel like creating a formal meeting every time.

### 6.4 Files

Do **not** make App1 the mandatory host of workspace files.

Preferred model:

- direct transfer;
- persistent references;
- external cloud objects;
- optional user/customer storage;
- App1-hosted persistence only where deliberately chosen/paid.

### 6.5 Notes/docs

Do not build a full office suite.

Direction:

- lightweight native notes where useful;
- integrate live external documents (Docs/Notion/etc.);
- external professional document systems remain authoritative.

### 6.6 Tasks

Community may include simple shared checklists.

Richer project/task management belongs in Hybrid or integrations.

### 6.7 Events/calendar

Community can support basic events plus calendar integrations.

Do not build a full calendar replacement.

### 6.8 Roles and permissions

Use simple defaults first.

Advanced roles appear only when the group needs them.

### 6.9 Moderation

Strong manual/moderator controls first.

Automated moderation may be an optional later capability, especially if it creates inference/COGS costs.

### 6.10 Discoverability

Privacy-first and invite-first by default.

Public discoverability may become optional later.

App1 should not design the Community layer primarily around giant public communities.

### 6.11 Bots and activities

Safe bot/integration hooks are desirable, but the normal user experience must remain clean.

Selected collaborative activities can exist where they materially improve the shared experience.

Do not blindly recreate a giant Discord-style app/activity marketplace.

### 6.12 Gaming

Gaming can become an optional capability pack.

Potentially useful:

- rich presence;
- voice;
- screen share;
- activity/game status.

Do not turn App1 into a gaming launcher.

### 6.13 Student/study use

Student/community scenarios may combine:

- group chat;
- voice/video;
- files;
- screen sharing;
- notes;
- events;
- study rooms;
- external Drive/Docs/LMS integrations.

### 6.14 Creator/public community use

Broadcast/community capability can be investigated later as an optional pack.

It is not the universal Community baseline.

### 6.15 Whiteboards

Do not build a full professional whiteboard product by default.

Direction:

- lightweight native sketching may be useful;
- integrate Miro/FigJam-class professional boards.

### 6.16 Polls

Basic polls are useful.

Do not expand this into a full forms/survey product unless evidence later justifies it.

### 6.17 Knowledge/wiki

No native full wiki requirement.

Persistent pinned/shared context may exist, but professional knowledge systems should generally remain external/integrated.

### 6.18 Search

Workspace search should eventually span:

- messages;
- files/references;
- workspace context;
- connected external objects.

It must respect source permissions and should avoid expensive centralized indexing by default.

### 6.19 Notifications and presence

Per-space controls plus context-aware prioritization.

Presence may become richer inside workspaces but remains privacy controlled.

### 6.20 Identity in workspaces

Use a core identity with workspace-specific profile/presentation where useful.

### 6.21 Guests

External/temporary guests may be allowed through invite/link flows with strong abuse controls.

### 6.22 Federation

Keep the product/data model compatible with future federation, but federation is not a Community MVP requirement.

### 6.23 AI

Community AI is optional later.

It is not required in the Community baseline.

### 6.24 Community monetization

No ads.

Monetization should come from real value or real cost surfaces such as:

- storage;
- relay/capacity;
- premium modules;
- paid managed capabilities.

### 6.25 Explicit Community non-goals

Unless future evidence materially changes the decision, App1 should not build native replacements for:

- full office/docs suites;
- full project-management suites;
- full professional whiteboards;
- full calendar products;
- full streaming platforms.

Community must explicitly avoid becoming:

- Discord clone;
- social network;
- creator monetization platform;
- productivity-suite monster;
- gaming launcher.

### 6.26 Community delivery model

Community should be an optional capability pack that can be dynamically enabled when a user creates or joins a workspace.

### 6.27 Community economic rule

Use:

- P2P/direct where possible;
- user/customer cloud for persistence where appropriate;
- paid App1 persistence only when deliberately chosen.

### 6.28 Community success condition

Community succeeds when groups choose App1 instead of juggling multiple disconnected tools such as messaging + voice + files + meeting apps, while App1 stays simple and economically sustainable.

---

## 7. Infrastructure and sovereignty thesis

The long-term product direction includes:

- peer-to-peer/direct-first individual communication;
- bounded relay fallback;
- self-hosted organizational deployments;
- dedicated managed organizational deployments;
- enterprise BYOC;
- customer-owned storage and models where appropriate;
- federation as a long-term differentiator.

Organizations should ultimately be able to control as much as practical of:

- identity;
- policy;
- media infrastructure;
- storage;
- encryption;
- geographic/data placement.

The vendor control plane should remain lightweight relative to media/data workloads where possible.

Specific transports, protocols, frameworks, hosting providers, databases, auth providers, and implementation mechanisms remain **unapproved architecture questions**.

---

## 8. Persistent workspace / BYOC principle

A persistent App1 workspace should not imply that all workspace bytes live in App1.

A workspace can instead be a persistent graph of:

- people;
- conversations;
- live sessions;
- shared context;
- decisions;
- references;
- external objects;
- allowed actions.

Example external objects:

- SharePoint/OneDrive files;
- Google Drive files;
- GitHub PRs/issues;
- Jira/Linear tasks;
- Figma/Miro artifacts;
- S3/object-storage data;
- internal enterprise systems;
- customer AI/model endpoints.

Strong principle:

> **No migration required where live integration can preserve source ownership, permissions, and data residency.**

An enterprise should not have to move all documents, models, files, or knowledge into App1 merely to collaborate through App1.

---

## 9. Integration and interoperability principles

### 9.1 Integration is layered, not universal

Do not promise "connect anything" as if all systems expose the same capabilities.

Use an interoperability ladder:

1. link;
2. preview;
3. live object;
4. read connector;
5. action connector;
6. cross-organization collaboration;
7. protocol federation.

Different external systems may stop at different levels.

### 9.2 Source ownership and permissions

Default principle:

> **The source system remains authoritative for its own data and permissions.**

App1 should not create a shadow ACL universe that accidentally grants access to content a user could not access at the source.

### 9.3 Integration methods to investigate

- native APIs;
- OAuth/OIDC delegated authorization;
- webhooks/events;
- MCP;
- open protocols;
- private/custom connectors;
- federation standards where appropriate.

MCP is worth serious research but should not be the only integration mechanism.

### 9.4 App1 should integrate both directions

Research direction:

- App1 consumes external systems;
- external tools/agents may eventually consume permitted App1 context/actions.

Potential future App1 surfaces may expose permitted operations such as:

- find conversation context;
- find a shared object;
- start a collaboration session;
- send a message;
- create/join workspace;
- access approved meeting/workspace context.

No specific API/protocol decision is approved yet.

---

## 10. AI/model direction

AI is **not** the defining App1 proposition and is explicitly excluded from Universal Core baseline.

Long-term capability directions to research:

- no AI;
- on-device/local model;
- customer-hosted model;
- customer Azure/OpenAI/Bedrock/etc.;
- enterprise model gateway;
- App1-managed paid AI.

Key principle:

> Do not make every App1 interaction create a vendor AI inference bill.

For enterprises, BYO-model/customer-approved AI should be a first-class research path so organizations do not have to migrate or expose proprietary models and knowledge to App1-managed infrastructure.

---

## 11. Economic model and cost discipline

Near-zero/very-low vendor marginal cost remains a core product constraint, not merely a backend optimization.

The cost rule should apply to:

- media;
- files;
- storage;
- indexing;
- AI inference;
- transcription;
- recording;
- sync;
- moderation;
- integrations;
- backups;
- managed infrastructure.

### 11.1 Preferred cost order

Where user experience and reliability allow:

1. direct/local;
2. customer-owned/customer-funded;
3. BYOC;
4. fixed/predictable dedicated infrastructure;
5. bounded App1-managed fallback;
6. externally metered services only when strategically justified.

### 11.2 Known expensive surfaces

Treat these as explicitly cost-bearing until proven otherwise:

- unlimited relay;
- centralized media;
- vendor-hosted persistent storage;
- broad centralized indexing;
- recording/transcoding;
- transcription;
- AI inference;
- PSTN/SMS/phone verification;
- continuous high-frequency synchronization;
- large-scale automated moderation.

### 11.3 Operating metrics retained

Four original metrics remain first-class:

1. direct-connect rate;
2. relay bytes per free user-hour;
3. concurrent participants per relay dollar;
4. operator minutes per customer per month.

No one metric may be optimized by making another economically unsustainable.

### 11.4 Benchmark-first thresholds

Do not invent arbitrary numeric thresholds before representative testing.

Current direction:

- benchmark direct-connect distributions first;
- define relay limits by actual cost per free user-hour;
- derive economic ceiling from validated conversion/LTV assumptions;
- benchmark mainstream call setup/reliability rather than guessing;
- use call completion + recovery + perceptual quality as reliability dimensions.

### 11.5 Degraded networks

Desired behavior:

- preserve audio;
- preserve low-resolution video where practical;
- prioritize smooth continuity;
- around 2% packet loss should remain usable as an initial target;
- final acceptance should be perceptual/recovery based, not raw packet-loss based.

---

## 12. Realtime infrastructure research register

Reference providers studied or queued for continued comparison include:

- GetStream.io;
- LiveKit;
- Daily;
- Agora;
- Twilio;
- Sendbird;
- 100ms;
- Vonage and adjacent providers.

Purpose of this category:

- harvest mature communication primitives;
- benchmark SDK/developer experience;
- identify commodity capabilities;
- calculate build-vs-buy economics;
- quantify how usage-linked managed infrastructure compares with App1's direct/customer-funded thesis.

### 12.1 GetStream.io role

Treat GetStream primarily as:

- communication capability benchmark;
- SDK/DX benchmark;
- managed-COGS counterfactual.

Do not assume it is the architecture choice.

### 12.2 LiveKit role

LiveKit is particularly important as an eventual architecture-stage reference because it supports both managed and serious self-hosted realtime models.

It remains a research/adopt-extend candidate only; no decision has been made.

---

## 13. Reliability, self-hosting, and operations requirements

### 13.1 Reliability

Target is **mainstream conferencing-class**, not experimental best effort.

Direct→relay failover may have a brief interruption if recovery is reliable and understandable.

### 13.2 Self-hosting

Self-hosting remains first-class in the long-term product.

Target operator:

- competent IT administrator;
- not a realtime-media specialist;
- not a dedicated SRE team requirement.

Installation time is less important than eliminating specialist knowledge.

Routine operator effort should approach zero.

### 13.3 Upgrade experience

Preferred product behavior:

- preflight compatibility/health checks;
- clear release/impact summary;
- selectable automatic vs controlled policy;
- admin approval where required;
- maintenance scheduling;
- staged/canary rollout where possible;
- post-upgrade health verification;
- safe rollback;
- enterprise deferral within supported security windows.

This is a product requirement, not an implementation decision.

---

## 14. Security and privacy direction

Long-term goals include:

- direct/customer-controlled paths where suitable;
- E2EE where applicable;
- relays unable to read protected media where the cryptographic model provides this;
- enterprise identity integration;
- policy controls;
- audit controls;
- customer infrastructure/data control.

Important rule:

> **Never market a privacy/security property before it is technically demonstrated and verified.**

Specific cryptographic standards and protocol choices remain architecture decisions.

---

## 15. Network effects and acquisition strategy

App1 should not demand that users "move their network" before receiving value.

Current discovery direction:

- use existing apps/services as distribution rails;
- invite to a concrete interaction rather than to "another messenger";
- preserve invite context through install/account creation where possible;
- resume the intended interaction after onboarding;
- earn primary-app status through repeated superior experiences.

Potential interaction triggers include:

- large direct file transfer;
- private/direct call;
- screen-share/collaboration invitation;
- conversation invite.

No single headline viral trigger has yet been proven.

The anti-network-effect strategy is currently a bundle:

- useful standalone capability;
- easy invites;
- exceptional UX;
- privacy;
- interaction-specific onboarding;
- messenger + meeting convergence;
- direct file transfer;
- future interoperability/federation where feasible.

Acquisition funnel to measure:

1. invite → install;
2. install → successful first interaction;
3. first interaction → second interaction;
4. retained contact pair/group;
5. high-value conversations migrating into App1.

---

## 16. Android-first MVP revision

The earlier desktop-first v0.1 assumption is superseded.

The **first MVP is Android-first**.

However, "Android-first" does **not** mean "throwaway calling prototype".

Later discovery expanded the Android product intent into a polished consumer communications experience with:

- text;
- voice/video;
- screen sharing;
- files;
- direct-first/fallback behavior;
- polished UX;
- account-based abuse controls;
- closed Play testing plus GitHub/F-Droid distribution where viable.

The full Universal Core vision is broad, but implementation sequencing remains unresolved.

No Android framework/toolkit or other stack choice has been approved.

---

## 17. Distribution direction

For initial Android real-user distribution, current direction includes:

- closed Google Play beta;
- GitHub distribution;
- F-Droid where feasible.

This means architecture must not later assume a Play-only modular-delivery mechanism without evaluating GitHub/F-Droid equivalents.

---

## 18. Commercial model direction

Initial wedge:

- free individual product.

Intended flywheel:

`individual adoption → professional use → organizational adoption → self-hosted / managed / BYOC`

Managed organizational pricing may eventually combine:

- capacity tiers;
- per-seat software licensing + fixed infrastructure;
- custom enterprise contracts.

Exact pricing is not yet finalized.

Minimum serious market signal before large build-out remains:

- at least one paid pilot.

Discovery exit requires:

- technical proof;
- at least one concrete commercial commitment.

Positive interviews alone are insufficient.

---

## 19. Kill / rethink conditions

Any of these may justify fundamental rethink rather than rationalization:

- direct P2P succeeds too rarely;
- relay cost erases the economic advantage;
- organizations do not value infrastructure control enough to adopt/pay;
- self-hosting requires too much specialist operational effort.

Positioning itself is evidence-led. If sovereignty is not the strongest market wedge, App1 may reposition around privacy, performance, cost, collaboration experience, business self-hosting, or another validated advantage.

---

## 20. Explicit strategic non-goals

App1 should resist becoming:

- full productivity suite;
- giant centralized media cloud;
- giant centralized data silo;
- full Teams/Zoom parity project;
- social network;
- ad/engagement platform;
- full email client/provider;
- full office suite;
- full project-management system;
- full professional whiteboard;
- full calendar replacement;
- full streaming platform;
- gaming launcher;
- wallet/payment network;
- mandatory AI platform;
- vendor-hosted AI for every interaction;
- massive bolt-on catalog with no coherent UX.

Integration should be preferred over duplication where the authoritative system already solves the underlying workload well.

---

## 21. Research reference universe

### Communication

- WhatsApp
- Signal
- Telegram
- Discord

### Meetings/calls

- Zoom
- Teams
- Google Meet

### Work communication

- Slack

### Knowledge/workspaces

- Notion
- Coda
- Craft and adjacent products

### Multiplayer/collaboration

- Figma
- FigJam
- Miro

### Productivity UX

- Linear
- Superhuman
- Raycast

### Async/meeting context

- Loom
- Granola

### Agentic work

- Linear agents/Loops
- Miro Sidekicks/Flows
- Slack AI/workflows
- Notion agents
- adjacent agentic collaboration products

### Sovereignty/federation

- Matrix/Element
- Nextcloud Talk
- Jitsi
- SimpleX

### Realtime infrastructure / SDK platforms

- GetStream.io
- LiveKit
- Daily
- Agora
- Twilio
- Sendbird
- 100ms
- Vonage

This list is a research universe, not a commitment to reproduce every feature.

---

## 22. Research findings retained

Current research has produced several strategic observations:

1. Messaging, calls, E2EE, screen sharing, and group communication are already table stakes across major incumbents.
2. Feature parity alone is not a switching reason.
3. Network effects are likely a major acquisition barrier.
4. Consumer sovereignty must be felt as a benefit, not explained as infrastructure jargon.
5. Direct file transfer is strategically interesting because it can improve user value while avoiding central storage/egress cost.
6. Persistent workspace can be persistent context rather than persistent App1-owned bytes.
7. Enterprise integration is increasingly feasible through APIs, delegated permissions, MCP, and source-owned objects.
8. Interoperability varies widely by platform; universal federation is unrealistic.
9. Managed realtime SDK platforms illustrate the usage-linked cost model App1 wants to avoid depending on structurally.
10. AI, transcription, recording, indexing, persistence, relay, and moderation can become hidden recurring COGS and need explicit economic treatment.
11. Modularity is technically plausible, but excessive module/plugin count would create its own complexity.
12. Best-in-class experience requires disciplined rejection as much as feature harvesting.

---

## 23. Superseded decisions / historical corrections

### Superseded: desktop-first first release

Earlier discovery treated Windows/macOS/Linux + business deployment as the first release boundary.

This was superseded by the founder decision that the first MVP is **Android-first**.

The broader desktop/business vision remains long-term product scope, not first-MVP release scope.

### Superseded: narrow Android calling prototype

A later capability harvest established that Android-first should still aim at a polished broad Universal Core experience rather than remain only a minimal 1:1 call demo.

Implementation sequencing is still open, so this does not mean every Universal Core feature must ship in the first technical build.

### Clarification: concept architecture is hypothesis, not approval

MoQ, QUIC, specific relay models, MLS, storage mechanisms, cloud providers, SDK providers, and other technical proposals from the original concept remain architecture hypotheses until researched and accepted later through the lifecycle/ADR process.

---

## 24. Repository lifecycle mismatch that must not be forgotten

The durable discovery work in Issue #1 is far ahead of the committed lifecycle/doc state on `main`.

At the time this register was created:

- `config/project.env` still says `PROJECT_PHASE=factory`;
- project name/slug are still empty in that committed file;
- `ALLOW_APP_STACK=0`;
- `STACK_DECISION_ADR=`;
- `docs/PRODUCT.md` still says the product is intentionally undefined.

This document does **not** silently fix that lifecycle mismatch.

The proper follow-up is a reviewed transition/update that brings project identity, lifecycle, and `docs/PRODUCT.md` into alignment with accepted discovery when the founder decides discovery is mature enough.

Until then:

- architecture is not authorized;
- application stack is not authorized;
- implementation is not authorized.

---

## 25. Remaining open discovery areas

### 25.1 Hybrid / Professional Workspace

Not yet defined. Next major capability harvest should cover:

- developers;
- startups;
- freelancers;
- agencies;
- small teams/businesses;
- researchers;
- open-source teams;
- GitHub/GitLab;
- Linear/Jira;
- Slack;
- Notion;
- Figma/Miro;
- calendars;
- work objects;
- automation;
- agents;
- richer integrations;
- remote control;
- customer storage;
- professional workflow continuity.

### 25.2 Enterprise

Still needs detailed definition for:

- identity;
- SSO/SCIM;
- policy;
- compliance;
- audit;
- retention;
- data residency;
- self-hosting;
- dedicated managed;
- BYOC;
- customer AI/models;
- enterprise integrations;
- federation;
- multi-region/HA;
- admin UX.

### 25.3 Capability fabric

Still needs detailed product decisions around:

- AI/models;
- storage;
- integration permissions;
- MCP/API/webhooks;
- automation;
- agents;
- source-owned search;
- customer-run workloads;
- App1-managed paid workloads;
- interoperability limits.

### 25.4 Consumer positioning

Still unresolved.

We need a user-facing reason powerful enough to entice people away from or alongside WhatsApp/Signal/Teams/Zoom without relying on technical infrastructure language.

### 25.5 Validation plan

Still needs concrete execution plans for:

- representative network matrix;
- direct-connect benchmarking;
- perceptual call quality;
- failover/recovery;
- relay cost model;
- self-host operator test;
- invite/install/retention funnel;
- paid pilot acquisition;
- abuse model;
- release-readiness rubric.

---

## 26. Decision rule for future discovery

Before adding any major capability, answer all of the following:

1. What user job does it solve?
2. Which product layer actually needs it?
3. What existing product does this best today?
4. What should App1 harvest from that experience?
5. Does App1 truly need to own it?
6. Can it remain a live external object instead?
7. Who owns the source data?
8. Whose permissions remain authoritative?
9. What bytes must App1 store?
10. What traffic must App1 carry?
11. What compute must App1 execute?
12. Does it require paid AI/transcription/moderation?
13. Can it be P2P/local?
14. Can it be user/customer-funded?
15. Can it be BYOC/customer-run?
16. Does it increase base app size?
17. Does it increase attack surface or permissions?
18. What happens when an external API/provider changes?
19. Is the UX materially better because this exists?
20. Final verdict: CORE-NATIVE / MODULE-NATIVE / LIVE-INTEGRATED / CUSTOMER-RUN / PAID-MANAGED / DEFER-REJECT.

---

## 27. Current north star

The clearest current north-star statement is:

> **App1 is a sovereign collaboration fabric delivered through one seamless application. It connects people, conversations, workspaces, and external systems while allowing data, infrastructure, storage, and intelligence to remain where their owners choose.**

And the practical product discipline beneath it is:

> **Best-in-class experience without best-in-class bloat. Own the collaboration experience. Integrate the rest when that is better. Keep vendor marginal cost structurally low.**

---

## 28. Next step

Continue discovery with the **Hybrid / Professional Workspace capability harvest**, then Enterprise, then the cross-cutting Capability Fabric.

Do not move to architecture until the product definition and validation requirements are sufficiently complete and accepted through the reviewed lifecycle.
