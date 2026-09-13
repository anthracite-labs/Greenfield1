# Product Discovery — App1

**Status:** discovery in progress  
**Lifecycle:** `PROJECT_PHASE=discovery`  
**Architecture/stack authorization:** none  
**Discovery discussion/provenance:** GitHub Issue #1

This file is the canonical product-discovery document for App1. It records founder-approved working decisions, explicit supersessions, product constraints, research findings, open hypotheses, validation requirements, and remaining discovery questions.

It is **not** a final product definition, architecture ADR, stack decision, or implementation authorization. Discovery remains open until the remaining product and validation questions are sufficiently resolved and accepted through the reviewed lifecycle.

---

## 1. Current working definition

App1 is a **sovereign collaboration fabric delivered through one seamless application**.

It combines a lightweight universal communications core with progressively richer workspaces and organization capabilities, while allowing users and organizations to keep their existing data, infrastructure, storage, tools, and intelligence where appropriate.

The key product principle is:

> **App1 owns the collaboration experience and context — not necessarily every workload, dataset, model, file, or external system underneath it.**

The infrastructure/economic principle remains:

> **Direct when possible. Dedicated when necessary. Yours when you want it.**

App1 is therefore not merely a WhatsApp, Signal, Zoom, Teams, Discord, Slack, Notion, IDE, AI-agent-platform, productivity-suite, social-network, or centralized-media-cloud clone. It is intended to be the collaboration layer that makes communication, workspaces, and external systems feel coherent without requiring App1 to rebuild or own all of them.

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

- students and study groups;
- gamers;
- clubs and hobby groups;
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
- freelancers and consultants;
- startups;
- agencies;
- researchers;
- open-source teams;
- small businesses and professional teams.

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

**Status:** not yet fully defined. This is the next major capability harvest.

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

**Status:** not yet fully defined.

### 2.5 Cross-cutting Capability Fabric

Capabilities that may span layers include:

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

Current product principle:

> **One experience. Progressive capabilities. Context-specific complexity. Modular delivery.**

Installed capability must not equal total platform capability. The base application should remain lightweight enough for the global average user. Richer capability can be delivered through coarse optional modules/capability packs such as Community, Hybrid/Professional, Enterprise, heavyweight collaboration capabilities, selected integrations, and specialized tools.

Avoid hundreds of microscopic plugins. Modularization should reduce app size, attack surface, permissions, startup cost, and cognitive load rather than becoming another complexity source.

The following states must remain conceptually distinct for later product/architecture work:

- capability available;
- capability installed;
- capability permitted;
- capability licensed.

---

## 4. Capability ownership classification

Every future major capability must receive an explicit ownership verdict before acceptance.

- **CORE-NATIVE** — App1 must own it because it defines the product experience.
- **MODULE-NATIVE** — App1 owns it, but it should be optional/downloadable/activated only where needed.
- **LIVE-INTEGRATED** — the external system remains authoritative; App1 provides native-feeling context, preview, search, and/or actions without unnecessarily copying or replacing the source system.
- **CUSTOMER-RUN** — the capability executes on customer infrastructure, storage, cloud, or models.
- **PAID-MANAGED** — App1 hosts the workload because customer revenue explicitly covers the associated marginal cost.
- **DEFER / REJECT** — the capability does not justify its product complexity, operational burden, app weight, security surface, or recurring cost.

---

## 5. Universal Core contract

### 5.1 Interaction model

Universal Core uses **one seamless conversation model**. Text, voice, video, files, media, screen sharing, and calls are capabilities of the same relationship/context rather than separate products.

The experience should remain **WhatsApp-simple** even when deeper capability exists.

### 5.2 Communication surface

Founder-approved Core direction includes:

- text messaging;
- voice calls;
- video calls;
- small-group chat and calls;
- screen sharing;
- direct-first file transfer;
- media sharing;
- voice and video messages;
- conversation history/context;
- message replies and reactions;
- privacy controls;
- search;
- multi-device continuity;
- notifications;
- optional lightweight integrations.

