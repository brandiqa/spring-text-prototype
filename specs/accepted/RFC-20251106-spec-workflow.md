 # RFC: Spec Workflow for SpringText
 
 - Status: Accepted
 - Date: 2025-11-06
 - Authors: SpringText Team
 - Tracking: (to be filled when MR is opened)
 - Related: specs/templates/RFC-TEMPLATE.md
 
 ## Summary
 Establish an RFC/ADR-style workflow to make design decisions visible, reviewable, and durable while leveraging existing prior art instead of reinventing solutions.
 
 ## Motivation
 We need a predictable process to propose changes, evaluate trade-offs, cite prior work on the web, and record final decisions for future contributors.
 
 ## Scope and Non-Goals
 In scope: spec directory layout, lifecycle, templates, and reference policy. Out of scope: implementation details of any specific feature.
 
 ## Prior Art
 - Rust RFCs (perma-commit links recommended)
 - ADRs (Architecture Decision Records)
 - Various open-source RFC processes (Kubernetes, Swift Evolution)
 
 ## Design
 - Layout: `specs/{drafts,accepted,rejected}/RFC-YYYYMMDD-<slug>.md` plus `specs/templates/RFC-TEMPLATE.md`.
 - Lifecycle: draft → accepted/rejected → implemented. Move files across folders on decision.
 - Review medium: GitLab Merge Requests (MRs) with label `rfc`.
 - Referencing policy: prefer stable permalinks (commit-SHA URLs) and include archived snapshots (e.g., web.archive.org) for external links.
 - Cross-link issues/MRs for traceability.

 ## Review Rules (single-maintainer)
 - Labels: `rfc` (required). Optional: `rfc:breaking`, `rfc:research`.
 - Approval: minimum 1 maintainer approval (you) to Accept; Rejection also recorded by 1 maintainer with a brief rationale.
 - SLA: Initial feedback within 3 business days; decision target within 10 business days for standard RFCs.
 - Acceptance criteria: clear motivation, prior art with stable links, explicit scope/non-goals, concrete design and trade-offs.
 
 ## Alternatives Considered
 - Free-form docs without lifecycle folders: simpler but harder to query and enforce consistency.
 - GitHub-only Actions for link checking: not suitable since we target GitLab.
 
 ## Impact
 - Improves decision traceability and onboarding; minimal runtime impact.
 - Enables optional CI checks for links and style on GitLab.
 
 ## Open Questions
 - Whether to adopt an ADR ID scheme in addition to dates.
 
 ## Implementation Plan
 1) Land directory structure and template (done).
 2) Adopt this RFC; move to `accepted/` when approved.
 3) `.gitlab-ci.yml` configured for rustfmt, clippy, tests, and link checks (done).
 
 ## Decision Record
 Accepted on 2025-11-07. This RFC defines the ongoing spec workflow. Future amendments should be submitted as follow-up RFCs or marked as amendments to this document.
 
