# Protocol Contracts

[![CI](https://github.com/nplongx/protocol-contracts/actions/workflows/ci.yml/badge.svg?branch=main)](https://github.com/nplongx/protocol-contracts/actions/workflows/ci.yml)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)

Typed, versioned wire contracts and deterministic structural validators for service-to-service messages, evidence records, approval receipts, and canonical JSON payloads.

> **Status:** `0.1.0`, initial standalone extraction. Included wire formats are versioned contracts, not a universal protocol standard. Compatibility and API may change before `1.0.0`.

## Included contracts

| Module | Scope |
|---|---|
| `protocol_contracts::` | COS-AP v1 message envelope, strict bounded JSON decoding, typed message kinds, and envelope validation. |
| `agg_checkpoint_v2` | Constrained I-JSON parsing, duplicate-key rejection, JCS-compatible canonicalization, and domain/component digests. |
| `evidence_resolution_v1` | Versioned source-resolution request/response, digest binding, bounded source size, and declared producer-lineage checks. |
| `evidence_verification_v1` | Evidence-verification subject and receipt schema, identity inventory, exact snapshot binding, and freshness checks. |
| `governance_v1` | Versioned approval request/receipt schemas, subject binding, reviewer metadata, and validity-window checks. |
| `mcp_service_v1` | Transport-neutral MCP gateway-to-service request/response contracts, principal assertions, side-effect class, and idempotency metadata. |

## Quick start

```toml
[dependencies]
protocol-contracts = { git = "https://github.com/nplongx/protocol-contracts" }
```

Decode a bounded COS-AP v1 envelope:

```rust
use protocol_contracts::{decode_envelope, MessageType};

fn main() -> Result<(), Box<dyn std::error::Error>> {
    let raw = br#"{
        "protocol":"cos-ap",
        "version":1,
        "message_id":"msg-1",
        "message_type":"job.proposed",
        "job_id":"job_1",
        "task_id":null,
        "attempt":1,
        "sender":"planner",
        "recipient":"workflow-runtime",
        "correlation_id":null,
        "created_at":"2026-11-01T09:00:00Z",
        "payload":{"title":"Example"}
    }"#;

    let envelope = decode_envelope(raw)?;
    assert_eq!(envelope.message_type, MessageType::JobProposed);
    Ok(())
}
```

## Security and trust boundaries

This crate validates structure, bounds, field relationships, selected identities, freshness, canonical representations, and content digests. It does **not**:

- authenticate a sender, service, reviewer, or provider;
- verify Ed25519 signatures or provision trust roots;
- authorize actions or enforce capability policy;
- prove that an evidence URI is retrievable or that a producer actually created an artifact;
- provide nonce consumption, replay protection, durable idempotency, or a network transport;
- establish that a governance decision is legitimate merely because its receipt parses and binds to a request.

Callers must obtain expected peer identities from an authenticated transport, verify signatures with independently provisioned trust roots, enforce authorization at the owning service, and persist nonce/idempotency/replay state transactionally.

## Compatibility notes

Some identifiers are deliberately retained because they are part of existing wire formats:

- `cos-ap` identifies the COS-AP protocol and its v1 envelope.
- `runalith.agg.external-checkpoint` remains the exact AGG checkpoint v2 digest protocol identifier.
- COS-AP v1 currently requires workflow IDs prefixed with `job_`.
- Evidence verification keeps its exact scope and signed-envelope kind constants.

Renaming these values would change wire compatibility. They are protocol identifiers, not a runtime dependency on Runalith.

## Development

Requirements: Rust `1.85` or newer.

```bash
cargo fmt --all -- --check
cargo test --all-targets --locked
cargo clippy --all-targets --locked -- -D warnings
cargo doc --no-deps --locked
```

## Documentation

- [Documentation index](docs/README.md)
- [Protocol glossary](CONTEXT.md)
- [Architecture and trust boundaries](docs/architecture.md)
- [Source lineage](docs/source-lineage.md)
- [Architecture decisions](docs/adr/)
- [Contributing](CONTRIBUTING.md)
- [Security policy](SECURITY.md)
- [Changelog](CHANGELOG.md)

## License

MIT. See [LICENSE](LICENSE).
