# Lazurio Platform architecture

Status: proposed implementation contract, updated 2026-09-13. Product direction is supplied
by the Principal; this document does not claim that the target is deployed. Decision
amendments and rollout gates are in [decisions](docs/decisions.md).

## Outcome and invariants

Provide a stable, maintainable product for hundreds of people building their own
Organizations, on local or hosted environments, including Buddy and AI Colleagues.
Removing architectural debt is the purpose; converting JavaScript syntax alone is
insufficient. **Lazurio Platform** is the chosen public source-available product and
codebase. Its reviewed source produces Lazurio releases; a source checkout is never the
installed product and does not remotely apply Machine changes. Architecture,
implementation and verification are transparent;
private data and credentials remain in their existing custody boundaries.

1. A normal installation and upgrade operate without any Platform source checkout.
   Installed Lazurio contains CLI, Launchpad and Lazurio Folder Factory. CLI and Launchpad
   invoke the same core; the shared core applies configuration and desired changes locally.
2. Lazurio Folder Factory plans, generates and reconciles only enumerated Lazurio-owned
   instructions/configuration in a non-Git Lazurio Folder.
   Organization repos, Personalspace, Git state and runtime data are never generator inputs to overwrite.
3. Every operation identifies the actual Principal, Machine Owner and higher host/operator boundary.
   Owner-local work uses the existing Machine/filesystem boundary; GitHub remains
   access authority for connected provider operations. Text, local paths and profile
   labels cannot grant provider access (proposed binding distinction in decision F6).
4. CLI and UI invoke the same use cases, validation and errors. Each persistent fact has one owner.
5. A failed operation preserves the last known usable generation or stops with recoverable evidence.
   Unknown state is a refusal to mutate, not permission to rebuild.
6. The legacy source-working directory and shared hosted workshop are explicitly
   transitional paths with retirement gates.

This preparation does not rewrite legacy apps, migrate current hosts, implement
account/billing services, choose commercial terms or create a release mandate.

## Current state versus target

| Concern | Existing evidence | Platform target |
| --- | --- | --- |
| Lazurio Folder | Supported source checkout also acts as the working directory | Installed product outside a thin generated non-Git Lazurio Folder |
| Distribution | Legacy npm gate explicitly expects package-only Launchpad unavailable | Full CLI and Launchpad work from installed artifacts, with source absent |
| Runtime | Existing CLI/core boundaries and extensive preservation fixtures are useful evidence | Port proven invariants into small owner-focused TypeScript modules |
| Hosted work | Shared Hosted Team Workspace is current documented model | Environment dedicated to one Principal, with higher provider boundary stated |
| Profile | Existing resident build profiles and locale contracts; no complete profile switch capability | Versioned preferences regenerate only owned output through one core use case |
| Dependency repair | Current decision 0133 rebuilds derived dependencies from the lockfile | Preserve that distinction: dependencies are rebuildable; user work is not |

Current-source observation is pinned to `HumanAndMachines/Lazurio` commit
`66dca7f09ec6e26e0c200db53903ab52a3d2b3dd`. The package gate in
`distribution/npm-package-gate.mjs` expects `LAZURIO_LAUNCHPAD_RUNTIME_UNAVAILABLE`.
This is evidence of a missing full-product packaging path, not evidence that every
existing runtime is broken. Module length alone is not a refactoring criterion.
The [adoption map](docs/legacy-adoption.md) specifies keep/adapt/remove decisions,
the first installed discover/start/status/stop consumer, and the accepted read-only
Doctor/explicit repair direction. Compatibility adapters must have retirement gates.

## Ownership and dependencies

```text
CLI entrypoint ───────────────┐
Launchpad HTTP/API adapter ──┼── application use cases ── platform/provider adapters
                             │          │
browser UI ── typed API ─────┘          └── pure contracts/profile renderer

Platform source → versioned build → installed Lazurio ─┬─ CLI
                                                       ├─ Launchpad → shared core
                                                       └─ Folder Factory → Lazurio Folder
                                                                            └─ selected profile (input)
Organization/Personalspace repos ← their own Git/data owners; never build output
```

