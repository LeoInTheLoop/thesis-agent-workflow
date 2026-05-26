# Paper Quality Rules

Use this reference for thesis prose, structure, tone, results, discussion, conclusion, and final-review edits.

## Thesis Boundary

The thesis contribution is whatever `paper_theme.md` declares — no more.

Before strengthening a claim, check whether the supporting evidence (experiment, table, figure, or cited source) is already in the thesis. If not, keep the stronger claim out of the body and record it as future work.

Common over-reach patterns to avoid:

- "Fully solves", "completely addresses", "guarantees", "eliminates".
- Generalising a method from one dataset/protocol to "any" similar problem.
- Implying downstream applications that were not measured.
- Claiming readiness for production, deployment, or certification without an evaluation.

## Good Paragraph Pattern

Every paragraph that makes a claim should follow:

1. **Claim** — the takeaway in one sentence.
2. **Evidence** — a metric (with unit and protocol), a citation, or a mechanism.
3. **Boundary** — scope, protocol condition, or limitation.

Avoid metric dumps that do not say why the number matters. Avoid claims that have no nearby evidence sentence.

## Chapter Roles

- **Introduction**: problem, RQ, contribution, thesis structure, delimitation.
- **Background**: technical background, related work, research gaps. Each gap maps to one RQ.
- **Method / Artefact**: design rationale, implementation, considered alternatives, evaluation setup.
- **Results**: observations only — "X achieved Y under protocol Z". No interpretation, no comparison to related work for the first time here.
- **Discussion**: interpretation grounded in cited mechanism or comparison to related work. No new raw numbers introduced for the first time.
- **Conclusion**: synthesis against RQs and contributions. No new numbers, no new citations.

If Results starts explaining implications, move that explanation to Discussion. If Discussion repeats dense numeric detail, compress it and point to Results via `\ref{}`.

## Cross-Chapter Echo

Maintain this chain:

`problem → RQ → evaluation question → result → discussion answer → conclusion recap`

Check especially:

- Abstract and Conclusion mirror the same method/result/limitation facts.
- Each RQ has a visible answer in Discussion or Conclusion.
- Each requirement has a status: fulfilled, partially fulfilled, not measured, or future work.
- Each limitation has a future-work path.
- Delimitations declared in the opening are acknowledged again near the end.

## Tone

- Use calm, evidence-led academic prose.
- Prefer `this thesis` / `this study` in the thesis body over "I" or "we".
- Avoid defensive, sales-like, or absolute wording.
- Use "partially", "not measured", "outside the current scope", and "future work" when that is the accurate status.
- Prefer natural clarification over stiff negation; use "not X" only when needed to prevent likely confusion.

Reflection chapters may use first person — see `reflection.md`.

## Numbers

Every important number needs:

- metric name,
- split / protocol,
- unit,
- role in answering an RQ, requirement, or limitation.

Before changing numbers, consult `requirements/numbers_consistency.md` and `final-submission.md`.

## Mixed-Status Reporting

When a result is partial or mixed, report it plainly. Do not inflate a partial result into a clean success, and do not hide it inside a limitations footnote.

Use direct status language, for example:

- Objective A: **fulfilled** under the reported protocol.
- Objective B: **partially fulfilled** — improvement observed but below target.
- Objective C: **not met** — remains the primary technical challenge.
- Objective D: **not measured** — future work.

## AI-Artifact and Plagiarism Hygiene

- Flag templated phrases that read as AI boilerplate: "In conclusion, it can be seen that…", "It is worth noting that…", "This paper aims to…".
- Flag over-structured paragraphs that read as bullet lists in disguise (every sentence starting with a transition word).
- Keep paraphrased material grounded in `Original_quote_or_core_statement` in `citation_ideas.csv` — never paraphrase from memory.
