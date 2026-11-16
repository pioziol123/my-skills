# PRD: product intent and scope

Use for creating or reviewing a product or initiative PRD, including an early vision. Keep it readable by the people deciding what should exist and why.

## Content guide

Adapt these sections to the existing template and maturity of the work:

1. **Context and sources:** brief origin of the initiative and links supporting its consequential claims.
2. **Problem and audience:** who faces what problem, when, and what they do today. Distinguish observed pain from a hypothesis to validate.
3. **Outcomes and evidence of success:** what improves and how the team could tell. Keep unagreed numerical targets visibly proposed; qualitative evidence is valid at an early stage.
4. **Scope and non-goals:** intended capabilities and meaningful exclusions, including the first useful release.
5. **User journeys:** a few representative paths through the product; enough to explain the scope without an exhaustive story inventory.
6. **Constraints and dependencies:** genuine business, operational, legal, or interoperability constraints supported by sources. Include a technical constraint here when it externally limits the product, with its origin.
7. **Stages and unknowns:** outcomes for later stages, key assumptions to validate, unresolved product decisions, and links to existing feature specifications.

Keep the PRD short enough to read in a few minutes. Leave technical solutions to the SD and detailed rules to the requirements.

For an early vision, a short document covering the problem, audience, outcome, first scope, and unknowns is enough. Omit irrelevant sections. For a meaningful missing fact, state what is unknown and what decision needs it, rather than leaving an unexplained placeholder.

## Product language

Translate mechanics into guarantees users can rely on. Preserve the guarantee when removing the mechanism.

| Mechanism in a draft | Product-level meaning |
|---|---|
| Child rows are deleted when their parent is removed | Removing a collection also removes the entries that belong exclusively to it |
| Changes remain in component state until a transaction commits | Edits take effect when the user saves; cancelling leaves the saved version unchanged |
| A worker retries the operation | A temporary interruption should not require the user to start again, if that guarantee is actually supported |

Do not invent a product guarantee just because a technical mechanism might provide it. Verify the semantics or label the translation as a question.

Keep detailed per-feature acceptance criteria in requirements and test methods in the SD. Product success measures belong in the PRD. If a project template includes high-level acceptance conditions here, retain them without duplicating the detailed criteria elsewhere.

## Readiness

A PRD is useful when a reader can identify the target user, intended improvement, selected scope, exclusions, and major unknowns. A full roadmap or detailed architecture is not required to start learning from the first work item.
