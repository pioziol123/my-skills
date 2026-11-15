# Solution design: decisions and contracts

Use when creating or reviewing the technical design for a defined scope. Read the relevant requirements and inspect the existing implementation where the approach relies on it. For a new system, identify technology choices as proposals unless already decided.

## Content guide

1. **Scope and document status:** requirements covered, unresolved decisions, source/code revision when useful, and how to read agreed constraints versus implementation snapshots.
2. **Approach and boundaries:** components, responsibilities, data flow, and the smallest diagram that clarifies an important interaction.
3. **Decisions:** chosen approach, reasoning and evidence, meaningful alternatives, tradeoffs, and assumptions under which the choice holds. Keep IDs stable. Label proposals and superseded decisions.
4. **Contracts and invariants:** externally observable interfaces and persisted semantics that implementation must preserve.
5. **Change and release approach:** relevant compatibility, migration, ordering across components, recovery, and rollout considerations.
6. **Verification:** how to establish acceptance and test the particular risks introduced by the change.

Scale this structure to the work. A small change may need only a few decisions and a contract. Record only relevant quality and operational concerns, tied to requirements or concrete failure modes.

## Make contracts decidable

For affected payload or storage fields, define identifiers, types, allowed values, requiredness, nullability, defaults, and what absence means where applicable. Distinguish omission, null, empty, and explicit deletion when they produce different effects. Prefer existing authoritative schemas by reference and describe the delta.

For interactions, consider the semantics that actually matter: authorization boundaries, error outcomes, atomicity, retries and idempotency, ordering or concurrent updates, and side effects. State dangerous or surprising behaviour explicitly. An omitted list meaning "delete all" requires a deliberate decision and verification, not an accidental default.

Technical reasoning may follow from verified code or engineering analysis. Describe inference as inference and uncertainty as uncertainty. A product rationale still needs a product source.

## Useful detail and reuse

Keep exact names and snippets when they define a contract or make a decision unambiguous. Label file inventories and implementation sketches as snapshots with a revision when useful. Do not treat every technical detail as equally binding.

Reference repository conventions and canonical architecture documentation when needed; describe only this change's exceptions and additions. The SD is not a second copy of the repository's test or style instructions.

For a port, design the integration and differences: compatibility gaps, state ownership, adapters, production requirements, and regression risks. Reuse verified logic while making its relevant contracts discoverable. Prior prototype success is evidence, not proof that production requirements are met.

## Verification and lifetime

Connect acceptance criteria to verification methods and add checks for concrete technical risks: duplicate effects on retry, partial migration, authorization leaks, serialization compatibility, or changed performance where relevant. State what the check observes. Verification proposals are not completed test results.

Select the document lifetime from project conventions. If none exist, keep the design current during implementation and reconcile material deviations before closing the work. Then treat it as a historical design record. Ongoing API and operational contracts belong in their maintained canonical locations, linked from the historical document. Use an existing ADR when it owns the decision instead of creating competing copies.
