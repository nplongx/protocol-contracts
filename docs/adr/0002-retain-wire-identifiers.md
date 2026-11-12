# ADR-0002: Preserve exact source wire identifiers

- **Status:** Accepted
- **Date:** 2026-11-12

## Context

The extraction includes multiple protocol families originally developed within one application. Several constants contain product-specific strings, and The legacy agent-message v1 envelope has established field and identifier constraints.

## Decision

Use a generic repository and Cargo package name, but preserve existing protocol IDs, scopes, kinds, enum wire names, field names, limits, and version constants. Do not normalize legacy identifiers during extraction.

## Consequences

- The crate can be adopted without silently changing existing wire bytes or semantic identifiers.
- Some public protocol identifiers retain historical product namespace strings.
- Generic branding applies to the repository/package, not to existing protocol namespaces.
- Any identifier change must be versioned and reviewed as a protocol compatibility change.