Calls remain part of conversation context/history without flooding the message timeline with noisy call metadata.

Core starts with **small groups**, not server/community-scale structures. Community structure belongs to the Community capability layer.

Voice and video messages are first-class communication objects; they must not turn into Stories/Reels/social-feed behavior.

Photos/video should optimize sharing sensibly by default while preserving an original-quality option. Avoid artificial quality degradation where the transport/cost model does not require it.

### 5.3 Direct file transfer

Direct file transfer is a core differentiator.

Desired behavior:

- direct-first where practical;
- resumable;
- no arbitrary App1 size cap when a transfer is truly direct and device/network limits permit it;
- optional persistence only when needed;
- configured cloud/BYOC may be used for persistence;
- when the recipient is offline, queue where practical and optionally offer temporary or configured persistent storage.

The product should exploit cases where a better user experience is also cheaper for App1.

### 5.4 Screen sharing and remote control

Screen sharing belongs in Core and should be available from an active conversation and easy to escalate from a call.

Remote control is **not** a default Core capability. Current direction:

- first belongs in Hybrid/Enterprise;
- may later become a paid consumer capability;
- always requires explicit consent and strong safety controls.

### 5.5 Identity and discovery

Target identity direction:

- internal App1 identity;
- optional external identifiers;
- long-term vendor-neutral identity direction.

Phone number should **not be mandatory**. Phone-number recovery/discovery trade-offs still require research.

Contact discovery is privacy-first by default:

- exact username;
- QR;
- invite links;
- potentially opt-in private contact discovery later;
- no mandatory address-book upload.

Presence should expose minimal information by default and be user-controlled. Read receipts and typing indicators should be privacy configurable.

### 5.6 Message policy, search, multi-device, backup

Consumer Core should support visible editing state. Enterprise contexts may require richer edit history/policy later. Deletion and disappearing-message behavior should be policy/context aware rather than hard-coded globally.

Search direction:

- device/local search by default where practical;
- optional remote/BYOC index;
- source-specific search for integrations;
- do not assume App1 must centrally index all user/company content.

Multi-device continuity is essential. The security model must preserve appropriate encryption and offline continuity.

Backup direction:

- local/export;
- user-selected cloud/BYOC;
- App1-managed backup only as an optional paid service where justified.

### 5.7 Notifications and call UX

Notifications should combine smart bundling, privacy-aware previews, context-aware priority, and user-controlled quiet modes.

Call UX is minimal by default, with advanced controls appearing progressively based on context/device/user need.

Connection-path status should be subtle in normal UX with detailed diagnostics on demand. Ordinary users should not have to choose P2P vs relay manually.

### 5.8 AI and consumer integrations

**No built-in AI in Universal Core.** AI belongs to an optional future capability layer, not the product's mandatory brain.

Lightweight integrations are allowed if they stay optional and do not bloat Core. Examples worth studying include Gmail/Calendar, Google Drive, Dropbox, and OneDrive.

Constraints:

- Gmail integration must not turn App1 into an email client;
- Drive-style integration should prefer references/live objects rather than copying files into App1;
- external systems should remain authoritative where possible.

### 5.9 Core non-goals

Core rejects:

- advertising;
- algorithmic engagement feeds;
- Stories/social-feed direction;
- wallet/payments/commerce as a core product category;
- mandatory App1 cloud storage;
- mandatory AI;
- mini-app clutter;
- unnecessary enterprise complexity.

### 5.10 Core economics and success

> **Free where App1 marginal cost is negligible; charge where App1 incurs genuine recurring cost; preserve customer-run/BYOC alternatives wherever practical.**

Core succeeds when users willingly move valuable conversations into App1, repeatedly invite others, retain those conversation pairs/groups, use App1 for ordinary communication rather than one-off novelty, and the economics remain sustainable.

Consumer headline positioning remains unresolved and needs further invention/research.

---

