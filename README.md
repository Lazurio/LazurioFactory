# Lazurio Factory

Lazurio Factory is the TypeScript source, build and distribution foundation for
Lazurio: a maintained installed product with a thin generated, non-Git Managed Root.
People install a release; they do not clone this repository to do their daily work.

**Status: architecture and implementation preparation.** The small executable proof
tests distribution boundaries. There is no supported installer, updater, live Root
migration or production release here yet. Existing Lazurio installations remain on
their current supported implementation.

- [Architecture and ownership](ARCHITECTURE.md)
- [Decisions, alternatives and required amendments](docs/decisions.md)
- [Migration, upgrade and recovery](docs/migration-and-recovery.md)
- [Proposed release cycle](docs/release-cycle.md)
- [Selective Launchpad adoption and Doctor direction](docs/legacy-adoption.md)
- [Developer commands and conventions](docs/development.md)
- [Future shared marketplace](docs/marketplace.md)
- [Open licensing decision and output boundaries](docs/licensing.md)
- [Acceptance and implementation slices](docs/acceptance.md)
- [Stack experiment and evidence](docs/stack-evidence.md)
- [Agent contribution contract](AGENTS.md)

The target includes local and hosted human work, Buddy and AI Colleague environments.
Each working environment is dedicated to one Principal. OS/CPU, purpose and
collaboration preferences are separate axes; they do not create product forks.

This repository is public from its foundation, by explicit instruction. Architecture,
decisions, code, tests and build procedures are openly reviewable. Secrets and private
personal, Organization or customer data never enter Git history, artifacts or logs.
Creating it does not transfer history from `HumanAndMachines/Lazurio`, choose a
license for reused code, redirect distribution channels or authorize product release.
See [provenance](docs/decisions.md#provenance-and-publication) and
[public development](docs/public-development.md).
