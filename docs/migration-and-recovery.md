# Migration and recovery contract

Status: design and acceptance requirements. No operation described here has been
run against an active installation by this preparation. A compiled proof is not an
installer. Each future mutator must refuse unrecognized state before its first write.

## Three independent transactions

| Operation | Reads | May change | Must not change |
| --- | --- | --- | --- |
| Product upgrade | Authenticated release metadata, installed version, compatibility, current profile revision | Staged product version and its compatible generated output, activation pointer | Repo history, worktrees, Personalspace, module content, user preference intent |
| Profile update | Current preferences, expected revision, installed templates and ownership manifest | Versioned preferences and enumerated generated instructions/config | Installed software, credentials, repositories, runtime data, grants |
| Legacy source-working → Lazurio Environment migration | Exact source inventory, mount/Git/process state, supported destination, approved plan | Lazurio Folder placement and ownership transition using a dedicated migration procedure | Work loss, silent branch reset, remote rewrite, secret copying or automatic publish |

Organization Git synchronization remains an explicit existing operation. Do not hide
fetch, checkout, stash creation or reset inside product/profile update.

A working profile belongs to the individual Machine installation. Changing it here
does not update any other Machine used by the same Principal. Profile transport or
copy is outside this first capability; no automatic sync is part of upgrade.

## Shared local migration use case

The official installed CLI can complete migration without a running Launchpad, source
checkout or separate Folder Factory installation. CLI and Launchpad invoke the same
application-core use case; neither carries its own migration implementation. The core
orchestrates inventory, approved plan, verified checkpoint, transition and recovery
through platform adapters. Folder Factory supplies only profile-based owned content.

Equivalent inputs, authority and initial state must yield equivalent plans, checks,
effects and recovery outcomes through either interface. Both share the same operation
lock and recovery state; simultaneous CLI/Launchpad requests cannot create two writers.
UI presentation may differ. No command names, packaging split or new service are selected
here, and these requirements do not claim an implemented migrator.

## macOS Lazurio Folder compatibility aliases

The target macOS layout has exactly one real Lazurio Folder at `<home>/Lazurio`.
`<home>/Conglomerate` and `<home>/Conglomerate_GEN3` are compatibility symlinks to
that folder so historical chats and tools using either absolute path continue to
resolve the same files. The aliases are not additional Environments, writable replicas
or evidence that the legacy Conglomerate product meaning is current.

The eventual migration is a shared local-core operation exposed by CLI and Launchpad.
Folder Factory supplies the owned content contract, not the Git migration plan. Neither this source checkout nor a
remote Dashboard mutates a Machine directly. macOS is the first explicit adapter;
Windows and Linux require separate path/link evidence and must not inherit symlink
assumptions.

Before the first write, inspect all three paths with `lstat`, `readlink` and canonical
path resolution; inventory nested Git/worktree state and active writers; and identify
one authoritative populated tree. If more than one distinct real tree contains data,
the target is occupied, a symlink points elsewhere, or the state is not understood,
stop with a no-op report. Never merge or recursively copy the trees merely because
their basenames are recognized.

After a verified checkpoint and quiescence, move the one authoritative real directory
to `<home>/Lazurio` only when the destination is absent. Validate that canonical Folder
through Doctor, then create both legacy symlinks. An already-correct symlink is an
idempotent success. Journal the exact pre-state, move and link operations so interruption
can resume or report a bounded repair instead of guessing.

Before new writes, rollback may restore the original real basename and remove only
aliases created by the recorded operation. After new writes, keep the same canonical
Folder and perform forward repair; never recreate independent copies or discard newer
work. Do not remove the aliases while supported consumers or historical chat paths may
still reference them.

## Common mutation discipline

1. Identify Principal, Machine Owner and parent provider/operator boundary. Check
   exact filesystem/remote identity, platform capability and necessary live rights.
2. Acquire one owner-controlled operation lock and capture expected current revision.
   A stale lock is not deleted on age alone; verify owner process and recovery state.
3. Build a read-only plan. Enumerate owned paths, expected old digests, target schema,
   disk requirements, compatibility, running consumers and recovery checkpoint.