The recommended stack is still a proposal, not a user-approved framework decision.
Start with one repository and one package, divided into directories when a real
consumer needs the boundary. Do not create a package, daemon or generic interface
per box. Core must not import CLI, browser, server or ambient filesystem state.
The application layer sequences operations. Adapters perform bounded filesystem,
process and Git/provider work. The server is a long-lived invocation of the same
installed executable, not a separate implementation of installation/profile logic.

| Fact / capability | Canonical owner | Consumer and lifecycle |
| --- | --- | --- |
| Source, profile templates, skills, default rules | Reviewed Lazurio Platform source | Build produces immutable release artifacts; no runtime edits to source |
| Installed executable and assets | Product installer/updater | Versioned OS-standard user installation location, manifest and retained rollback version |
| Chosen collaboration profile, locale, detail preference | Machine-local versioned settings selected by its Principal | Profile use case validates then generates instructions; upgrade preserves preference |
| Lazurio Folder generation and expected digests | Lazurio Folder Factory and its installed generation manifest | CLI or Launchpad invokes the shared core locally and replaces only listed owned paths |
| Organization identity, repo and app declarations | Organization manifests | Discovery and lifecycle consume them; Platform source never creates a second allowlist |
| Git access, membership, publication permission | GitHub | Live checks for online mutations; offline state is not fresh authority |
| Running app processes | Existing lifecycle owner, adapted once | One process tree and one state locator, bounded to the actual environment |
| Secrets and provider recovery | Existing credential/provider custody | Reference/operation proof only; no secret material in manifests or logs |
| Planning and delivery status | Owning Organization Mission Control | Links to code and knowledge; no product-local task ledger |

Installed executable location uses OS-standard per-user data/install conventions;
the target Lazurio Folder remains `<home>/Lazurio`. The release activation mechanism
must work on native Windows without assuming executable overwrite or POSIX symlinks.
Detailed physical layout is an installer-slice decision, constrained by these owners.

Platform developers use a separate source checkout. The canonical repository was renamed
to `Lazurio/LazurioPlatform` on 2026-09-13 while preserving its GitHub repository identity
and history. An Organization may temporarily retain the legacy local mount
`productionspace/LazurioFactory` until its guarded path migration to
`productionspace/LazurioPlatform`. Existing `development/Lazurio` legacy-source
coordinates remain migration provenance; changing a directory name does not select
a runtime. Legacy `development/Lazurio` is not part of the target standard Lazurio
Environment.
Retire an existing checkout only through the dependency/ref/worktree/dirty-work
inventory and restore gates in the migration contract; nothing is removed now.
Isolated worktree testing and explicit integrated-candidate Machine activation are
different accepted workflows, defined in [release lifecycle](docs/release-cycle.md).
Program selection and Lazurio Folder selection are independent; source edits
are never live.

## Confirmed system topology

A **Lazurio Environment** is one Machine's operational composition of compatible
installed Lazurio components and its correctly materialized **Lazurio Folder**.
`Managed Root` and `Lazurio Root` are historical aliases, not current user-facing names, because `root`
is ambiguous on Linux. Machines share a versioned environment contract and conventions/interfaces.
They do not share one live directory and are not required to hold identical state.

The **Conglomerate** is the end-state fleet/graph of Machines and their Lazurio
Environments across Organizations, including meaningful relationships and flows of
data, information and work. It is not a directory, an Organization, an access boundary,
an ACL or an authority. Canonical decision 0128 deprecated `Conglomerate` as the old
root/product name, while `Conglomerate Host` already names a specific infrastructure
Machine profile. The new fleet meaning therefore needs an explicit canonical amendment
and legacy-terminology plan; this draft does not silently rewrite either decision.

