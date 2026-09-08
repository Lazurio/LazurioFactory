# Decision proposals and convergence

Status: review draft, 2026-09-08. These local identifiers are Factory proposals,
not new numbers in the maintained Lazurio decision register. They do not override
legacy runtime contracts until the owning decision is amended and consumers migrate.

## F1 — New Factory and installed product

**Direction accepted in the request:** new TypeScript development repository, thin
non-Git Managed Root, local and hosted work plus Buddy and AI Colleagues.
**Implementation proposal, not yet approved:** one Bun/TypeScript product, native
CLI and HTTP adapter, shared core, standalone distribution as the first supported
consumer channel. React/Vite for the real Launchpad remains under consideration;
the proof's tiny native HTML surface is not a final UI framework selection.

Baseline incremental cleanup of the old Source Root retains deployment coupling.
It remains the maintenance path for existing users, but cannot be the final daily
installation model. A wholesale source copy reproduces hidden assumptions and
licenses without review. Reuse behavior, fixtures and proven contracts selectively.
A new service per subsystem increases lifecycle and recovery complexity without
an independent consumer; reject that split at foundation stage.

An npm distribution could reuse current tooling but still requires correct runtime
and asset resolution. Standalone packaging reduces end-user runtime setup, at the
cost of larger OS/CPU artifacts and native signing/upgrade work. The bounded
[stack proof](stack-evidence.md) qualifies the choice only for its tested behavior.
Do not maintain npm and standalone as two independently implemented update channels.
If a package-manager shim is later needed, it must select the same verified release.

## F2 — A dedicated environment per Principal

**Direction accepted in the request:** retire the shared multi-Principal workshop
as the target execution topology. Collaboration occurs through authorized repos,
review and explicit handoffs. Infrastructure ownership may remain organizational.

Baseline shared workspace costs less infrastructure but combines credentials,
processes and recovery. A Unix-user-only split provides insufficient independence
unless the supported host envelope proves the missing controls. Dedicated provider
environments simplify attribution and failure scope; the cost is more provisioning,
per-seat updates and capacity management. Do not label this choice a new IAM system.

The hosting owner must specify and prove the isolation envelope. Dedicated placement
does not prove the Git pusher: verify GitHub identity and exact repo grants at the
operation boundary. Existing shared-App attribution must be disclosed and retired
or explicitly resolved before the dedicated cohort's acceptance.

## F3 — Profile is behavior, not authority

**Direction accepted:** coordinator behavior, configurable technical detail and
publication mandate are distinct. **Accepted ownership:** per-Machine profile, independently selectable for the same
Principal on different Machines. No automatic sync or global override engine.
**Proposed implementation:** versioned machine-local
preferences and deterministic root-owned generation through one CLI/core capability.

Editing generated instructions creates a second truth; editing Factory source for
every user creates personal product forks. Both are rejected. A generic plugin/profile
DSL is unnecessary. Predefined templates and preserved machine-local custom sources
are both accepted: free-form working instructions and proposed mandates are supported
design requirements. Composition precedence must be explicit; an imported proposal
is never effective authorization. Storage format and activation UI remain open.

Generation manifests identify owned files, expected previous digests and the
active preference revision. Product upgrade, profile activation and data migration
have different transactions and compatibility checks. See [recovery](migration-and-recovery.md).

## Required amendments before production implementation

| Existing authority | Proposed precise change | Preserved invariant / retirement evidence |
| --- | --- | --- |
| Decisions 0136 and resident-distribution knowledge | Factory source is optional development input; installed product owns runtime; preserve canonical Managed Root path | Source Root supported until explicit migration and restore proof; no second active Root |
| Decision 0137 and hosted Machine contract proposals | Replace shared Team workshop execution with a dedicated environment per Principal; manifest-derived eligibility remains | Existing shared environments retained only for bounded transition; stop new shared cohorts after approved cutoff |
| Decisions 0091, 0092, 0094 and Machine architecture | Clarify dedicated use versus infrastructure ownership and custodian recovery | Personalspace remains private, Buddy not Principal, AI Colleague own identity, parent operator boundary explicit |
| Decision 0129 | In Managed installations product upgrade uses artifacts, Organization Git synchronization keeps its own existing semantics | No product updater scanning/rewriting repositories; Source update retired by cohort |
| Decisions 0134, 0140 | Installed executable carries its runtime; development/module toolchain checks remain capability-specific | No automatic machine-wide PATH/tool upgrades; packaging does not claim third-party app dependencies bundled |
| Decision 0142 | Root generation composes purpose, behavior and locale from versioned inputs | Organization language ownership and stable locale-neutral reason codes preserved |
| Collaboration constitution / 0132 | Define coordinator acceptance with real harness capability and independent verification | Principal retains scope, access and publication authority |

Canonical amendments belong with the existing maintained decision owners. This
preparation records replacement text and acceptance intent; it neither edits live
host policy nor assigns new global decision IDs. Owner-specific migration and
infrastructure details stay outside this repository.

## Provenance and publication

`Lazurio/LazurioFactory` is a new public repository, not a transfer or rename of
`HumanAndMachines/Lazurio`. Creating the repository does not change legacy package
coordinates, Git remotes, signing identities, releases, version history or IP rights.

Public-first development was explicitly requested after repository creation. The
bootstrap history was inspected before changing visibility: one commit containing
only the short repository README. No legacy core or private content was published.