4. Stage in the same filesystem where atomic replacement is promised. Verify
   authenticated artifact provenance, digest, archive path containment, permissions,
   platform and no symlink/hardlink traversal. Refuse unsupported mounts/case collisions.
5. Recheck lock, fingerprint, preference revision and running-process policy before
   activation. An intervening edit invalidates the plan and requires a new preview.
6. Activate one coherent generation. Persist enough local non-secret operation state
   to distinguish prepared, activated and validated states after a crash. Do not build
   a second general workflow database: the installed manifest and bounded journal
   belong to the installer, not to access authority.
7. Verify the actual installed command and affected consumers using the activated
   version. CLI migration does not require launching the graphical interface; verify
   Launchpad readiness when it is an affected running consumer. On failure retain or restore the compatible prior generation. Report
   exact state and recovery action, never success merely because files copied.

POSIX rename and native Windows replacement/locking behavior need separate adapter
tests. Do not assert multi-file atomicity by independently renaming files. Prefer
immutable generation directories plus one activation record, with a supported
Windows launcher/selection mechanism proven before accepting the layout. Preserve
old versions until no running process references them and retention gates pass.

## Product upgrade and profile rollback

The release declares supported preferences and generated-manifest versions. Backward
read compatibility is checked before stage; write compatibility and rollback support
are checked before activation. Keep the original preference snapshot and exact prior
product/profile artifacts. A forward migration that makes old software unable to
read new state is an explicit no-automatic-rollback boundary. Restore the coherent
old product and preference generation only if subsequent work can be preserved;
otherwise stop for forward repair rather than start an old binary on incompatible data.

A profile update renders deterministic output without host secrets. It changes only
paths named in its ownership manifest, each matched to the expected old digest.
Untracked/unknown paths and edited generated files are preserved and block conflicting
replacement. Removed generated paths can be deleted only if still owned and unchanged.
New sessions select the new generation; existing sessions keep a pinned snapshot and
show restart-required state. Profile rollback is a new checked activation, not an
unconditional restoration over edits made since the previous activation.

Do not terminate unrelated processes to complete an update. Query the lifecycle owner,
request a bounded drain of affected managed processes and preserve open agent sessions.
If a running consumer cannot safely move, leave its old version installed and report
pending activation or require an explicit maintenance window.

## Legacy source-working directory inventory and preservation

Migration must run on each actual machine only after consent to its exact plan. The
supported Lazurio Folder is `<home>/Lazurio`; an occupied target or ambiguous folder is a blocker.
Do not create a second active locator, infer identity from a basename, or recursively
copy a Lazurio Folder with nested `.git` files and claim preservation.

Inventory includes:

- Legacy source repo identity, full HEAD, branch, remotes and upstreams; staged, unstaged,
  untracked and ignored user files; local-only commits and ongoing Git operations.
- Every nested Organization/module/productionspace repo and permitted own Personalspace,
  including `.git` indirection, refs/reflogs, stashes, linked worktrees and their sidecars.
- Worktrees outside the Lazurio Folder, bare common directories and absolute Git path references;
  runtime selection, open files/processes, leases and service definitions referencing paths.
- Config and manifests with exact schema/version, custom files and generated ownership;
  credential references and access proof without reading/copying secret values into evidence.
- Filesystem/volume boundaries, case collisions, symlinks, permissions/ACLs and free space.

Verify recovery before mutation: preserve the whole relevant Git common directory,
working trees and mutable data with platform-correct permissions. `git bundle` alone
does not preserve untracked files, dirty indexes, worktree linkage or all reflogs.
Stashing alone is not a migration backup. No clean/reset/rebase is used to make the
inventory easier. A merge/rebase/am in progress blocks migration until its owner
resolves it. Unknown layouts receive a no-op report and a supported repair proposal.

Classify old files into Folder Factory-derived, user-owned and unknown using an exact old
release/source manifest plus reviewed mapping. Unknown files remain preserved; they
are not guessed to be obsolete. Do not treat all ignored files as disposable caches.
Before relocating any linked worktree use supported Git relocation/repair with
proof on a faithful fixture; never rewrite arbitrary `.git` pointer text blindly.