Dashboard initially presents the whole-system overview and reasoning surface. It owns
neither access nor a parallel copy of truth. GitHub remains access authority for each
connected Organization, and Machine facts remain local. Personalspace, credentials and
private content are not centralized or crossed. If Dashboard later originates a desired
change, that intent must write through to the fact's natural owner and the target Machine
must apply it through the local shared core exposed by CLI and Launchpad.

This is intentionally a minimal projection/view, not a central control plane. Whether
any central registry exists is open because it may conflict with the current
no-central-registry/no-global-sync rule. Also open are topology ownership,
discovery/projection/freshness, future write-through, privacy/observability, the physical
legacy local-mount migration and the legacy terminology migration. No implementation mechanism for
those choices is selected here.

## Public platform and private managed services

The public Lazurio Platform must remain independently installable and self-hostable for
personal and internal Organization use. It does not require Lazurio Account, Dashboard
or Human and Machine hosting to form a working Lazurio Environment.
An external implementer may help a customer deploy Lazurio for that customer's own
internal use; that implementation work alone is not a competing managed Lazurio service.

`HumanAndMachineEmpire` is the private integration repository owned by Human
and Machine s.r.o. It may pin the public Lazurio Platform together with private Lazurio
Account/Auth, Lazurio Dashboard and managed-hosting components for authorized company
collaborators. It is a development, test and service-delivery composition, not a runtime
authority or second source of Platform code. Component changes remain in their owning
repositories.

The public Platform is source-available under Elastic License 2.0. Personal and internal
company self-hosting remain allowed under that license. A third party offering customers
a hosted or managed service exposing a substantial set of Lazurio functionality requires
a separate commercial agreement from Human and Machine s.r.o.; approved partners may
receive such terms. Exact partner contracts, pricing and service implementation remain
open and outside this public architecture.

## Environment composition

| Axis | Meaning | Does not mean |
| --- | --- | --- |
| Platform | Detected OS, architecture, supported ABI and capabilities | Linux is Buddy; Windows is nontechnical |
| Purpose | Human work, Buddy acting for a human, or AI Colleague seat | Organization role or permission |
| Expertise | Domain methods and task competence, e.g. senior marketing specialist | Proven quality from a senior label |
| Collaboration / proactivity | Responsive drafts or proactive coordination within mandate | A persistent runtime, automatic access, merge or release authority |
| Explanation detail | Concise outcome versus implementation detail | Different approval authority |
| Locale | Versioned Lazurio Folder-owned instruction language and UI language | Translation or modification of Organization-owned content |

Validate supported combinations from the release manifest. Unknown combinations
fail before mutation. Keep legacy machine enums as migration input, not guessed
aliases. Roles such as Steward/Admin/Builder remain per Organization and provider-
verified. They are not Machine kinds or independent distributions.

A hosted human environment may be owned by an Organization but is dedicated to
one named Principal. It does not mount that human's private Personalspace. Buddy
belongs to its human's private boundary and is not a new Principal. An AI Colleague
has its own seat, identity, dedicated environment and one human custodian; custody
does not create access to another Principal's Personalspace. Organization-owned
work assets remain Organization-owned even when used by one person.

An OS account or container is not sufficient proof of isolation. The supported
hosting envelope must cover files, process control, credentials, network and
recovery; a parent operator remains a higher compromise domain. No Machine registry
or alternate ACL is added by this proposal.

## Coordinator collaboration contract

The default behavior understands the requested outcome, identifies authority and
scope, decides what to do locally and what to delegate, supplies sufficient bounded
context, follows progress, independently verifies returned artifacts and completes
the task or names a concrete blocker. Delegation is not completion.

