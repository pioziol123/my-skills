---
name: spec-docs
description: Create, review, and revise product requirements documents (PRDs), feature requirements with acceptance criteria, and solution designs (SDs). Use when turning a vision, brief, ticket, or RFC into these documents, or resolving review feedback and inconsistencies between them. Adapt to the project's templates and terminology.
---

# Product and solution specifications

Produce specifications that distinguish product intent, observable behaviour, and technical decisions. Match detail to the next decision or implementation step. This skill works with a single repository, a central specifications repository, or standalone documents, without requiring a tracker or another skill.

## Document ownership

| Document | Owns | Useful readiness condition |
|---|---|---|
| PRD | Audience, problem, desired outcomes, scope, constraints, stages | The first useful scope and its major unknowns are clear |
| Requirements | Observable behaviour of a bounded feature, business rules, acceptance criteria | An implementer can distinguish acceptable from unacceptable behaviour |
| Solution design / SD | Technical approach, decisions, contracts, change-specific verification | The selected work can be implemented without guessing critical contracts |

PRD → requirements → solution design is the direction of justification. Technical discovery can expose an upstream problem: surface it, obtain a scope decision when needed, then update upstream and reconcile downstream. Links may point in either direction; an index link does not make a product document depend on an implementation choice.

## Start with the requested work

1. Identify whether the user wants a new draft, a review, or a revision, and which document or slice is in scope. A review returns findings unless edits are requested. A request for one document does not require producing all three.
2. Read existing relevant documents and project instructions. Use the project's templates, naming, language, repository map, and lifecycle where available. Apply this skill to their content rather than imposing new headings. A local domain skill can supply stricter project conventions.
3. Establish the sources and current decisions. Read linked source material needed for consequential claims; if unavailable, identify the gap. Read implementation code when an SD depends on existing behaviour. Verify where that code lives rather than inventing workspace paths.
4. Read the relevant guide: [PRD](references/prd.md), [requirements](references/requirements.md), or [solution design](references/solution-design.md). For tracker handoff, multiple repositories, or combining skillsets, also read [workflow integration](references/workflow-integration.md).

For a new project without conventions, use the user's language and Markdown. A suitable default is `specs/<initiative>/PRD.md` and `specs/<initiative>/features/<slice>/{requirements,solution-design}.md`; use only the files needed. Place standalone documents in the requested output location. A readable slug is enough; ticket IDs are optional.

## Evidence and uncertainty

Distinguish these states in the prose or a small decision/open-question list:

- **Confirmed:** an explicit user decision or a supported statement from an authoritative product source. Link consequential or disputed claims to their source.
- **Observed:** behaviour verified in code, an experiment, or an existing product. It describes the current system, not automatically the desired product.
- **Proposed:** a recommendation with reasoning, awaiting a decision. Use this for suggested metrics, scope, or architecture that has not been accepted.
- **Open:** missing information, with the consequence of leaving it unresolved and the next action needed.

A plausible explanation is not evidence of a stakeholder's intent. Preserve a sourced choice even when its rationale is unknown; say the rationale is unavailable rather than inventing one. Schema names and prototype capabilities are evidence about an implementation, not authority for business rules.

Ask focused questions when answers change scope, user-visible behaviour, critical contracts, or feasibility. First use available sources; ask the smallest useful batch. Continue drafting unaffected sections while decisions remain open. Choose routine presentation details yourself. If the user requests a draft without questions, label uncertain choices and readiness explicitly.

When sources conflict, describe the conflict and its effect. An explicit current user decision governs the requested change; otherwise use the project's documented source precedence. Without such precedence, do not silently pick a winner. Keep the affected section provisional.

## Draft or revise

Write the next useful level of detail. For a large project, keep later stages at outcome level and fully specify only the selected near-term slice. A risky unknown can call for research or a prototype before a committed SD.

Preserve a single authoritative location for each rule or contract. Downstream documents reference upstream requirements and add decisions at their own level. Short contextual summaries are useful when clearly identified as summaries.

Keep stable requirement and decision IDs where they support cross-references; retain existing IDs when editing. For small documents, section links are enough. Mark removed or superseded referenced items rather than reusing their IDs for a different meaning.

When revising, follow changed claims through the affected requirements, design, and linked work. Check additions and changed meanings as well as deletions. Update authorized dependent documents; report anything inaccessible or outside the requested edit scope as needing reconciliation. Preserve the project's language and vocabulary, including exact contract terms.

An SD must state which sections express agreed constraints and which are illustrative implementation snapshots. In a draft, those same sections remain proposals. Design decisions cannot weaken acceptance criteria without an explicit scope change.

## Finish with a consistency check

Before delivering:

- Check that each in-scope requirement has an observable acceptance condition, and that the SD's relevant decisions and verification cover it. Use links or a small mapping only when useful.
- Check for unsupported scope, invented reasons, unexplained contradictions, and missing semantics in the contracts touched by the change.
- Check affected cross-references, vocabulary, document paths, and source availability.
- Keep product language in the PRD; preserve genuine external constraints even when technical. Put implementation mechanisms in the SD.
- List remaining material questions and state what each blocks. A draft with open decisions is still a valid deliverable. Describe it as ready for implementation only for the portions whose material questions are resolved; never imply stakeholder approval that was not given.

Deliver the requested files or review findings, summarize the substantive decisions and remaining blockers, and name the next useful step. Writing specifications does not itself authorize publishing tickets, changing code, or starting implementation.
