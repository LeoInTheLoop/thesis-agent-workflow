# Paper Writing Guidelines (Unified Enforcement)

> Purpose: Unify paper structure, language, evidence, and AI-rewriting workflow to reduce repeated revision cycles.
> Writing requirements are jointly defined by `requirements/paper_guidelines.md` and `requirements/terminology/field_terms.md`.
> If conflict with official requirements exists, the official institution instructions take precedence.

## 1. Chapter Structure Rules
- Chapter 1 fixed logic: Problem → RQ → Contribution → Thesis Structure → Delimitation.
- Chapter 2 fixed logic: Technical Background → Related Work → Research Gaps.
- Chapter 3 fixed logic: Research Design → Data → Pipeline → Training/Optimization → Metrics → Reproducibility.
- Results: write only "what was observed"; Discussion: write "why / what it means".

## 2. RQ and Gap Alignment Rules
- Define a clear Main RQ + Sub-RQs (adapt count to your paper's scope).
- Research Gaps must correspond one-to-one with your RQs.
- Do not introduce new gaps or task threads unrelated to your RQs.

## 3. Language and Style Rules
- Use academic prose; prefer paragraph-form over bullet lists.
- Maintain an objective, restrained tone; avoid exaggeration and unsupported conclusions.
- Background → simple present tense; completed experiments → simple past; section introductions → simple present.
- Prefer `this thesis` / `this study` over first-person pronouns.

## 4. Citation and Evidence Rules
- Every key claim must have a citation; unsupported assertions are prohibited.
- Prefer 1–3 highly relevant references per claim; avoid citation padding.
- Use readable BibTeX keys (e.g., `Smith2021`); never use `ref1`, `article`, etc.
- First appearance of a method, dataset, or evaluation metric must include its source.
- When rewriting, never change "claim → citation" pairings.
- Original quotes in BibTeX `note` fields must be preserved; do not delete them.
- Each time you add or modify a `citation_ideas.csv` entry, verify against the original text in `ref/<BibTeX key>.pdf`; secondary summaries are insufficient.
- If a citation idea is logged in the CSV but the corresponding PDF is missing from `ref/`, treat the citation as incomplete.

## 5. Terminology Consistency Rules
- Authoritative source for terminology: `requirements/terminology/field_terms.md`.
% Reason: Keep terminology checks aligned with the current terminology file.
- Write the full term + abbreviation on first occurrence; use the fixed term consistently thereafter.
- Do not use multiple synonyms for the same concept within the same chapter.

## 6. AI Rewriting Execution Rules
Lock three things before each rewrite:
- What to change this time (scope).
- What must NOT be changed (RQs, terminology, citation keys, conclusion boundaries).
- What CAN be changed (sentence structure, paragraph order, expression compression).

Run four checks after each rewrite:
- Is the logic still aligned with the RQ?
- Is terminology consistent with the terminology sheet?
- Do all key claims have citations?
- Have templated AI phrasing or over-bulleted structures crept in?

## 7. Minimum SOP (Before Each Commit)
1. Read one paragraph of context above and below the target section.
2. Run a terminology consistency check.
3. Run a "claim → citation" pairing check.
4. Check that no undefined concepts were introduced.
5. Final check: tone and formatting consistency.

## 8. Hard Veto Items
- Any key assertion appears without a citation.
- Number of gaps in Chapter 2 does not equal the number of RQs, or is not aligned with them.
- Results and Discussion are seriously mixed together.
- Citation key uses ambiguous naming.
- A citation is moved to follow a sentence it does not actually support.

## Modification Log
- YYYY-MM-DD: Initial template created. Adapt chapter structure and RQ count to your own research design.
