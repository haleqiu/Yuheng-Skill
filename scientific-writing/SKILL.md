---
name: scientific-writing
description: Draft and revise scientific documents for robotics and computer vision research. Applies BLUF structure, Williams clarity principles, and domain-specific patterns. Use when writing or editing LaTeX papers, grant proposals, thesis chapters, abstracts, introductions, related work, or experiment sections.
---

# Scientific Writing for Robotics and Computer Vision

## Core Principles

### 1. Three Laws of Communication (Doumont)

1. **Adapt to your audience** — Structure for the reader's reasoning, not yours.
2. **Maximize signal-to-noise** — Everything that doesn't help the message detracts from it.
3. **Use effective redundancy** — Reinforce key messages through verbal and visual channels.

### 2. BLUF: Bottom Line Up Front

- Lead every paragraph with its main claim (topic sentence).
- Lead every section with its key message.
- Readers should grasp your purpose from the first 1-2 sentences.

### 3. Williams' Clarity Principles

- **Characters as subjects**: Make actors the grammatical subjects.
- **Actions as verbs**: Express key actions as verbs, not nominalizations.
- **Old before new**: Open with familiar information, end with new.
- **Get to the verb quickly**: Avoid long introductory phrases before the main verb.
- **Be concise**: Cut meaningless words; prefer affirmative over negative.

### 4. Style Rules

- **No em dashes** (`---`). Use parentheses, colons, semicolons, or restructure instead.
- **One sentence per line** in `.tex` source files (cleaner diffs, easier editing).
- **No undefined terminology**. Never introduce a new technical term unless it is defined on first use or already standard in the field; if you use a coined term, include a one-sentence operational definition.
- **Do not add colons by default**. Use `:` only when introducing a short, explicit list or formal definition; otherwise prefer a period or sentence rewrite.
- **Avoid repetitive "Label: statement" openings** across consecutive lines (for example, repeated patterns like "Benchmark comparability: ..."), because this pattern reads mechanical and reduces narrative flow.

---

## Document-Type Structures

### Research Paper

**Abstract** (single paragraph, 150-250 words):
1. Context/Problem (1-2 sentences)
2. Gap or limitation (1 sentence)
3. Your approach (1-2 sentences)
4. Key results with numbers (1-2 sentences)
5. Implications or availability (1 sentence)

**Introduction flow**:
1. Motivation: Why does this problem matter?
2. Gap: What's missing in current approaches?
3. Approach: What do you propose? (high-level)
4. Contributions: Bullet list of specific technical contributions

**Contribution statement**:
```latex
Our key contributions are:
\begin{itemize}
    \item We introduce [method] that [key capability].
    \item We demonstrate [result] achieving [metric] over [baseline].
    \item We release [dataset/code] to enable future research.
\end{itemize}
```

**Figure guidelines**:
- First figure: Overview of approach with visual pipeline.
- Captions tell the complete story (understandable without main text).
- Use "so what" captions, not "what" captions.

### Grant Proposal

**Structure (NSF CAREER style)**:
1. Motivation (1 page)
2. Scientific Context and Related Work (1-2 pages)
3. Intellectual Merit and Contributions (0.5 page)
4. Research Thrusts — each: Goal, Approach, Expected outcomes, Risks and mitigation
5. Broader Impacts
6. Timeline/Management

**Structure (Internal/Seed Proposal)**:
1. Motivation (problem + recent advances + gap)
2. Objectives
3. Tasks (numbered, specific deliverables)
4. Estimated Timeline (3/6/9/12 months)
5. Team
6. Budget (if required)
7. References

### Thesis

**Abstract** (multi-paragraph):
1. Problem scope and importance
2. Thesis statement (1-2 sentences)
3. Each major contribution as a paragraph (align with chapters)
4. Synthesis: how contributions advance the field

**Chapter structure**:
- Each chapter can mirror a paper structure.
- Add connective tissue: how this chapter builds on previous / leads to next.
- Introduction chapter: broader context than any single paper.
- Conclusion chapter: synthesis and future directions.

---

## Drafting Workflow

1. **Identify document type and audience**
   - Paper: peer reviewers, then area researchers
   - Grant: program managers, then review panel
   - Thesis: committee, then future students
2. **Outline message hierarchy**
   - Main claim (1 sentence)
   - Supporting claims (3-5 key points)
   - Evidence for each claim
3. **Draft topic sentences first**
   - Write only the first sentence of each paragraph.
   - Check: do these sentences alone tell your story?
4. **Fill in supporting evidence**
   - Each paragraph: topic sentence + evidence + interpretation.
5. **Add transitions and flow**
   - Connect paragraphs with logical bridges.
6. **Verify references**
   - Read the [bibtex-verification skill](../bibtex-verification/SKILL.md) and follow its steps: locate the `.bib` file, run the checker script, and fix any issues by fetching correct entries from arXiv or publisher pages.

## Revision Workflow

1. **BLUF Check** — Read only topic sentences: do they convey your argument?
2. **Williams' Diagnostic** — Circle subjects (are they actors?), circle verbs (are they actions?), fix nominalizations.
3. **Signal-to-Noise Audit** — Cut filler ("it is important to note that", "in order to"), hedges, redundancy.
4. **Flow Check** — Read aloud, check sentence variety, check paragraph length (3-7 sentences).

---

## Quick Concision Reference

| Wordy | Concise |
|-------|---------|
| in order to | to |
| due to the fact that | because |
| in the event that | if |
| at this point in time | now |
| a large number of | many |
| has the ability to | can |
| prior to | before |
| for the purpose of | to, for |
| with regard to | about |
| in spite of the fact that | although |

## Anti-Patterns

- **Burying the main point**: Long windup before the key finding. Lead with the result.
- **Nominalizations**: "make a decision" -> "decide", "conduct an investigation" -> "investigate".
- **Passive voice overuse**: "The model was trained" -> "We trained the model". (Use passive only when actor is unknown or emphasis requires it.)
- **Information without interpretation**: "Table 3 shows results" -> "Table 3 shows our method outperforms all baselines on indoor environments."
- **Vague quantifiers**: "significant improvements" -> "15% higher accuracy on the test set."

---

## Revision Checklist

### Structure (Macro)
- [ ] Abstract follows problem, gap, solution, results pattern
- [ ] Each section opens with its main message
- [ ] Each paragraph has a clear topic sentence
- [ ] Contributions are explicitly listed
- [ ] Figures have informative "so what" captions

### Clarity (Micro)
- [ ] Subjects are characters (people, methods, systems)
- [ ] Main verbs are actions (not "is", "has", "involves")
- [ ] Sentences open with familiar information
- [ ] Main verb appears within first 7-10 words
- [ ] No unnecessary nominalizations

### Concision
- [ ] No filler phrases
- [ ] No redundant modifiers ("completely eliminate")
- [ ] No vague quantifiers without numbers
- [ ] Every sentence earns its place

### Flow
- [ ] Paragraphs connect logically
- [ ] Sentence length varies
- [ ] Technical terms defined before heavy use
- [ ] Acronyms spelled out on first use

### References
- [ ] `.bib` file exists and all `\cite` keys resolve
- [ ] Entries verified against arXiv / publisher pages (read and follow [bibtex-verification skill](../bibtex-verification/SKILL.md))
- [ ] `bibtex` compiles with zero warnings

---

## Additional Resources

- For detailed sentence patterns, domain templates, and examples, see [patterns.md](patterns.md).
