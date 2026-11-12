# Contributing

## Compatibility first

Treat serialized field names, enum spellings, protocol identifiers, bounds, and canonicalization rules as public wire contracts. Do not rename or normalize them as part of a cleanup. Any breaking change needs a new protocol version or an explicit compatibility decision.

Read [CONTEXT.md](CONTEXT.md), [architecture](docs/architecture.md), and relevant ADRs before changing contracts.

## Validation boundary

Keep parsing and structural validation separate from authentication, cryptographic verification, authorization, durable replay prevention, and transport. Do not add service-specific runtime dependencies to this crate.

## Required checks

Requirements: Rust 1.85 or newer.

```bash
cargo fmt --all -- --check
cargo test --all-targets --locked
cargo clippy --all-targets --locked -- -D warnings
cargo doc --no-deps --locked
```

Cross-language canonicalization changes require updated golden vectors generated and independently checked by every supported reference implementation.

## Pull requests

State exact protocol families affected, whether wire bytes change, backward-compatibility impact, exact commands and outcomes, and what was not tested. Never infer authentication or authority from parser tests.
