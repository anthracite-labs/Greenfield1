# Roadmap

Lifecycle sequencing and current discovery progress for App1.

The stages below map to `PROJECT_PHASE` in [`../config/project.env`](../config/project.env). The current committed phase is **discovery**. This document does not authorize architecture or implementation.

```text
factory  →  discovery  →  architecture  →  implementation
   │            │              │                 │
 template   product being   product definition  stack recorded in an ADR;
 itself     discovered       accepted enough     application code allowed
                             to choose stack     (ALLOW_APP_STACK=1)
```

---

## Stage: factory (`PROJECT_PHASE=factory`)

Only the reusable App-Factory template itself sits here. Foundation work includes rules, workflows, verification, negative tests, CI, provenance, and factory documentation.

Greenfield1 has already left this phase and is an instantiated App1 repository.

---

## Stage: discovery (`PROJECT_PHASE=discovery`) — **CURRENT**

Purpose: define App1 precisely enough to support evidence-led validation and, only when discovery is mature enough, a later architecture phase.

The no-stack guard remains active: `ALLOW_APP_STACK=0`, with no accepted application-stack ADR.

### Durable discovery state

- [x] Project identity is committed as App1 in `config/project.env`.
- [x] Product-discovery discussion/provenance is active in GitHub Issue #1.
- [x] Canonical working product discovery is maintained in [PRODUCT.md](PRODUCT.md).
- [x] Provisional product-domain vocabulary is maintained in [DOMAIN.md](DOMAIN.md).
- [x] Universal Core contract has founder-approved discovery direction.
- [x] Community / Personal Workspace contract has founder-approved discovery direction.
- [ ] Hybrid / Professional Workspace contract is defined.
- [ ] Corporate / Enterprise contract is defined.
- [ ] Cross-cutting Capability Fabric is defined.
- [ ] Consumer headline positioning is strong enough to test.
- [ ] Concrete validation programme and release-readiness rubric are defined.
- [ ] Representative technical proof is obtained.
- [ ] At least one paid pilot or other concrete commercial commitment is obtained.

### Next discovery sequence

1. Hybrid / Professional Workspace capability harvest.
2. Corporate / Enterprise capability harvest.
3. Cross-cutting Capability Fabric decisions.
4. Consumer positioning research/invention.
5. Validation programme: network matrix, direct-connect distribution, call quality/recovery, relay economics, self-host operator test, acquisition funnel, abuse model, and release-readiness gates.

### Discovery exit conditions

Discovery does **not** exit merely because a broad vision exists.

Before proposing `PROJECT_PHASE=architecture`:

- [PRODUCT.md](PRODUCT.md) must contain a reviewed product definition sufficiently complete for architecture to serve rather than invent;
- unresolved product-layer boundaries must be reduced to explicitly accepted deferrals rather than hidden gaps;
- product/security/domain constraints needed by architecture must be recorded in canonical docs;
- technical proof must support the load-bearing realtime/economic assumptions;
- at least one concrete commercial commitment is required; positive interviews alone are insufficient;
- the founder must explicitly accept the discovery exit.

Until then, remain in discovery and do not select an application stack.

---

## Stage: architecture (`PROJECT_PHASE=architecture`) — **NOT AUTHORIZED YET**

Only after discovery exits:

- open an architecture issue proposing implementation approaches;
- research real alternatives;
- record durable choices as ADRs under [decisions/](decisions/README.md);
- choose the application stack through an accepted application-stack ADR;
- define stack-specific testing/build/lint gates.

The no-stack guard remains active during architecture until the required accepted stack ADR exists. It is not disabled to "try something out".

Exit condition: accepted application-stack ADR plus the reviewed lifecycle transition required by `config/project.env`.

---

## Stage: implementation (`PROJECT_PHASE=implementation`) — **NOT AUTHORIZED**

Implementation may begin only after the stack ADR is accepted and a reviewed lifecycle transition sets all of the following consistently:

- `PROJECT_PHASE=implementation`;
- `ALLOW_APP_STACK=1`;
- `STACK_DECISION_ADR=docs/decisions/NNNN-<title>.md`.

`scripts/verify.sh` independently checks lifecycle and no-stack consistency. Stack-specific lint/test/build jobs are added alongside the foundation gate; the foundation gate is never replaced.

---

## Cross-stage rules

- Product discovery does not imply architecture approval.
- Product terms such as direct, relay, E2EE, BYOC, integration, federation, identity, workspace, or module do not select implementation mechanisms.
- Durable technical trade-offs belong in ADRs only when the relevant lifecycle stage is reached.
- `docs/MEMORY.md` remains append-only session memory, not the canonical product specification.
- GitHub Issue #1 preserves discovery discussion/provenance; [PRODUCT.md](PRODUCT.md) and [DOMAIN.md](DOMAIN.md) carry current canonical discovery state.
