# Proposed release cycle

Status: recommendation under discussion, not an accepted release/deploy mandate.

Use one product version for CLI, server/Launchpad runtime and generator. Their
compatibility is tested as one delivered product. Profile/preferences schemas retain
their separate contract versions; they are not independently drifting binaries.

```text
reviewed PR + CI → main → immutable candidate artifacts → native acceptance
                      → opt-in preview → approved stable promotion
```

A merge does not roll out software. Candidate acceptance includes install, product
upgrade, profile preservation and recovery on each supported native platform. Preview
is opt-in. Stable requires an explicit authorized decision for the exact candidate.
Promote the same tested artifacts and digests; do not rebuild them at promotion.

Artifact identity is immutable (`version + target + digest + source provenance`).
Preview/stable are authenticated channel references selecting an existing artifact.
Publish monotonic channel metadata and retain signed historical metadata for restore;
the implementation must prevent a stale/malicious channel response from triggering
an unintended downgrade. An explicit rollback selects a known compatible retained
version and is distinguishable from normal channel progression.

If npm becomes a supported transport, settle version semantics before shipping:
`1.0.0-rc.1` and `1.0.0` are different package identities and cannot be renamed while
claiming identical package bytes. Either promote one already final-version immutable
package via distribution tags after preview qualification, or treat the final package
as a new artifact requiring qualification. The standalone recommendation avoids
making an unproven npm promotion promise; it does not forbid a future thin shim.

First-version update behavior should detect availability and explain compatibility;
activation remains explicit. Detection is not a download/execute mandate. Resident
updates require a bounded drain and safe resumption through the actual lifecycle
owner. Offline, failed signature, unsupported schema or unknown state preserves the
current installation and reports a precise reason.

Product update, profile activation and Source→Managed migration are distinct
operations. Rollback is permitted only with the compatibility and preservation
evidence in [migration and recovery](migration-and-recovery.md). Channel rollback
alone cannot reverse data/schema changes.

Before implementing the release publisher, accept: version/transport identity,
signing/trust bootstrap and rotation, channel authorization, artifact retention,
OS signing/notarization requirements, native support floor, update-check privacy,
and preview cohort exit criteria. Prefer the provider's standard release and signing
capabilities; do not create a general deployment service for this workflow.
