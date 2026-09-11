# Archived Provenance Worksheet — Moved to PSDC Web

The authoritative import policy is
`psdc-web:docs/upstream/Open-WebUI-Provenance-Policy.md`.

No Open WebUI source was imported into `psdc-ai`. This path is retained as a
migration pointer and MUST NOT contain web-client source or authorize an import.

ADR-0025 moved browser-client ownership to the independent `psdc-web` repository.
Any future upstream evaluation, immutable source reference, license record, file
inventory, checksum, SBOM, security review, accessibility review, and maintenance
decision belongs in the pull request that proposes an import into that repository.