The working profile is defined per Machine, not globally per human identity. One
Principal may use a developer/coordinator profile on one Machine and an everyday
assistant profile on another. OS does not choose behavior. CLI/UI changes affect
only the selected local installation; there is no automatic sync, global override
engine or central Machine registry. Explicit profile import/copy may be considered
later as a separate capability. Personal use does not implicitly install Buddy.
The requested [future marketplace](docs/marketplace.md) distributes pinned
declarative definitions into this same local profile capability. It is outside the
bootstrap; no store, backend, IAM or arbitrary install scripts are introduced.

Predefined and custom profiles are both accepted requirements. A custom profile may
contain free-form working instructions used to compose AGENTS.md and proposed mandates
for expected work. User-authored source remains separate from generated output and
survives regeneration/upgrade; storage format and activation UI remain undecided.

Composition has explicit precedence: harness/system constraints and live provider
rights remain binding; shared invariants and machine-local custom behavior compose,
with custom instructions refining defaults. Conflicts with an invariant are surfaced
for a decision, never silently resolved by last-write-wins. The generated AGENTS.md
identifies its input revisions; custom source is the supported authoring surface.

A proposed mandate is not effective authorization. The actual Principal in this
installation must supply explicit scope, consent provenance and revocation within
live rights. Import cannot transfer the author's consent, credentials or active
mandate. Mandates can concern a Machine (tools, version activation, owned processes) or
an exact Organization (campaign, publication, merge). Each requires an authorized
Principal and its own scope; Machine scope cannot grant Organization rights or the
reverse. An action crossing both boundaries must satisfy both, plus live provider
rights and higher constraints. Use the existing mandate owner/model, not profile
metadata as a new IAM. Export
reviews custom content for private data and excludes effective authorization and secrets.

One future marketplace covers both profiles and Organization modules. It shares
catalog presentation, discovery, authorship, descriptions and version metadata, but
keeps separate installation contracts: profile to a specific Machine, module to an
explicit project/Organization under its own rules (owner-local preparation in F6,
live GitHub rights for connected operations). No universal
package or second Organization access authority follows from the shared catalog.

The profile changes instructions and presentation; capability depends on actual
harness tools. With no delegation tools, report the limitation and perform the
bounded task locally when possible. With tools, give each delegate a concrete scope,
expected artifact, owner boundary, acceptance and stop conditions. Do not copy
unrelated Organization or private context. Validate actual diffs, test evidence and
exact versions, not just a delegate's self-report. Cancellation stops owned child work
without destroying artifacts. No profile can authorize publication by implication.

## Versioning and activation

Use separate versions for product release, machine-local preferences schema and generated profile
contract. Each release declares readable/writable preference and manifest versions,
supported platform/purpose combinations and rollback compatibility. A product
version alone cannot prove data downgrade safety.

The profile use case accepts a validated candidate and expected current revision,
renders deterministically, previews the owned diff, stages it and atomically activates
a generation after rechecking the revision. CLI is the supported profile entrypoint;
Launchpad and agents call that same application use case. No second UI writer.
The concrete CLI verbs and JSON schema become supported API only with the first
consumer slice. This repository's experiment is not that API.

New sessions capture the active generation. Running sessions keep their snapshot
and report that a restart is required; do not hot-rewrite instructions in a running
conversation. An upgrade preserves preferences and refuses unsupported schema or
purpose instead of resetting to defaults. A profile switch never installs software
or moves repositories. If generated files were edited manually, show drift and stop;
offer a reviewed preference change, not silent overwrite or bidirectional sync.

Only an independently controlled harness or OS boundary can technically prohibit
self-modification. Hidden directories and read-only policy text are not security
enforcement when the Agent can change permissions. Report the actual enforcement
level and avoid making an untrue isolation claim.

## Discovery at task entry

A Machine profile is not a snapshot of Organization access. Generated base AGENTS.md
instructs the agent, when entering a connected Organization, to use the installed CLI's shared discovery capability to identify
the active provider identity, accessible Organizations/repos, known local paths and
the permitted materialization procedure. It then reads the selected Organization's
AGENTS.md before work there. Base profiles never embed an Organization roster, its
instructions or private data. An Organization list is not authorization for all actions.

