# Security Policy

## Scope

This library parses and validates versioned protocol data. It is not a cryptographic verifier, identity provider, authorization engine, transport security layer, replay database, or execution boundary.

## Safe integration requirements

- Authenticate the transport peer independently.
- Supply expected responder identities from authenticated connection state.
- Verify signatures using independently provisioned trust roots and the exact signed bytes/canonicalization profile.
- Enforce authorization at the service that owns the protected operation.
- Persist nonce consumption, idempotency, and replay state atomically with the protected state transition.
- Treat unknown or ambiguous outcomes as unresolved until reconciled with authoritative evidence.

## Reporting

Use GitHub private vulnerability reporting for this repository when available. Do not include secrets, credentials, private signatures, or production evidence in public issues. Include affected version and a minimal deterministic reproduction.

No production security certification or response SLA is claimed for this initial `0.1.x` extraction.
