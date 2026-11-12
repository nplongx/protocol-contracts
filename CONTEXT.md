# Protocol Contracts Language

## Message and wire format

**Wire contract**
A versioned schema and validation rules for serialized data exchanged across a defined boundary. A wire contract does not implement transport.

**Envelope**
A bounded message wrapper containing protocol identity, version, message identity/type, routing metadata, timestamp, and message-specific payload.

**Structural validation**
Checks that data satisfies a schema, size limit, field constraint, or exact binding rule. It does not authenticate the sender or prove that claims inside the data are true.

**Protocol identifier**
An exact value identifying a wire format or digest domain. Changing it may break compatibility and requires an explicit protocol-version decision.

## Evidence

**Evidence reference**
A durable source URI and expected digest. The reference alone does not prove source availability, authorship, or truth.

**Producer lineage**
A set of claims linking a source artifact to a task, attempt, result, and completion event. The fields require verification by the source-owning service or another trusted authority.

**Verification receipt**
A structured statement by an asserted verifier over an exact subject/snapshot. Structural validation does not verify the cryptographic signature or trusted identity.

## Governance

**Approval request**
A versioned request binding an exact subject, evidence digest, audience, idempotency identity, and validity interval.

**Approval receipt**
A response describing a decision over the exact request. Parsing and binding checks do not make the decision authoritative; the receiver must verify the authenticator and trust configuration.

**Principal assertion**
Identity metadata supplied by a trusted transport adapter. This crate cannot prove that the assertion came from an authenticated connection.

## Canonicalization

**Canonical JSON**
A deterministic serialization under a specific profile. Canonical bytes make digest calculation repeatable; they do not make the represented claims correct.

**Domain digest**
A digest over a canonical envelope that binds a payload to a protocol identifier, domain, and component version. A digest is not a signature.
