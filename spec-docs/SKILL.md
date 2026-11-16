---
name: spec-docs
description: Create, review, and revise product requirements documents (PRDs), feature requirements with acceptance criteria, and solution designs (SDs). Use when turning a vision, brief, ticket, or RFC into these documents, or resolving review feedback and inconsistencies between them. Adapt to the project's templates and terminology.
---

# Product and solution specifications

Produce specifications that distinguish product intent, observable behaviour, and technical decisions. Match detail to the next decision or implementation step. This skill works with documents in a project repository or standalone, without requiring a tracker or another skill.

## Document ownership

| Document | Owns | Useful readiness condition |
|---|---|---|
| PRD | Audience, problem, desired outcomes, scope, constraints, stages | The first useful scope and its major unknowns are clear |
| Requirements | Observable behaviour of a bounded feature, business rules, acceptance criteria | An implementer can distinguish acceptable from unacceptable behaviour |
| Solution design / SD | Technical approach, decisions, contracts, change-specific verification | The selected work can be implemented without guessing critical contracts |

## Document levels

Each document stays at its own level. These are the defaults; an explicit project convention can override them.

| Document | Contains | Leaves out |
|---|---|---|
| PRD | Problem, goal, what changes for users, scope and exclusions, evidence of success, stages. Readable in a few minutes. | Technical solutions and detailed requirements |
| Requirements | Business and functional decisions and requirements, more detailed than the PRD. Each criterion says how it is checked in the same terms: an automated test, a check of the running product, a review. | Libraries, protocols, function, type, file and directory names |
| Solution design | Every technical decision: the requirements restated in precise technical language, with mechanisms, data and error semantics, and verification. Library, option and SQL names are fine. | Concrete paths, file names, function and type names; the implementer chooses them |

One thought at the three levels:

- PRD: "An operation spanning several modules is saved completely or not at all."
- Requirements: "An error in any step rolls back the writes of every module made during the operation, including steps that already succeeded."
- SD: "The transaction context travels in AsyncLocalStorage; an operation called inside a running transaction joins it without BEGIN or COMMIT; savepoints are not used."

Existing documents and tickets are evidence of content, not of style. When they mix levels, follow these levels rather than copying their form.

PRD → requirements → solution design is the direction of justification. Technical discovery can expose an upstream problem: surface it, obtain a scope decision when needed, then update upstream and reconcile downstream. Links may point in either direction; an index link does not make a product document depend on an implementation choice.

## Start with the requested work

1. Identify whether the user wants a new draft, a review, or a revision, and which document or work item is in scope. A review returns findings unless edits are requested. A request for one document does not require producing all three.
2. Read existing relevant documents and project instructions. Use the project's templates, naming, language, and lifecycle where available. Apply this skill to their content rather than imposing new headings. A local domain skill can supply stricter project conventions.
3. Split mixed sources by level. Tickets and notes often hold product intent, behaviour and implementation detail side by side: assign each consequential statement to the PRD, the requirements or the SD and restate it in that document's language. An implementation detail from a ticket becomes an SD decision, not a requirement.
4. Establish the sources and current decisions. Read linked source material needed for consequential claims; if unavailable, identify the gap. Read implementation code when an SD depends on existing behaviour. Verify where that code lives rather than inventing workspace paths.
5. Read the relevant guide: [PRD](references/prd.md), [requirements](references/requirements.md), or [solution design](references/solution-design.md).

For a new project without conventions, use the user's language and Markdown, and this default layout:

- `docs/specs/<id>-<slug>/PRD.md`, `requirements.md` and `solution-design.md`, where `<id>` is the tracker id of the initiative when one exists. Several work items share the requirements and design files, each in its own section with an anchor.
- Stable IDs per work item: `<item>-R01` for requirements and `<item>-AC01` for acceptance criteria, kept across revisions.
- Shared sections for criteria that every work item must meet and for cross-cutting rules, written once and cited by ID instead of copied into each item.
- A table per work item with the criterion, its condition and how it is checked.

Use only the files needed. Place standalone documents in the requested output location.

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

Write the next useful level of detail. For a large project, keep later stages at outcome level and fully specify only the selected near-term work item. A risky unknown can call for research or a prototype before a committed SD.

Preserve a single authoritative location for each rule or contract. Downstream documents reference upstream requirements and add decisions at their own level. Short contextual summaries are useful when clearly identified as summaries.

An implementer reads every sentence as something to satisfy, so write only what must hold:

- **Permissive constraints.** State the property that must hold ("one source of truth for the price list"), and leave the rest open. "And nothing else", "only" and "in exactly one place" belong in a document when that limit is itself the requirement, as in an acceptance criterion that a rejected change leaves the saved data as it was.
- **Branch on the set.** For a set whose members change without a revision of the specification, write the rule for all, some or none of its members ("every source in the catalogue"), not for today's members ("both sources").
- **An honest unknown.** A value nobody has decided is Open, as described in the evidence states above. A default is written only when a source sets it, the code shows it (Observed) or it is labelled Proposed.

Keep stable requirement and decision IDs where they support cross-references; retain existing IDs when editing. For small documents, section links are enough. Mark removed or superseded referenced items rather than reusing their IDs for a different meaning.

When revising, follow changed claims through the affected requirements, design, and linked work. Check additions and changed meanings as well as deletions. Update authorized dependent documents; report anything inaccessible or outside the requested edit scope as needing reconciliation. Preserve the project's language and vocabulary, including exact contract terms.

An SD must state which sections express agreed constraints and which are illustrative implementation snapshots. In a draft, those same sections remain proposals. Design decisions cannot weaken acceptance criteria without an explicit scope change.

## Finish with a consistency check

Before delivering:

- Check that each in-scope requirement has an observable acceptance condition, and that the SD's relevant decisions and verification cover it. Use links or a small mapping only when useful.
- Check for unsupported scope, invented reasons, unexplained contradictions, and missing semantics in the contracts touched by the change.
- Check affected cross-references, vocabulary, document paths, and source availability.
- Check the levels. The PRD and requirements hold no code identifiers, paths, library protocols or function names (tracker and requirement IDs are fine); a search for backticked identifiers in them should find only IDs. The SD holds no paths, file names or function names. When the project provides a check for this, run it on the documents you changed and resolve what it reports. The PRD reads in a few minutes. Genuine external constraints stay in the PRD even when technical.
- List remaining material questions and state what each blocks. A draft with open decisions is still a valid deliverable. Describe it as ready for implementation only for the portions whose material questions are resolved; never imply stakeholder approval that was not given.

Deliver the requested files or review findings, summarize the substantive decisions and remaining blockers, and name the next useful step. Writing specifications does not itself authorize publishing tickets, changing code, or starting implementation.
