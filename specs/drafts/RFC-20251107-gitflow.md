# RFC: GitFlow Strategy for SpringText

- Status: Draft
- Date: 2025-11-07
- Authors: SpringText Team
- Tracking: (fill when PR is opened)
- Related: specs/accepted/RFC-20251106-spec-workflow.md

## Summary
Adopt a GitFlow-inspired branching and release strategy tailored for SpringText to maintain stability on production while supporting iterative feature work driven by RFCs.

## Motivation
- Provide clear branch roles and merge policies as the project grows beyond a single maintainer.
- Enable structured releases with predictable integration (`develop`) and production (`master`) branches.
- Ensure RFC-driven feature work has a consistent path from proposal to release.

## Scope and Non-Goals
In scope: branch topology, naming conventions, release cadence, tagging, CI alignment.
Out of scope: monorepo considerations, package publishing automation, detailed release notes tooling.

## Prior Art
- Original GitFlow model by Vincent Driessen.
- Variants used in Rust ecosystem projects (e.g., Servo, ripgrep) combining `master` stability with `develop` integration.
- GitHub Flow (single main branch) considered but rejected due to desire for staged integration.

## Design
### Branches
- `master`: production-ready. Only release merges and hotfixes land here. Tag every release (`vX.Y.Z`).
- `develop`: integration branch. Feature and release branches target `develop`.
- `feature/<slug>`: spawn from `develop`, one RFC/feature per branch. Merge into `develop` via PR after acceptance and implementation.
- `release/<version>`: created from `develop` when stabilizing for a release (bug fixes, docs). After release, merge into `master` (tag) and back into `develop`.
- `hotfix/<version>`: branch off `master` for urgent fixes. After release, merge into both `master` (tag) and `develop`.

### Naming & Lifecycle
- Use kebab-case slugs (e.g., `feature/text-buffer-refactor`).
- Delete feature/release/hotfix branches after merge (auto-delete enabled).
- Require PR approvals per CODEOWNERS (currently @brandiqa).

### Tagging & Releases
- Annotated tags: `git tag -a vX.Y.Z` on `master` after release merges.
- Draft release notes summarizing accepted RFCs and major changes since last tag.

### CI Alignment
- GitHub Actions (`ci.yml`) runs on PRs and pushes to `develop` and `master`.
- Add release workflow triggered on tag push (`v*`) to build artifacts when applicable.

## Alternatives Considered
- GitHub Flow: simpler but lacks staging branch; rejected for long-running features.
- Trunk-based development with feature flags: future possibility but unnecessary now.

## Impact
- Clarifies contributor expectations and simplifies future onboarding.
- Slight overhead managing `develop` and release branches.
- Requires updating branch protections and CI triggers.

## Open Questions
- Release cadence (monthly? milestone-driven?)
- Automated changelog generation vs manual notes.

## Implementation Plan
1. Create `develop` branch from `master` and push to remote.
2. Update branch protections: require PR for `master` and `develop`, CI checks passing, CODEOWNERS review.
3. Update GitHub Actions to trigger on both branches and add tag-triggered workflow (future).
4. Document GitFlow summary in README (link to this RFC once accepted).
5. Move this RFC to `specs/accepted/` upon approval.

## Decision Record
Pending review.