Before legacy code reuse/product release, the authorized owner must settle license and IP
provenance, preserving notices and exact source refs. Decide the final public source
URL and legacy redirect policy, artifact/package names and trusted signing identity.
Keep an auditable mapping `legacy source/ref → reviewed reused component → Factory ref`.
Do not copy private planning, provider operations or customer context into public docs.
The Principal selected [Elastic License 2.0](licensing.md) for newly owned Factory
code, documentation, runtime and embedded templates. User content and marketplace
submissions retain their own rights; dependencies retain original terms/notices.
No legacy FSL source is relicensed and no automatic Apache transition applies.

A candidate's provenance includes source repository and full commit, dependency
lockfile, toolchain pin, target, artifact digest and signed release metadata. A digest
alone detects corruption but does not authenticate its publisher. Trust bootstrap,
signing-key rotation, rollback retention and Windows/macOS distribution signing
must be implemented and exercised before user installation. No keys or workflows
are created by this draft.

## Open gates, owners and resolution evidence

The [release cycle proposal](release-cycle.md) recommends one product version,
immutable candidates and channel promotion without rebuild. Its two test paths, explicit Machine-wide candidate activation and promotion of the
same qualified artifact are accepted requirements. Concrete verbs, version/transport
semantics, trust mechanism and automatic update detection remain implementation proposals.

| Gate | Accountable function | Evidence needed |
| --- | --- | --- |
| Decision amendment acceptance | Product Principal and maintained decision owner | Reviewed canonical amendments, explicit migration scope |
| License/IP and product release | Authorized repository/IP owner | Reused-source inventory, license disposition, explicit product-release instruction; repository visibility is already public by request |
| Native supported platform floor | Factory maintainer | Native OS/CPU/ABI tests; build success alone insufficient |
| Hosting envelope and shared-workshop cutoff | Infrastructure owner | Dedicated isolation and identity smoke, recovery and decommission plan |
| Release signing and recovery | Distribution owner | Verified candidate, tamper denial, key rotation drill and offline restore |
| Coordinator capability | Harness integration owner | Actual delegated and unavailable-tool scenarios, not generated text assertions |

Function labels describe required responsibility, not granted permissions. Concrete
assignment and scheduling belong to the Organization's Mission Control.

## F4 — Qualification and one active installed product

Accepted: the first usable transition version requires official native macOS, Windows
and Linux installation, full CLI, real Launchpad and generated base instructions used
by actual Codex and Claude Code consumers. Preserved Launchpad scope is module
discover/start/status/stop plus the necessary navigation, readiness and error handling;
full unspecified legacy feature parity is not an accepted promise.

Accepted: three simultaneous worktree tests are isolated; a separately integrated,
qualified candidate may then be explicitly selected for the Principal's whole dedicated
Machine and real Root before stable release. These are not alternatives. A per-shell
override alone cannot prove daily activation. Repeated PATH rewriting and a separate
candidate updater are rejected because they create conflicting selectors. Extend the
installer's existing version selection and lifecycle owner; details remain proposals.
Build failure preserves active software. Program rollback and data recovery are separate.

## F5 — Profiles, evidence and the single marketplace

Accepted: expertise and proactivity are independent, profiles are Machine-local and
can propose Machine or Organization mandates without transferring effective consent.
Generated instructions discover current access instead of embedding an ACL snapshot.

Accepted: optional minimal field measurement informs profile/model/harness/task fit;
community sharing has explicit preview and author choice. Benchmark and field results
remain distinct. No guarantee of anonymity, universal best profile or backend exists.
Reuse profile version/provenance and existing consent/runtime owners rather than a
new recommendation identity graph, configuration engine or telemetry platform.

Accepted module consumer: an immutable authored release is deliberately integrated
as a tested draft into a customer's own Organization; later updates preserve local
changes through another integration. Licensing/entitlement/support/visibility terms
are independent open decisions, not consequences of Factory's ELv2.

Accepted hosted-assistance outcome: scoped advice and preparation of customer-owned
repo drafts can run without a local developer toolchain. Credit budget is not access
or publication authority. The provider isolation, credential delegation, charging and
lifecycle mechanisms require their actual consumer and failure evidence before launch.
No implementation, account service, billing or live migration is authorized here.

## Discussion gap audit and implementation routing

The initial foundation covered ownership, preservation and a preview proof. The
following gaps are now specified as contracts; this table is a coverage map, not a
claim of completed implementation or a second delivery ledger.

| Clarified requirement | Gap in initial foundation | Canonical implementation contract |
| --- | --- | --- |
| First transition usable on three OS / two harnesses | Compilation matrix did not bind actual harness behavior | acceptance.md: first usable transition gate |
| Retire legacy development checkout | Legacy path was only provenance | migration-and-recovery.md: retirement gate |
| Isolated tests and Machine candidate | No explicit distinction or active-selector lifecycle | release-cycle.md: two modes, state/failure contract |
| Dynamic discovery | Access checks lacked generated-agent entry flow | ARCHITECTURE.md: discovery at task entry |
| Expertise and proactivity | Collaboration/detail omitted domain competence | ARCHITECTURE.md: axes and profiles |
| Machine and Organization mandates | Scope was underspecified | ARCHITECTURE.md: scoped consent intersection |
| Optional evidence | No minimization/consent/bias contract | profile-evidence.md |
| Community loop | Catalog fields lacked share/try/adapt/feedback and moderation | marketplace.md: community loop |
| Provider business model | Not technical public-source authority | Owning Organization's private knowledge and planning; no customer/business data here |
| Paid immutable modules | No purchased-release integration/update consumer | marketplace.md: source purchase and integration |
| Dashboard assistance | No scoped execution/budget/recovery contract | hosted-assistance.md |
