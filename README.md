# psdc-ai

Commons AI Fabric subsystem of the **Post-Secondary Digital Commons**: identity-aware AI access,
gateway and model routing, client/OpenCode integration, academic capabilities,
agents, SDKs, and inference adapters. Browser, desktop, and mobile clients
release from their own repositories.

**Status:** pre-code scaffold. The architecture, ADRs, and accepted technology
catalog are the current source of truth. Component directories mark ownership
boundaries; exact releases, measurements, service extraction, implementation,
and production approvals remain incomplete.

## Sibling workspace

Distributed campus compute (turning idle lab machines into an opportunistic
inference/compute pool) lives in a **separate** workspace, `psdc-compute`,
not in this one. The two tracks develop in parallel and only integrate at Phase 9
(see `docs/architecture/05-roadmap-phases.md`). Keeping them separate means the
AI product doesn't get blocked by distributed-systems R&D, and the compute work
doesn't inherit the AI platform's security/compliance surface before it's ready to.

The complete tenant-neutral Post-Secondary Digital Commons also includes sibling
repositories for Commons Cloud Fabric, Commons Media and Spatial Fabric, Commons Social Fabric, and the umbrella
cross-platform architecture. Algonquin is the first deployment overlay.
Integrations
use versioned APIs and contracts; Commons AI Fabric never reads a sibling system's private
database or imports its internal code.

## Ecosystem dependencies

Commons AI Fabric depends on Commons Cloud Fabric for identity, authorization context, secrets,
observability, and shared events. Local inference is the minimum viable runtime;
Commons Compute Fabric is an optional capacity provider reached only through the compute contract.
Media and Fediverse capabilities are integrations, not hidden runtime
dependencies. Model providers and hosted AI APIs are optional adapters and cannot
be required for core operation.

- [Consolidated ecosystem architecture](../psdc-architecture/docs/architecture/Consolidated-Ecosystem-Architecture.md)
- [Dependency contract](../psdc-architecture/docs/architecture/Ecosystem-Dependency-Contract.md)
- [Cross-pollination model](../psdc-architecture/docs/architecture/Cross-Pollination-and-Shared-Capabilities.md)
- [Open-source-only policy](../psdc-architecture/docs/vision/11-Open-Source-Only-Policy.md)
- [Full technology stack](../psdc-architecture/docs/vision/14-Full-Technology-Stack-and-Open-Source-Alternatives.md)
- [Commons architecture](../psdc-architecture/docs/vision/constitutional/Post-Secondary-Digital-Commons-Architecture.md)

## How to read this workspace

| Folder | Contents |
|---|---|
| `docs/architecture/` | The technical design: gateway, identity/SSO, model routing, repo layout, phased roadmap |
| `docs/governance/` | The club/org taxonomy, identity & role model, agent action-risk levels |
| `docs/decisions/` | Architecture Decision Records (ADRs) — why things were decided a particular way |

## First vertical slice (target for the earliest working prototype)

1. Commons AI Gateway — the one AI service the clients depend on
2. Basic user authentication (dev-auth is fine before Entra is wired up)
3. One local model behind it
4. OpenAI-compatible API surface (`/v1/chat/completions`, `/v1/models`, etc.)
5. The independent `psdc-web` client, bootstrapped only from a legally and
   technically verified Open WebUI v0.6.5 BSD source baseline and pointed only
   at the gateway
6. A thin OpenCode integration pointed at the same gateway, subject to release
   license review
7. A basic usage/logging dashboard
8. Hardware-census prototype — lives in `psdc-compute`, not here

If steps 1–7 work reliably, the rest of the roadmap is additive, not a rewrite.

The web baseline is frozen: do not copy or merge post-v0.6.5 Open WebUI source or
assets without file-level license review and a new ADR. See
[ADR-0009](../psdc-architecture/docs/architecture/architecture-decision-records/ADR-0009-psdc-ai-web-foundation.md).
