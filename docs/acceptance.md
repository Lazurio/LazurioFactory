# Implementation acceptance

This is a public technical contract, not a second task/status ledger. Scheduling,
assignment and delivery status live in the owning Organization's Mission Control.
The foundation delivers documentation and a bounded proof only. Every future slice
must add evidence here or in its reviewed test/build instructions without claiming
the other slices are complete.

## Ordered consumer slices

| Slice | Prerequisite | Smallest real consumer and exit criterion |
| --- | --- | --- |
| 0 — Foundation review | Product intent and repository routing | Public architecture, explicit decision amendments, stack comparison, working standalone proof, independent review |
| 1 — Distribution | Accepted stack and release trust/layout decisions | Clean machine runs full installed CLI + Launchpad without source; signed/tampered/offline artifact cases and artifact secret scan |
| 2 — Managed generation | Slice 1 and ownership/schema contract | Fresh dedicated human environment produces only owned Root files, starts full app; unknown/edited paths preserved; rollback drill |
| 3 — Profile capability | Slice 2 and accepted behavior schema | CLI and Launchpad use the same profile use case; deterministic generation, stale revision refusal, session pin/restart and upgrade preservation |
| 4 — Environment purposes | Slices 2–3 and hosting amendment | Dedicated human/Buddy/AI Colleague acceptance with correct Principal, Owner, custody and unavailable-capability behavior |
| 5 — Migration rehearsal | Slices 1–4, legacy compatibility and restore mapping | Faithful dirty Source Root fixtures plus shared-workshop transition prove preservation, interrupted recovery and no-op unknown state |
| 6 — Opt-in cohorts | Rehearsal and explicit per-owner migration approval | Small native cohort on each supported OS, user completion evidence, observation and recovery; halt on data loss/identity ambiguity |
| 7 — General availability and retirement | Successful cohorts, public release approval | Published support matrix and release provenance; legacy install/update paths retired by declared criteria, backups retained by policy |

Do not silently fold ongoing legacy maintenance into a new Factory rewrite. Existing
fixes continue with their owners; selectively port proven contracts with provenance.

## Required scenarios

| Area | Positive proof | Negative / failure proof |
| --- | --- | --- |
| Installation | CLI and real Launchpad run from installed artifact in a fresh home without Factory/Bun source tools | Missing dependency, bad signature/digest/platform, hostile archive, occupied Root: no partial activation |
| Shared core | CLI and UI produce equivalent validated operation plans and reason codes | UI cannot bypass validation/authority; unknown fields/enums/schema rejected |
| Profile | Two Machines of one Principal retain different profiles; local change does not sync; detail changes independently from delegation and locale; deterministic digest; upgrade retains selection | Manual output drift, stale revision, unsupported purpose/locale, concurrent mutation, missing harness capability |
| Public development | Source, build commands and sanitized evidence publicly reproducible | CI catches synthetic secret and `.env` in archive without printing values; placeholders stay valid |
| Data preservation | Dirty index/worktree/untracked/ignored files, local refs/stashes and external linked worktrees match before/after | Disk full, permissions, interruption at every phase, path traversal, foreign Personalspace: stop safely |
| Runtime | One selected version, managed process tree drained/restored through its owner | Port collision, stale locator, busy executable, active writer, failed healthcheck do not kill unrelated work |
| Access | Live identity and exact repo operation attributable to correct Principal | Revoked membership, wrong account, shared-App ambiguity, peer credential access fail closed |
| Rollback | Exact old compatible product/profile with verified checkpoint and retained work | New schema/data or new user writes block blind downgrade and produce forward-repair plan |
| Retirement | Old route/process/credential/profile inventory empty after accepted cutover | Recovery dependencies or unattributed drafts prevent deletion |

## Platform matrix and truth labels

Target native acceptance: macOS arm64/x64, Linux glibc arm64/x64 and Windows x64/arm64.
Each cell is independently `not qualified`, `compiled`, `native tested` or `supported`.
Optional musl and unsupported CPU/OS versions must not be silently treated as qualified.
The release owner publishes exact minimum OS/ABI versions only from actual evidence.

Use Bun behavioral tests for pure/core and filesystem fixtures, a strict TypeScript
check for contracts, and native OS process/Git/installer tests for adapters. Browser
acceptance should use Playwright against the real Launchpad; adding it to this tiny
distribution experiment is not needed to claim a final browser acceptance gate.
Test docs-like source text only where the text itself is the contractual output.

On native Windows cover drive/UNC constraints, case-insensitive collision, path spaces,
file handles, executable replacement, reparse points, Git worktrees and environment
propagation into a clean process. On POSIX cover permissions, symlinks, process groups,
cross-volume rename, signal interruption and credential-socket boundaries.

Native compiled smoke does not prove app compatibility, signed distribution,
installer readiness, hosting isolation or migration safety. CI workflow presence
does not prove that an exact head passed. Preserve exact source/artifact versions
and test output with explicit skipped/unavailable cells.

## Custom profile and future marketplace acceptance

Custom free-form source survives regeneration and upgrade; shared/custom precedence
conflicts are visible. Export excludes private data and effective authorization.
Imported proposed mandates remain inactive without local scoped consent and stop
being effective after revocation. One catalog may present both profiles and modules,
but tests reject a profile installation targeting an Organization and require the
Organization's real module contract/rights for a module. Marketplace implementation
is a future workstream, not an added foundation service.

## Coordinator evals

Run actual harness scenarios, not only prompt snapshots: complete a bounded task
locally; delegate independent work with sufficient scoped context; receive a false
success report and catch it from the artifact; handle delegate failure/cancellation;
operate with no delegation tool; refuse a requested publication absent mandate;
avoid copying another Organization's data; preserve a nontechnical user's final
decision while presenting an understandable artifact. Score outcome completion,
scope/privacy, verified evidence, recovery and publication authority separately.
Record the exact harness/tool capability set. A generated instruction file alone
cannot pass these evals.
