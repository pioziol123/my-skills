---
name: write-documents
description: "Create non-code documents and substantially revise existing ones. Use before drafting documentation, reports, specifications, proposals, guides, learning materials, README, AGENTS.md, or skills, including documents created during coding tasks and documents for humans or agents. Applies across file formats and to complete documents delivered in chat. Excludes ordinary conversational replies, code, machine configuration, raw data, and temporary working notes."
---

# Write Documents

## Abstract

Create documents that readers can understand and use without reconstructing the conversation that produced them. Follow this sequence: establish purpose and audience, choose a form and outline, collect material, draft, review and verify, then remove your temporary notes.

## Scope and collaboration

Apply this workflow whenever creating a non-code document or substantially revising one. It covers documents for humans and agents, local files, connected document services, and complete documents delivered in chat. Code examples inside documentation do not exempt the document.

Ordinary conversational replies, progress updates, code, machine configuration, raw data, and temporary working notes do not require this workflow. For a typo correction or small local edit, preserve the requested scope rather than restructuring the whole document.

Combine this skill with relevant domain and artifact skills, such as specifications, writing for agents, Word, or PDF. This skill governs content preparation; other skills may supply domain requirements, formatting, and artifact verification. Respect the user's instructions and required templates. Resolve material conflicts explicitly rather than silently dropping a requirement.

Write the deliverable in the language requested by the user or established by its audience and context. The English language of this skill does not determine the deliverable's language.

## 1. Establish purpose and audience

Before drafting, briefly establish:

- Who will use the document and in what situation.
- Their relevant domain knowledge, and the context they may lack or need refreshed.
- What they should understand, be able to do, or decide after reading.
- Which information supports that outcome and where the document's scope ends.

Express purpose as an outcome for the reader. “Describe the topic” is insufficient. These decisions can remain in a short working note; they need not become a separate section of the deliverable.

If the purpose or audience is uncertain and cannot be established confidently from available context, ask the user before drafting content that depends on it. Match terminology and explanations to knowledge in the relevant domain, rather than labeling readers as generally “technical” or “nontechnical.”

## 2. Choose the form using Diátaxis

Before outlining, read [the Diátaxis instructions](references/diataxis.md). Identify whether the reader needs to learn through practice, accomplish a task, look up precise information, or understand a subject. Apply the writing instructions and quality criteria for the relevant form.

Use Diátaxis to recognize needs and organize content. Adapt it to the document's purpose; do not automatically create four sections or four files. Reports, specifications, and other genres can retain their own structure. A mixed document can contain sections with distinct functions.

## 3. Prepare an outline before drafting

Record an outline before writing the document's main content. For each planned section, identify the reader's question it answers or the need it serves. Include an abstract and a conclusion.

Order material by its dependencies: introduce concepts and context before they are needed. Cover the intended outcome without adding unrelated topics. Revise the outline after collecting material if necessary. Separate approval of the outline is required only when requested by the user or when a material unresolved question prevents proceeding.

## 4. Collect working material

Before drafting the final content, gather all information relevant to the document. When useful, collect it in temporary notes in the environment's appropriate working directory, separate from the deliverable.

Collect facts, sources, decisions, useful examples, questions, and gaps. Distinguish:

- Confirmed information from assumptions and interpretations.
- Existing behavior from plans and proposals.
- Material essential to the purpose from possible digressions.

Do not fill gaps with invented facts. Verify claims that need checking, ask for missing decisions, or state uncertainty when the document can still serve its purpose. Research should follow the needs of the content; this skill does not require an internet search for every document.

Notes contain working material, decisions, and the outline; they do not require recording private reasoning. Do not recursively invoke this workflow for your own temporary notes.

## 5. Draft for understanding without conversation history

Write for a reader who may lack context or need it refreshed. Make clear what is being discussed, why it works or matters, and what follows from it, to the extent needed for the document's purpose.

Do not shorten away premises, relationships, or explanations necessary for understanding. Pay particular attention to missing context: brevity does not justify leaving the reader to guess. At the same time, remove tangents that obstruct the intended outcome. Ask of every piece of information: “What is this for, and how does it support this document's purpose?”

Use terminology the audience understands, based on their domain knowledge. Familiar terms do not need explanation. Explain unfamiliar concepts in accessible language, adding an example only when it improves understanding.

Knowing a term does not imply knowing the meaning assigned to it by the author. If a word stands for an additional process, a collection of ideas, or project-specific decisions beyond its ordinary meaning, state that scope explicitly.

During review, ask: “Will the reader understand this term as the author intends, and does the surrounding text provide all the information needed here?”

For human readers, use useful examples and short narratives when they clarify complexity, a relationship, or a consequence. Omit them when they are unnecessary, delay the answer, or obscure the purpose. Present invented scenarios as examples. State the limits of an analogy when a misleading inference is plausible.

For agent readers, provide context and examples that support correct execution or interpretation. Make conditions, actions, branches, and completion criteria explicit where relevant.

## 6. Make the document easy to scan

Use informative headings, paragraphs that develop one main idea, lists for steps or parallel items, and tables for comparisons. Keep structure proportional to the document's length, terminology consistent, and information logically ordered.

Check whether reading the abstract, headings, and conclusion reveals the subject, progression, and main outcome. Scannability should help readers locate content, not replace adequate explanations with disconnected labels.

## 7. Include an abstract and a conclusion

Every document you create must contain both. Scale them to the document's length and form; a short document may need only one sentence for each. Adapt heading names to the required template while preserving both functions.

- The opening abstract conveys the subject, purpose or scope, and main message so the reader can quickly assess relevance.
- The closing conclusion states what follows: a finding, implication, result, decision, or next action appropriate to the purpose. It introduces no new facts or forced recommendations.

Finalize both after drafting the body. Avoid mechanically repeating the abstract in the conclusion.

## 8. Review content, sources, and the result

Before delivery, check:

- The document achieves its purpose and satisfies the quality criteria of its chosen Diátaxis form.
- The audience can understand it without conversation history or the author's unstated meanings.
- Claims are accurate, with assumptions, plans, and uncertainties distinguished.
- Essential premises, steps, definitions, and consequences are present.
- Every section supports the purpose; terminology and conclusions are consistent.
- Examples, narratives, and references contribute to understanding.
- The abstract and conclusion are present, and the document is easy to scan.

Include information and links to other documents only when needed for understanding, useful expansion of context, or substantiation of claims. Place references near the content they support. Supply essential context in the document itself rather than making the reader reconstruct it from several links. Do not add a bibliography or “useful links” list merely to make the document look complete.

Perform verification appropriate to the artifact and task. Distinguish editorial review from checking whether a described procedure works. Do not claim to have executed steps you have not tested.

After writing and verification, ensure all necessary findings and sources have reached the final document. Then delete only your temporary notes created for this document. Preserve source materials, user files, and the final deliverable. Completion includes verifying the result and removing your own temporary notes.

## Conclusion

A finished document serves a specific audience need, provides sufficient context, and communicates its outcome clearly. Judge structure, terminology, examples, and detail by their contribution to that result.