One provider probe serves CLI, Launchpad and Doctor. Its result separates provider
verification time/status and exact identity from checkout presence/path/health and
stale/offline metadata. Proposed result states include verified, denied, unavailable
and stale; cache is evidence with age, never a grant. Access for the exact mutation
is rechecked at the operation boundary. A provider outage prevents claims of fresh
rights; safe local inspection may continue under the applicable local boundary.
Revocation blocks unauthorized provider operations but does not delete local work.
Wrong identity, stale path or inaccessible repo leads to explanation and a legal
materialization route, not credential substitution or cloning another Principal's data.

## Profiles, evidence and assistance

The same senior marketing specialist may respond to assignments and hand over drafts,
or proactively coordinate authorized work. Expertise, collaboration/proactivity and
explanation detail are independent. Quality requires task-specific evals. "Worker"
is informal language for a Task Agent session, never an additional Principal persona.
Persistent proactive work needs an explicitly owned runtime and triggers; instructions
alone do not create background execution. Existing scheduler/lifecycle capabilities
must be used with revocation and cancellation, not a new always-on profile service.

Marketplace is primarily comparison and selection; personalization uses the same
Machine-local settings/generation path. [Measurement](docs/profile-evidence.md) keeps
controlled benchmarks separate from optional field evidence. [Hosted assistance](docs/hosted-assistance.md)
defines advice, draft execution and publication without a second Organization authority.
Neither future capability exists in the proof. Commercial strategy stays with its owning
Organization; this public source contains the complete generic technical boundaries.

## Maker's first use

Accepted entry journey: obtain the small CLI utility, select a community-tested
profile, create a Lazurio Environment and use an existing Codex or Claude Code installation
with the maker's own model access. First value is transferring a versioned working
method/persona into an agent already in use. An Organization, hosted environment or
platform credits are not prerequisites. Empty Organization discovery is a valid
initial state, not an onboarding failure. The CLI profile selection and generation
use the same settings owner; a full marketplace backend is not needed for this path.
Exact packaging and profile acquisition UI remain proposals. A profile transfers
instructions, not proven competence or identical capabilities across harnesses.
Codex and Claude Code are the initial supported consumers; others are future extensions.

First work may use the Principal's own files or personal repositories in their own
Personalspace. No Organization or Open Connector is required; external integrations
are optional through supported tools and the applicable access boundary. Company
repositories still belong to their Organization; another Principal's Personalspace
is never an onboarding fixture or import source.

## Technical founder: local preparation before GitHub

Both local entries are first-version priorities. The founder can prepare a useful local
organization/project with modules and Git history before creating or connecting a GitHub
account. [F6](docs/decisions.md#f6--two-priority-local-entry-journeys) explicitly proposes
how this accepted requirement changes the current Organization=GitHub model: owner-local
project preparation is distinct from a provider-bound Organization, with no invented
membership, roles or second ACL. The exact schema and canonical amendment remain pending;
this foundation does not implement either state or mutate existing installations.

Discovery starts by identifying the selected local scope. Maker Personalspace and
owner-local project work do not require a provider login. Connected Organization work
uses the live provider probe described above. CLI, Launchpad and Doctor share the same
binding-aware manifest/lifecycle contract: absent GitHub in an intentionally local project
is not a readiness failure, while a connected target with missing access remains denied.
Module local use validates ownership, license, manifest and required capabilities; remote
operations additionally require actual provider rights. A template cannot silently attach
a remote, enable hosting, grant access or start a paid service.

Explicit later binding inventories all affected local repos and work, previews exact
remote destinations/visibility and preserves history and files. Nonempty remote conflicts,
wrong accounts, revocation and partial completion have recovery gates in F6 and acceptance.
There is one project data owner throughout; connecting GitHub neither unlocks local code
nor deploys an app. Continued local use is allowed; team collaboration remains under the
connected provider contract rather than local role emulation.
