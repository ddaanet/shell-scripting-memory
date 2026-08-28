---
name: plugin-dev-subtree-updates
description: How to safely update the vendored plugin-dev toolkit subtree and what to check for consumer-side breaking changes
metadata: 
  node_type: memory
  type: reference
  originSessionId: dd3c35b3-18bc-4a1b-8274-98ae5ecccac6
  modified: 2026-07-28T09:52:14.549Z
---

The `plugin-dev/` toolkit is vendored via `git subtree` from
`git@github.com:ddaanet/claude-plugin-dev.git`, updated with
`just update-plugin-dev vX.Y.Z` (defined in `plugin-dev/release.just`).
Before running it across more than a patch version, check the target
tag's `plugin-dev/DESIGN.md` "History" section (clone the toolkit repo
to a scratch dir and `git show <tag>:DESIGN.md` — the local copy is at
the *old* version until the pull completes) for consumer-required
changes.

**Why:** updating from v0.3.0 straight to v0.4.2 pulled a breaking
change (v0.4.0): `release` now depends on a consumer-defined
`prerelease` recipe instead of `precommit` directly. Without adding
`prerelease: precommit` to the consumer's root `justfile`, `just`
refuses to compile *any* recipe (`unknown dependency prerelease`) —
not just `release`. `just --list` right after the subtree pull is the
fast way to confirm nothing broke.

**How to apply:** after `just update-plugin-dev vX.Y.Z`, always run
`just --list` before considering the update done. If the toolkit's
History notes a required consumer change, make it as a separate commit
from the subtree-pull merge commit (the merge commit is toolkit
content; the consumer-side fix is this repo's own).
