# One future marketplace: profiles and modules

Status: requested product vision and future roadmap, outside the current bootstrap.
There is no marketplace service, account system, billing, discovery backend or
executable extension capability in this foundation.

One shared marketplace for profiles and Organization modules is an accepted future
product requirement. Discovery/presentation, authorship, versions and descriptions
are shared; package contracts and installation targets remain distinct. A module
installs only into an explicitly selected Organization, with its manifest/schema,
repo ownership and live access/publish rules. The marketplace never becomes a
second ACL. No commercial terms, billing or license choice are inferred.

The active profile remains per Machine. A future marketplace distributes versioned
profile definitions which a Principal deliberately selects for a particular local
installation. Installing a definition is not importing another person's Root,
credentials, Organization data, Personalspace or authority. It must not update the
same person's other Machines implicitly.

## Minimal portable definition — proposal

Use one versioned declarative document when the first real consumer is built:

| Field | Purpose and boundary |
| --- | --- |
| `schemaVersion` | Definition format; unknown versions refused before activation |
| `id`, `version` | Stable publisher-scoped name and immutable definition version; name is not verified identity |
| `author`, `source` | Attributed author and original source reference; authorship alone is not trust or permission |
| `compatibility` | Required product/profile contract range and relevant platform constraints |
| `requiredCapabilities` | Declared harness features needed for intended behavior; missing capability is visible, not auto-installed |
| `preferences` | Supported behavior/detail/locale values from the existing profile contract |
| `description`, `intendedUse` | User-submitted explanation of proven use and suitability |
| `customInstructions` | Free-form user-authored source, separate from generated AGENTS.md |
| `proposedMandates` | Intended work/scope description, never imported consent or effective grants |

The actual schema is not implemented here. Avoid a speculative configuration DSL.
Predefined and custom instructions plus proposed mandates are accepted requirements.
Tools/plugins and arbitrary executable hooks are not implied. No postinstall/shell
scripts or provider grants are part of this profile definition. Field names and
storage format remain proposals. Module installation follows its own approved
contract, not the profile contract or an invented universal package.

Machine-local activation records the selected immutable version, source and digest,
the compatibility/capability check and the reviewed effective preference/output diff.
This record extends the existing local profile ownership manifest; it is not a second
profile database. A marketplace listing is discovery information, not permission.

Pin installed definitions. Discovering an update may notify, but never silently
activates new instructions or adds capabilities. A change requires the same checked
local profile operation, expected revision and session adoption policy as a local
profile edit. Show changed preferences and generated instructions before activation;
rollback uses retained compatible versions and preserves subsequent edits.

Custom source survives regeneration and upgrade. Shared/custom composition has
explicit precedence and displays conflicts before activation. Export/submission
includes reviewed portable source and intended-use explanation, never private data,
credentials, the author's consent or effective mandates. Local effective authority
requires this Principal's scope, consent provenance, revocation and actual rights.

Untrusted publisher content cannot redefine scope, bypass required approval or read
private data. Trust/authenticity, publisher verification and revocation, content
review, discovery/hosting, billing and executable extensions are future decisions.
Resolve them against real producer and consumer examples before building a store.

## Future acceptance

One synthetic producer publishes a declarative definition; two Machine fixtures of
the same Principal activate different pinned profiles without sync. Unknown schema,
unavailable capability, wrong compatibility and tampered definition fail before
activation. A new version produces an explicit diff and does not expand authority.
The test includes attempted secret/Root/data import and attempted install script.
It proves refusal without executing the content. Service launch and public profile
publication retain their own explicit mandates.
