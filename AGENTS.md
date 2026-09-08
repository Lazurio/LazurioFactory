# Lazurio Factory: implementation contract

This repository develops and distributes Lazurio. It is not an installed user's working Root.

Public-first is a project invariant. Keep source, architectural rationale, proposed
decisions, tests, reproducible build steps and safe evidence publicly reviewable.
Use configuration names and safe placeholders; never actual secret values, private
keys, personal/Organization/customer data, or private operational logs. Check staged
content, history and artifact contents before sharing. Follow `docs/public-development.md`.
Do not invent a secret store or hide harmless implementation details.

Read `ARCHITECTURE.md`, `docs/decisions.md`, `docs/migration-and-recovery.md` and
`docs/acceptance.md` before implementation. This foundation is a proposal and bounded
proof, not authorization to migrate an installation, transfer a repository, publish
a release or change access. Distinguish proposed contracts from executable evidence.

Use strict TypeScript and the exact `packageManager` toolchain. CLI and Launchpad
call one application core; platform adapters own filesystem/process/provider effects.
Keep product state, profile preferences and generated instructions separately owned.
Do not create an IAM, Machine registry, second app supervisor or a writable copy of
the source as a substitute for the installed product.

Work on a review branch in an owner-scoped worktree, preserve all unrelated work,
commit only scoped changes, open a PR and report exact validation. Primary `main`
is a reference checkout. Publication requires the Principal's explicit instruction
and live provider rights. A generated profile never grants permission.

Never read or copy another Principal's Personalspace. Organization data, credentials,
deployment inventory and planning ledgers do not belong in this product repository.
Do not import legacy source wholesale: preserve license and provenance for every
deliberately reused component, and port only behavior justified by a consumer.

The proof has no install/update/profile-write/migrate command. Do not quietly turn
it into one. Implement each subsequent slice only after its recorded acceptance and
decision prerequisites are satisfied. Test behavior and failure recovery, not source
text shape or arbitrary file-size limits. Compiling for an OS is not testing on it.
