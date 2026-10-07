# Roadmap — Main Track (Phases 0–8, then merge)

Dependency order, not excitement order. Each phase should produce something
usable before moving up. The compute-fabric workspace runs as a parallel
track and only becomes a dependency at Phase 9.

```text
Phase 0   Club + institutional partnership
Phase 1   Platform kernel (gateway, identity, API contract)
Phase 2   AI MVP (independent PSDC Web + OpenCode + one local model)
Phase 3   Production foundation (HA, PostgreSQL/Valkey, policy, telemetry)
Phase 4   Academic platform (Brightspace, read-only)
Phase 5   Personal Student Agent (tasks, calendar, reminders, planning)
Phase 6   PSDC OpenWork Desktop (OpenWork MIT core + AC Session Host)
Phase 7   PSDC Happy Mobile (Happy + self-hosted E2EE Session Relay)
Phase 8   Action Gateway (registration, booking, clubs, forms)
Phase 9   ← MERGE POINT: psdc-compute becomes a routable backend
Phase 10  Campus Graph (unified institutional knowledge graph)
Phase 11  Department/club specialist agents
Phase 12  SDK + student developer platform
Phase 13  Agent/app marketplace, federation, volunteer compute
```

## Phase details (0–3)

**Phase 0 — Club + partnership.** Get SA recognition, a faculty advisor, and
early relationships with ITS / Learning & Teaching Services / Applied
Research. You don't need ITS sign-off to write code and experiment on
hardware you're already authorized to use — you do need it before touching
Entra, Brightspace, College servers, or College lab PCs.

**Phase 1 — Platform kernel.** Minimum services: `gateway`, `identity`,
`model-registry`, `model-router`, `policy`, `usage`, `telemetry`. API contract
locked early:
```text
/v1/models  /v1/responses  /v1/chat/completions  /v1/embeddings
/ac/v1/me   /ac/v1/usage   /ac/v1/projects        /ac/v1/tools
```
Milestone: login → gateway → local model → "hello". If that's reliable, the
nucleus of the whole platform exists.

**Phase 2 — AI MVP.** Independent `psdc-web` + OpenCode + one local inference engine.
The web client starts from the verified Open WebUI v0.6.5 BSD source only after
ADR-0009's provenance, legal, security, accessibility, and maintenance gates pass.
Use a handful of aliases (`AC Fast`, `AC General`, `AC Code`, `AC Reasoning`), not
thirty models. Current Open WebUI releases remain compatibility clients only.

**Phase 3 — Production foundation.** PostgreSQL, Valkey, object storage, vector
storage, backups, secrets management, audit logs, metrics, tracing, rate
limits, quotas, model health, failover. This is when `CAMPUS_ONLY` /
`SELF_HOSTED` / `USER_EDGE_ALLOWED` routing actually gets implemented, and
when you should be able to kill any single instance of anything without
taking the service down.

## Phases 4–8 (build after 0–3 are solid)

Academic AI (read-only Brightspace via OAuth 2.0 / LTI Advantage, no write
access yet) → Student Agent (deterministic task/notification service behind
the LLM, not the LLM remembering timers itself) → OpenWork-derived desktop app
(calls the same APIs web already uses; adds local workspace, terminal, tools and
the Session Host) → Happy-derived mobile (adds E2EE pairing, continuity, opaque
notifications, approval and handoff through the Session Relay) → Action Gateway (low-consequence
actions first: reminders, free-event registration, room booking; anything
touching enrollment or payment gets a separate, stricter workflow with an
explicit PLAN → PREVIEW → CONFIRM → EXECUTE → VERIFY → RECEIPT flow).

## The rule

> Platform capability → API → permissions → then every client (web, desktop,
> mobile, OpenCode, third-party apps) consumes it. Never build a feature
> directly into one client first and "figure out the backend later."