## 6. Community / Personal Workspace contract

### 6.1 Product identity and structure

A Community Workspace is a **persistent shared project/interest space containing people, conversation, voice/video, files, and shared context**.

Any group should be able to evolve naturally into one without a hard migration step.

UX rule:

> **Start simple. Expose structure only when the group actually needs it.**

Channels are acceptable, but they must not force Discord/Slack-style configuration complexity onto every group. Preferred direction is a main conversation with channels/topics/threads where useful and adaptive structure as groups grow.

### 6.2 Voice/video and events

Desired behavior includes instant contextual voice spaces, small/group video, screen sharing, presentation/watch-style modes where useful, and optional scheduling for events. Live collaboration should not feel like creating a formal meeting every time.

Community can support basic events plus calendar integrations; do not build a full calendar replacement.

### 6.3 Files, notes/docs, tasks

Do **not** make App1 the mandatory host of workspace files.

Preferred file model:

- direct transfer;
- persistent references;
- external cloud objects;
- optional user/customer storage;
- App1-hosted persistence only where deliberately chosen/paid.

Do not build a full office suite. Lightweight native notes may be useful; live external documents such as Docs/Notion should remain authoritative where appropriate.

Community may include simple shared checklists. Richer project/task management belongs in Hybrid or integrations.

### 6.4 Roles, moderation, discoverability, guests

Use simple role defaults first; advanced roles appear only when the group needs them.

Strong manual/moderator controls come first. Automated moderation may be an optional later capability, especially if it creates inference/COGS costs.

Discoverability is privacy-first and invite-first by default. Public discoverability may become optional later, but giant public communities are not the Community design center.

External/temporary guests may be allowed through invite/link flows with strong abuse controls.

### 6.5 Bots, activities, gaming, study, creators

Safe bot/integration hooks are desirable, but normal UX must remain clean. Selected collaborative activities can exist where they materially improve the shared experience; do not blindly recreate a giant Discord-style app/activity marketplace.

Gaming can become an optional capability pack using capabilities such as rich presence, voice, screen share, and activity/game status. Do not turn App1 into a gaming launcher.

Student/community scenarios may combine group chat, voice/video, files, screen sharing, notes, events, study rooms, and external Drive/Docs/LMS integrations.

Broadcast/community capability may be investigated later as an optional creator/community pack; it is not the universal Community baseline.

### 6.6 Whiteboards, polls, knowledge

Do not build a full professional whiteboard product by default. Lightweight native sketching may be useful; integrate Miro/FigJam-class professional boards.

Basic polls are useful. Do not expand this into a full forms/survey product unless evidence later justifies it.

There is no native full-wiki requirement. Persistent pinned/shared context may exist, but professional knowledge systems should generally remain external/integrated.

### 6.7 Search, notifications, identity, federation, AI

Workspace search should eventually span messages, files/references, workspace context, and connected external objects. It must respect source permissions and should avoid expensive centralized indexing by default.

Use per-space notification controls plus context-aware prioritization. Presence may become richer inside workspaces but remains privacy controlled.

Use a core identity with workspace-specific profile/presentation where useful.

Keep the product/data model compatible with future federation, but federation is not a Community MVP requirement.

Community AI is optional later and not required in the Community baseline.

### 6.8 Community monetization, delivery, non-goals

No ads. Monetization should come from real value or real cost surfaces such as storage, relay/capacity, premium modules, and paid managed capabilities.

Community should be an optional capability pack that can be dynamically enabled when a user creates or joins a workspace.

Economic rule:

- P2P/direct where possible;
- user/customer cloud for persistence where appropriate;
- paid App1 persistence only when deliberately chosen.

Unless future evidence materially changes the decision, Community should not build native replacements for full office/docs suites, full project-management suites, full professional whiteboards, full calendar products, or full streaming platforms. It must explicitly avoid becoming a Discord clone, social network, creator monetization platform, productivity-suite monster, or gaming launcher.

