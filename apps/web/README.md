# Web Client Migration Notice

The independent browser client is owned by `psdc-web`. This directory contains no
web source and SHALL NOT receive new browser-client implementation.

`psdc-ai` owns the AI gateway, routing, policy integration, inference adapters,
evaluation and service contracts consumed by clients. It does not own the web
product lifecycle.

Canonical references:

- `Post-Secondary-Digital-Commons/psdc-web`
- [ADR-0025: Independent Web Client Repository](../../../psdc-architecture/docs/architecture/architecture-decision-records/ADR-0025-independent-web-client-repository.md)
- [Web Client Architecture](../../../psdc-web/docs/architecture/Web-Client-Architecture.md)
