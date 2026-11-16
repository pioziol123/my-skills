# Solution design: decisions and contracts

Use when creating or reviewing the technical design for a defined scope. Read the relevant requirements and inspect the existing implementation where the approach relies on it. For a new system, identify technology choices as proposals unless already decided.

## Content guide

1. **Scope and document status:** requirements covered, unresolved decisions, source/code revision when useful, and how to read agreed constraints versus implementation snapshots.
2. **Approach and boundaries:** components and their responsibilities, including the one owner of each fact the change shares between parts (the part that stores it, decides it or owns its fixed list); data flow, and the smallest diagram that clarifies an important interaction.
3. **Decisions:** each choice made among options, recorded as [Record decisions](#record-decisions) describes, with the assumptions under which it holds. Keep IDs stable. Label proposals and superseded decisions.
4. **Contracts and invariants:** externally observable interfaces and persisted semantics that implementation must preserve.
5. **Change and release approach:** relevant compatibility, migration, ordering across components, recovery, and rollout considerations.
6. **Verification:** how to establish acceptance and test the particular risks introduced by the change.

Scale this structure to the work. A small change may need only a few decisions and a contract. Record only relevant quality and operational concerns, tied to requirements or concrete failure modes.

## Record decisions

A decision is a choice between technical options that the owner made after weighing them: they proposed one and another was set beside it, or several were laid out and they picked. Everything else is written as a plain statement without alternatives: an answer to a clarifying question (one asking for a fact or an intent the owner holds), a point a requirement settles (cite its ID), behaviour observed in the existing code (marked as observed), and a choice an ADR or an earlier design already records (cite it rather than recording it again). The options a clarifying question named are not recorded.

Each decision carries:

- **The chosen option**, stated as a fact.
- **The reason**, in the owner's words, or none. Keep their sentence as given; analysis of your own goes into the options' consequences.
- **Each discarded option**, with why it was discarded: the owner's words, the verified fact that made them withdraw it, or "none recorded". Add its consequence in one line when it is a verified fact. List the options that were on the table, including ones the owner proposed and withdrew.
- **The consequences of the chosen option** that the owner accepted, including any design cost from the project's architecture rules.

Check each option against those architecture rules when the project has them, so the costs are on the table before the owner chooses.

A proposal awaiting a decision follows the same shape, labelled as a proposal, with the reasoning marked as yours. When revising a design, keep the recorded options as they are; an option that was never weighed stays out of the record.

## Make contracts decidable

For affected payload or storage fields, define identifiers, types, allowed values, requiredness, nullability, defaults, and what absence means where applicable. Distinguish omission, null, empty, and explicit deletion when they produce different effects. Prefer existing authoritative schemas by reference and describe the delta.

For interactions, consider the semantics that actually matter: authorization boundaries, error outcomes, atomicity, retries and idempotency, ordering or concurrent updates, and side effects. State dangerous or surprising behaviour explicitly. An omitted list meaning "delete all" requires a deliberate decision and verification, not an accidental default.

Technical reasoning about facts and consequences may follow from verified code or engineering analysis; a decision's reason follows [Record decisions](#record-decisions). Describe inference as inference and uncertainty as uncertainty. A product rationale still needs a product source.

## Useful detail and reuse

State contracts by meaning, not by name: the operations, their inputs and results, field semantics, errors, atomicity, ordering and idempotency. The implementer chooses file, function and type names, and a reviewer compares behaviour with the contract. "Implementable without guessing" refers to decisions and semantics, not to naming. Describe the current system in words ("the existing batch-save path") rather than paths; the implementer finds the code.

Reference repository conventions and canonical architecture documentation when needed; describe what this change adds or alters and its exceptions to them. Something that stays as it is appears as an invariant under contracts and invariants, citing the requirement that protects it, or as context the change builds on. The SD is not a second copy of the repository's test or style instructions.

The design states the current agreement. The progress of this change's implementation and its review rounds live in the tracker and version control; superseded decisions stay labelled in place.

For a port, design the integration and differences: compatibility gaps, state ownership, adapters, production requirements, and regression risks. Reuse verified logic while making its relevant contracts discoverable. Prior prototype success is evidence, not proof that production requirements are met.

## Verification and lifetime

Connect acceptance criteria to verification methods and add checks for concrete technical risks: duplicate effects on retry, partial migration, authorization leaks, serialization compatibility, or changed performance where relevant. State what the check observes. Verification proposals are not completed test results.

Select the document lifetime from project conventions. If none exist, keep the design current during implementation and reconcile material deviations before closing the work. Then treat it as a historical design record. Ongoing API and operational contracts belong in their maintained canonical locations, linked from the historical document. Use an existing ADR when it owns the decision instead of creating competing copies.