## Legacy source-working → Lazurio Environment phases and reversal points

| Phase | Exit proof | Reversal |
| --- | --- | --- |
| Discover and plan | Exact inventory, known schema, approved owner/target, supported platform | No writes, no rollback needed |
| Checkpoint | Offline-restorable verified copy, refs/index/dirty/untracked/stash/worktree parity, enough space | Delete only own unused staging after safe cleanup check |
| Quiesce | Affected managed processes drained, active writers reconciled, fingerprint unchanged | Restart the exact old runtime; preserved sessions/files unchanged |
| Prepare managed target | Valid staged artifacts and generation; nested Git mapping validated; no new active locator | Restore/check old paths before resuming any writer |
| Switch active locator | One canonical Lazurio Folder and one runtime identity; native path/process checks | Before new writes, inverse relocation plus exact old runtime/config |
| Verify and allow writes | Actual CLI/Launchpad/module smoke, credentials operation proof, data/Git parity | After new writes, reconcile/preserve new work before restoring old layout |
| Retire source-as-runtime | Agreed observation period, backup restore drill, no dependent processes/paths | Historical source/backup retained until explicit retention decision |

After target-side user writes or incompatible schema changes, rollback is not a
simple directory rename. Compare both inventories, preserve new work, then either
perform a reviewed inverse migration or forward repair. Never silently discard new
work to recover a green check. Interrupted operations resume only from a recognized
journal phase and matching artifacts; ambiguity produces a no-op recovery report.

The optional developer source checkout is migrated separately from active Lazurio Folder
selection. Preserve legacy source refs, worktrees and provenance; do not redirect
its remote to Platform because the names look related. Platform is a separate repo.

## Shared workshop → dedicated environments

This is an owner-led infrastructure migration, separate from local environment migration.
Approve the amendment and stop creating new shared cohorts at a named rollout gate.
Inventory sessions, working copies, dirty branches, stashes, jobs, credentials and
organization-owned data with the authorized owner; do not inspect foreign Personalspace.
Attribute work to its owner instead of copying the shared directory to every seat.

Provision one isolated target per Principal using the existing infrastructure owner.
Re-establish each identity through its provider flow; never clone another person's
credentials. Preserve attributable drafts through authorized Git branches or explicit
scoped data handoff. Verify peer denial for files, process signals, network and
credential use, and disclose parent-operator access. Prove actual Git operation
attribution and effective repo grants from each target.

Drain the old workshop, prevent concurrent writers, redirect only owner-approved
entrypoints and verify the human/AI Colleague flows. After the agreed observation
and restore period, revoke old shared credentials through their owner, remove old
routes/services and retire the old shared profile and docs in their owning repos.
An unresolved attribution or restore test blocks decommission, not permission to
run two writable environments indefinitely. No current infrastructure is touched
by the Platform foundation.

## Legacy source checkout retirement

`development/Lazurio` is not a target standard component of a Lazurio Environment;
Platform development belongs in `productionspace/LazurioPlatform`. The GitHub repository
has been renamed; an existing `productionspace/LazurioFactory` checkout remains a legacy
local path until a separate guarded mount migration proves all consumers and worktrees.
Do not equate path relocation with runtime activation. Before retiring old source,
inventory shell/launcher/service paths, dependencies, scripts, open sessions, module
references and all linked worktrees in addition to refs/index/dirty/untracked/ignored
work. Prove no active consumer requires it and that recovery can restore the captured
state. Unattributed work or a remaining dependency blocks deletion; retain the checkout
as migration provenance until the explicit cleanup gate. This preparation deletes none.

The [two qualification modes](release-cycle.md) remain separate from migration. A fixture
is not a real-environment checkpoint. Integrated candidate activation in a legacy
source-working environment cannot bypass the explicit migration plan. A product downgrade
cannot restore a Lazurio Folder move, schema or user writes; the recovery plan
must evaluate each independently.
