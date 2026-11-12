# Source Lineage

## Upstream source

- Repository: [nplongx/runalith](https://github.com/nplongx/runalith)
- Original crate: `rust/crates/runalith-protocol`
- Source revision: [`29c24cfa2b6ead5704d26cf2746bc384f2938b80`](https://github.com/nplongx/runalith/tree/29c24cfa2b6ead5704d26cf2746bc384f2938b80/rust/crates/runalith-protocol)
- Upstream license: MIT

The selected source directory was clean at the extraction revision. The source was copied into a new directory and its workspace-inherited manifest was replaced with a standalone manifest. The direct dependency versions/features and all six source modules were retained.

## Extracted material

- All six files under the original crate's `src/` directory.
- `tests/fixtures/agg-checkpoint-v2-jcs-vectors.json`, referenced by the source crate's in-module tests.

The Cargo package is now `protocol-contracts`; its Rust import name is `protocol_contracts`.

## Excluded material

No Runalith runtime, network transport, service gateway, trust service, database, signer, or authorization implementation is included. External integration and host-specific verification tests remain in their owning Runalith crates. Those integrations are not implied by the standalone crate's unit tests.

## Compatibility identifiers

`runalith.agg.external-checkpoint`, `cos-ap`, evidence verification scope/kind values, and other versioned strings remain unchanged because changing them would change existing wire contracts. Their presence is protocol data, not an imported runtime dependency.

## Independence statement

The new repository has no workspace path dependency, Git submodule, or runtime dependency on Runalith. It maintains explicit source attribution and preserves MIT license terms. Future work is governed by this repository's own reviews and version history.
