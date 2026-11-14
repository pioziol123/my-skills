# Requirements: observable behaviour

Use for a bounded feature or work item, whether or not it has a tracker ticket. Read its relevant PRD or brief; if none exists, make the provided user intent and limits explicit without manufacturing a parent document.

## Content guide

1. **Purpose, sources, and scope:** parent initiative if any, relevant source decisions, included behaviour, and meaningful exclusions.
2. **Actors and conditions:** who can do what, prerequisites, permissions, and relevant initial states.
3. **Behaviour and business rules:** outcomes triggered by user actions or external events; relevant transitions and failure behaviour.
4. **Acceptance criteria:** observable pass/fail conditions tied to the requirements.
5. **Quality constraints:** only relevant expectations such as latency, accessibility, privacy, reliability, or compatibility, with their origin and measurable conditions when known.
6. **Dependencies, decisions, and open questions:** what upstream sources actually establish, confirmed choices with sourced reasons, and unresolved matters with their consequences.

Use the smallest structure that covers the feature. Integrate criteria beside their requirements if this avoids repetition.

## Acceptance criteria

Express context, action/event, and observable result. Given/When/Then is optional. Prefer stable IDs such as `R-01` and `AC-01` when other documents or tasks need to cite them.

Example: "Given a member without edit permission, when they try to change a saved collection, the change is rejected and the saved collection remains unchanged."

Include negative and boundary cases that matter to the selected behaviour, rather than exhaustively listing every imaginable failure. "Works correctly" and "is fast" are not decidable criteria. A latency target needs a workload and measurement boundary; when these are unknown, record the target as an open decision or proposal.

Each in-scope requirement needs an acceptance condition. Criteria must not silently introduce extra scope. An accepted requirement may deliberately have no separately documented rationale.

## Reuse, rollout, and constraints

For a port or prototype reuse, compare the requested behaviour with observed capabilities. Record gaps explicitly: the prototype may be incomplete or unsuitable for production. Existing capabilities do not override requested requirements, and speculative extensions should not become accepted scope.

Define user-visible release conditions when relevant: who gets access, what existing users experience, and any agreed migration or compatibility promise. A feature flag or phased rollout is one possible implementation, not a universal requirement. Put its technical mechanism in the SD; preserve it as a constraint when explicitly required.

## Readiness

The selected scope is ready for technical design when its intended behaviour and acceptance conditions are clear enough to evaluate options. Identify material open decisions before presenting it as ready for implementation; unaffected parts may proceed independently.