Community succeeds when groups choose App1 instead of juggling multiple disconnected tools such as messaging + voice + files + meeting apps, while App1 stays simple and economically sustainable.

---

## 7. Sovereignty, persistence, integration and interoperability

### 7.1 Infrastructure and sovereignty thesis

Long-term product direction includes:

- peer-to-peer/direct-first individual communication;
- bounded relay fallback;
- self-hosted organizational deployments;
- dedicated managed organizational deployments;
- enterprise BYOC;
- customer-owned storage and models where appropriate;
- federation as a long-term differentiator.

Organizations should ultimately be able to control as much as practical of identity, policy, media infrastructure, storage, encryption, and geographic/data placement.

The vendor control plane should remain lightweight relative to media/data workloads where possible.

Specific transports, protocols, frameworks, hosting providers, databases, auth providers, and implementation mechanisms remain **unapproved architecture questions**.

### 7.2 Persistent workspace / BYOC principle

A persistent App1 workspace should not imply that all workspace bytes live in App1. A workspace can instead be a persistent graph of people, conversations, live sessions, shared context, decisions, references, external objects, and allowed actions.

Example external objects include SharePoint/OneDrive files, Google Drive files, GitHub PRs/issues, Jira/Linear tasks, Figma/Miro artifacts, S3/object-storage data, internal enterprise systems, and customer AI/model endpoints.

> **No migration required where live integration can preserve source ownership, permissions, and data residency.**

### 7.3 Interoperability ladder and source authority

Integration is layered, not universal. Use the following interoperability ladder:

1. link;
2. preview;
3. live object;
4. read connector;
5. action connector;
6. cross-organization collaboration;
7. protocol federation.

Different external systems may stop at different levels.

> **The source system remains authoritative for its own data and permissions.**

App1 should not create a shadow ACL universe that accidentally grants access to content a user could not access at the source.

Integration methods to investigate include native APIs, OAuth/OIDC delegated authorization, webhooks/events, MCP, open protocols, private/custom connectors, and federation standards where appropriate. MCP is worth serious research but must not be the only integration mechanism.

Research direction is bidirectional: App1 consumes external systems, and external tools/agents may eventually consume permitted App1 context/actions. No specific API/protocol decision is approved yet.

---

## 8. AI/model direction

AI is **not** the defining App1 proposition and is explicitly excluded from Universal Core baseline.

Long-term directions to research:

- no AI;
- on-device/local model;
- customer-hosted model;
- customer Azure/OpenAI/Bedrock/etc.;
- enterprise model gateway;
- App1-managed paid AI.

> **Do not make every App1 interaction create a vendor AI inference bill.**

For enterprises, BYO-model/customer-approved AI should be a first-class research path so organizations do not have to migrate or expose proprietary models and knowledge to App1-managed infrastructure.

---

## 9. Economic model, reliability and operations requirements

Near-zero/very-low vendor marginal cost remains a core product constraint, not merely a backend optimization. It applies to media, files, storage, indexing, AI inference, transcription, recording, sync, moderation, integrations, backups, and managed infrastructure.

Preferred cost order where user experience and reliability allow:

1. direct/local;
2. customer-owned/customer-funded;
3. BYOC;
4. fixed/predictable dedicated infrastructure;
5. bounded App1-managed fallback;
6. externally metered services only when strategically justified.

Treat unlimited relay, centralized media, vendor-hosted persistent storage, broad centralized indexing, recording/transcoding, transcription, AI inference, PSTN/SMS/phone verification, continuous high-frequency synchronization, and large-scale automated moderation as explicitly cost-bearing until proven otherwise.

First-class operating metrics retained:

1. direct-connect rate;
2. relay bytes per free user-hour;
3. concurrent participants per relay dollar;
4. operator minutes per customer per month.

Do not invent arbitrary thresholds before representative testing. Benchmark direct-connect distributions, relay cost/free-user-hour, mainstream call setup/reliability, and use call completion + recovery + perceptual quality as reliability dimensions.

