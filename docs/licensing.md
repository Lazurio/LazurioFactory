# Licensing decision still open

The Principal is considering the license for Factory and its outputs. Public
visibility is accepted; a new license is not. No Apache license or relicensing of
existing source is introduced by this foundation.

The legacy CLI manifest declares `FSL-1.1-ALv2`. Do not copy that code into a newly
licensed tree or assume repository ownership permits removing third-party terms.
Before reuse, inspect the exact source license/notices and record the provenance.
This proof is newly authored for the requested task; no legacy implementation is
copied. Its runtime/development dependencies are pinned, and any distributed binary
must retain the notices required by what is actually bundled.

The current business intent is free use on one's own Machines and internal use
by organizations, while reserving commercial provision of hosted Lazurio environments
to third-party customers. Internal cloud hosting and selling a service to others
are distinct; physical localhost versus cloud is not the intended boundary.

The exact standard license remains under discussion, including whether restrictions
expire. Apache-2.0 from day one is not the current proposal. No custom hosting-only
license text, blanket relicensing or new license grant is introduced here. The owner
must approve the exact terms and resolve rights/provenance before applying them.

| Material | Required separate disposition |
| --- | --- |
| New Factory code and documentation | Owner's selected license and copyright notices |
| Existing reused code/assets | Exact original license and provenance; permission for intended reuse |
| Binaries and dependencies | Bundled-component inventory, original notices and distribution obligations |
| Embedded instruction/templates authored by Factory | Explicit output/template license, not an accidental inheritance assumption |
| User-authored content/custom profiles | Remains its author's content; generation does not assign it to Factory |
| Marketplace submissions | Each author's declared license and submission terms; catalog membership is not a universal relicense |

Release acceptance must inspect the resulting source and artifact bill of materials.
A package's metadata field is not proof that all included components have that license.
This preparation does not publish binaries, transfer IP, choose marketplace terms,
or modify the legacy project's license.
