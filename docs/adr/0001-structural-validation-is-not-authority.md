# ADR-0001: Keep structural validation separate from trust and authority

- **Status:** Accepted
- **Date:** 2026-11-12

## Context

The contracts contain identity claims, signatures, approval outcomes, evidence lineage, idempotency metadata, and side-effect classifications. A pure serialization crate cannot authenticate their origin or enforce authority merely by parsing them.

## Decision

The crate validates structural rules, exact field binding, supported protocol versions, size limits, canonical representations, and declared freshness. It does not verify cryptographic signatures, authenticate transports, configure trust roots, authorize actions, consume nonces, or persist replay/idempotency state.

Callers must obtain expected identities from authenticated contexts and perform authority checks at the owning service.

## Consequences

- Contracts remain reusable without a shared trust implementation.
- Documentation and APIs must not label structural success as verified authorization.
- Service adapters remain responsible for cryptographic and transactional safeguards.