Desired degraded-network behavior:

- preserve audio;
- preserve low-resolution video where practical;
- prioritize smooth continuity;
- around 2% packet loss should remain usable as an initial target;
- final acceptance is perceptual/recovery based, not raw packet-loss based.

Reliability target is **mainstream conferencing-class**, not experimental best effort. Direct→relay failover may have a brief interruption if recovery is reliable and understandable.

Self-hosting remains first-class long term. Target operator is a competent IT administrator, not a realtime-media specialist or dedicated SRE team. Installation time is less important than eliminating specialist knowledge; routine operator effort should approach zero.

Preferred upgrade experience includes preflight compatibility/health checks, release/impact summary, automatic vs controlled policy, admin approval where required, maintenance scheduling, staged/canary rollout where possible, post-upgrade health verification, safe rollback, and enterprise deferral within supported security windows. These are product requirements, not implementation decisions.

---

## 10. Acquisition, MVP, distribution and commercial direction

App1 should not demand that users "move their network" before receiving value.

Current acquisition direction:

- use existing apps/services as distribution rails;
- invite to a concrete interaction rather than to "another messenger";
- preserve invite context through install/account creation where possible;
- resume the intended interaction after onboarding;
- earn primary-app status through repeated superior experiences.

Potential interaction triggers include large direct file transfer, private/direct call, screen-share/collaboration invitation, and conversation invite. No single headline viral trigger has yet been proven.

Acquisition funnel to measure:

1. invite → install;
2. install → successful first interaction;
3. first interaction → second interaction;
4. retained contact pair/group;
5. high-value conversations migrating into App1.

### 10.1 Android-first MVP supersession

The earlier desktop-first v0.1 assumption is superseded. The **first MVP is Android-first**.

Android-first does **not** mean a throwaway calling prototype. Later discovery expanded the Android product intent into a polished consumer communications experience with text, voice/video, screen sharing, files, direct-first/fallback behavior, polished UX, and account-based abuse controls.

The full Universal Core vision is broad, but implementation sequencing remains unresolved. No Android framework/toolkit or other stack choice has been approved.

### 10.2 Distribution direction

For initial Android real-user distribution, current direction includes:

- closed Google Play beta;
- GitHub distribution;
- F-Droid where feasible.

Later architecture must not assume a Play-only modular-delivery mechanism without evaluating GitHub/F-Droid equivalents.

### 10.3 Commercial direction

Initial wedge: **free individual product**.

Intended flywheel:

`individual adoption → professional use → organizational adoption → self-hosted / managed / BYOC`

Managed organizational pricing may eventually combine capacity tiers, per-seat software licensing + fixed infrastructure, and custom enterprise contracts. Exact pricing is not finalized.

Minimum serious market signal before large build-out remains **at least one paid pilot**.

Discovery exit requires technical proof plus at least one concrete commercial commitment. Positive interviews alone are insufficient.

---

## 11. Kill / rethink conditions

Any of these may justify fundamental rethink rather than rationalization:

- direct P2P succeeds too rarely;
- relay cost erases the economic advantage;
- organizations do not value infrastructure control enough to adopt/pay;
- self-hosting requires too much specialist operational effort.

Positioning is evidence-led. If sovereignty is not the strongest market wedge, App1 may reposition around privacy, performance, cost, collaboration experience, business self-hosting, or another validated advantage.

---

## 12. Explicit strategic non-goals

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

## 13. Discovery research register

### 13.1 Research reference universe

Communication: WhatsApp, Signal, Telegram, Discord.  
Meetings/calls: Zoom, Teams, Google Meet.  
Work communication: Slack.  
Knowledge/workspaces: Notion, Coda, Craft and adjacent products.  
Multiplayer/collaboration: Figma, FigJam, Miro.  
Productivity UX: Linear, Superhuman, Raycast.  
Async/meeting context: Loom, Granola.  
Agentic work: Linear agents/Loops, Miro Sidekicks/Flows, Slack AI/workflows, Notion agents, adjacent agentic collaboration products.  
Sovereignty/federation: Matrix/Element, Nextcloud Talk, Jitsi, SimpleX.  
Realtime infrastructure/SDK platforms: GetStream.io, LiveKit, Daily, Agora, Twilio, Sendbird, 100ms, Vonage.

