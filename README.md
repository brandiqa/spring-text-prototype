# SpringText

[![CI](https://github.com/brandiqa/spring-text-prototype/actions/workflows/ci.yml/badge.svg)](https://github.com/brandiqa/spring-text-prototype/actions/workflows/ci.yml)

SpringText is a modern, minimalistic text editor prototype built in Rust. The goal is to deliver a focused writing experience while borrowing proven ideas from existing editors instead of reinventing them.

## Specification Workflow

All product and architecture decisions flow through the RFC process located under `specs/`:

- Drafts live in `specs/drafts/`, accepted records in `specs/accepted/`, and declined proposals in `specs/rejected/`.
- Every RFC follows `specs/templates/RFC-TEMPLATE.md` and must cite prior art to reduce duplicated effort.
- Proposed changes are discussed via pull requests labeled `rfc`. As the sole maintainer, @brandiqa approves or rejects the RFC and moves the file to the appropriate folder.

The canonical workflow is described in [`specs/accepted/RFC-20251106-spec-workflow.md`](specs/accepted/RFC-20251106-spec-workflow.md).

## Branching Strategy

SpringText follows a GitFlow-derived model documented in [`specs/accepted/RFC-20251107-gitflow.md`](specs/accepted/RFC-20251107-gitflow.md):

- `master` tracks production-ready releases; each release is tagged (`vX.Y.Z`).
- `develop` is the integration branch for all feature work.
- Short-lived branches (`feature/<slug>`, `release/<version>`, `hotfix/<version>`) flow back into `develop` or `master` per the RFC.
- GitHub Actions validate pull requests targeting `develop` and `master`.

## Releasing

1. Ensure `develop` is merged into `master` and the CI badges are green.
2. Tag the release locally: `git tag -a vX.Y.Z -m "SpringText vX.Y.Z"` and push with `git push origin vX.Y.Z`.
3. The `Release` workflow runs tests, generates changelog notes via git-cliff, and publishes the GitHub release automatically.

## Getting Started

1. Install Rust (stable toolchain) from <https://rustup.rs>.
2. Clone the repository:
   ```bash
   git clone git@github.com:brandiqa/spring-text-prototype.git
   cd spring-text-prototype
   ```
3. Build and run the prototype:
   ```bash
   cargo run
   ```

## Development Workflow

Before opening a pull request:

```bash
cargo fmt --all
cargo clippy --all-targets --all-features -- -D warnings
cargo test --all --locked
```

GitHub Actions automatically runs formatting, clippy, tests, and link checking for all pushes and pull requests.

## Contributing

1. For substantial changes, author an RFC using the template and open a pull request labeled `rfc`.
2. Reference inspirations or prior art with stable links (commit permalinks, archived pages).
3. Once approved, the RFC is moved into `specs/accepted/` and tracked alongside the implementation work.

For smaller fixes (typos, refactors), open a regular pull request without an RFC.

## Roadmap Snapshot

- Establish the editor core (buffer model, undo/redo, UTF-8 correctness).
- Add basic UX: open/save, status bar, search.
- Integrate syntax highlighting and extensibility informed by accepted RFCs.

Follow accepted RFCs and issues for the authoritative roadmap. Contributions, feedback, and experiments are welcome!
