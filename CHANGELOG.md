# Changelog

## 0.1.1

- Add generic names for the legacy agent-message v1 protocol identifiers while retaining deprecated source-compatible aliases.


## 0.1.0 — 2026-11-12

Initial standalone package release from immutable source snapshot `29c24cfa2b6ead5704d26cf2746bc384f2938b80`.

- Legacy agent-message v1 envelope and bounded decoder.
- Strict constrained JSON/JCS-compatible canonicalization and digest helpers.
- Evidence-resolution and evidence-verification v1 contracts.
- Governance approval request/receipt v1 contracts.
- MCP service gateway request/response v1 contracts.
- Pinned strict-JSON golden vectors, docs, MIT license and CI workflow.

No runtime, transport, database, trust provider, service gateway implementation, or authorization implementation was extracted.