This is a research universe, not a commitment to reproduce every feature.

### 13.2 Retained research findings

Current research has produced these strategic observations:

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

Realtime infrastructure providers studied or queued for continued comparison include GetStream.io, LiveKit, Daily, Agora, Twilio, Sendbird, 100ms, Vonage and adjacent providers. Their role is to harvest mature communication primitives, benchmark SDK/developer experience, identify commodity capabilities, calculate build-vs-buy economics, and quantify usage-linked managed infrastructure against App1's direct/customer-funded thesis.

GetStream is a communication capability, SDK/DX and managed-COGS benchmark, not an architecture choice. LiveKit is an important eventual architecture-stage reference because it supports managed and serious self-hosted realtime models, but remains a research/adopt-extend candidate only; no decision has been made.

---

## 14. Superseded decisions / historical corrections

- **Desktop-first first release — superseded.** The first MVP is Android-first. The broader desktop/business vision remains long-term product scope, not first-MVP release scope.
- **Narrow Android calling prototype — superseded.** Android-first should aim at a polished broad Universal Core experience rather than remain only a minimal 1:1 call demo. Implementation sequencing remains open; this does not mean every Core capability must ship in the first technical build.
- **Concept architecture — hypothesis, not approval.** MoQ, QUIC, specific relay models, MLS, storage mechanisms, cloud providers, SDK providers, and other technical proposals from the original concept remain architecture hypotheses until researched and accepted later through the lifecycle/ADR process.

---

## 15. Remaining open discovery areas

### 15.1 Hybrid / Professional Workspace

Next major capability harvest should cover developers, startups, freelancers, agencies, small teams/businesses, researchers, open-source teams, GitHub/GitLab, Linear/Jira, Slack, Notion, Figma/Miro, calendars, work objects, automation, agents, richer integrations, remote control, customer storage, and professional workflow continuity.

### 15.2 Enterprise

Still needs detailed definition for identity, SSO/SCIM, policy, compliance, audit, retention, data residency, self-hosting, dedicated managed, BYOC, customer AI/models, enterprise integrations, federation, multi-region/HA, and admin UX.

### 15.3 Capability fabric

Still needs detailed product decisions around AI/models, storage, integration permissions, MCP/API/webhooks, automation, agents, source-owned search, customer-run workloads, App1-managed paid workloads, and interoperability limits.

### 15.4 Consumer positioning

Still unresolved. App1 needs a user-facing reason powerful enough to entice people away from or alongside WhatsApp/Signal/Teams/Zoom without relying on technical infrastructure language.

### 15.5 Validation plan

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

## 16. Decision rule for future discovery

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

## 17. Current north star

> **App1 is a sovereign collaboration fabric delivered through one seamless application. It connects people, conversations, workspaces, and external systems while allowing data, infrastructure, storage, and intelligence to remain where their owners choose.**

Practical product discipline:

> **Best-in-class experience without best-in-class bloat. Own the collaboration experience. Integrate the rest when that is better. Keep vendor marginal cost structurally low.**

---

## 18. Discovery status and exit

Discovery is **not complete**.

The next sequence is:

1. Hybrid / Professional Workspace capability harvest;
2. Corporate / Enterprise definition;
3. cross-cutting Capability Fabric definition;
4. consumer positioning work;
5. concrete validation programme and measurable gates.

Do not move to architecture until the product definition and validation requirements are sufficiently complete and accepted through the reviewed lifecycle.

Before discovery exits, the repository must have a reviewed product definition plus the required technical proof and at least one concrete commercial commitment. The no-stack guard remains active throughout discovery.