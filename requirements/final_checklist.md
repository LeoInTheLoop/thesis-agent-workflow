# Final Thesis Review Checklist

> For AI agents: follow the methodology in Section 0 before touching any checklist item.
> This checklist is derived from all accumulated workflow rules and failure modes.

---

## 0. Checking Methodology (Read Before Starting)

Checking a long thesis document in one pass causes context overflow and missed cross-chapter errors.
Use the following phased approach instead:

### Phase order

```
Phase 0 — SCAN (no edits)
    ↓
Phase 1 — Hard Veto (blockers first)
    ↓
Phase 2 — Structure + RQ alignment
    ↓
Phase 3 — Citation audit
    ↓
Phase 4 — Terminology sweep
    ↓
Phase 5 — Style + language
    ↓
Phase 6 — Placeholder cleanup
    ↓
Phase 7 — File integrity
```

### Phase 0 — Scan pass (mandatory first step)

**Do not edit anything during this phase.**

1. Read `paper_theme.md` to load the thesis scope and RQs into context.
2. Read `requirements/terminology/field_terms.md`.
3. Skim `thesis.tex` chapter by chapter — note section headings and approximate content only.
4. Produce a short issue inventory grouped by phase:
   ```
   Hard Veto candidates: [list]
   Structure issues: [list]
   Citation issues: [list]
   Terminology issues: [list]
   Style issues: [list]
   Placeholders remaining: [list]
   File/path issues: [list]
   ```
5. Show the inventory to the user and confirm which phases to run.

> Reason: A scan-first approach prevents a fix in Chapter 2 from creating an inconsistency
> in Chapter 5 that was not yet checked. Batching by type keeps context focused.

### Batch size rule

- Process one chapter at a time within each phase.
- After finishing a chapter, summarize changes before moving to the next.
- If a fix in one chapter requires a matching change elsewhere, flag it — do not fix it
  in the same pass. Add it to the next round's issue inventory.

---

## Phase 1 — Hard Veto Checks (Blockers)

Stop and resolve these before proceeding to later phases.
Any single failure here means the thesis is not ready for submission.

- [ ] **No key assertion appears without a citation.**
  Check: grep for sentences ending in a strong claim (e.g. "significantly", "outperforms", "demonstrates") that have no `\cite{}` within the same sentence or immediately following.

- [ ] **Number of research gaps in Chapter 2 equals the number of RQs.**
  Check: count gap items in Chapter 2 Section "Research Gaps"; count RQs in `paper_theme.md`; they must match one-to-one.

- [ ] **Results and Discussion are not mixed.**
  Check: Results chapter contains only observations ("X achieved Y"); Discussion chapter contains interpretation ("This suggests Z because..."). Flag any "This suggests" or "because" in Results, and any raw numbers introduced for the first time in Discussion.

- [ ] **All BibTeX keys use readable naming (AuthorYear format).**
  Check: `tex/biblio.bib` — no keys named `ref1`, `article`, `paper`, `cite1`, or similar.

- [ ] **No citation has been moved to a sentence it does not support.**
  Check: for each `\cite{key}`, verify that the sentence it follows is actually supported by `Original_quote_or_core_statement` in `citation_ideas.csv` for that key.

---

## Phase 2 — Structure and RQ Alignment

- [ ] Chapter 1 follows the fixed logic: Problem → RQ → Contribution → Thesis Structure → Delimitations.
- [ ] Chapter 2 follows: Technical Background → Related Work → Research Gaps.
- [ ] Chapter 3 covers: Research Design → Data → Pipeline → Metrics → Reproducibility.
- [ ] Each gap in Chapter 2 is explicitly linked to a specific RQ (either by name or `\ref{}`).
- [ ] Contributions listed in Chapter 1 are each addressed somewhere in Results or Discussion.
- [ ] Delimitations chapter explicitly states what is out of scope.
- [ ] No new task threads or research directions are introduced that are not connected to any RQ.

---

## Phase 3 — Citation Audit

Run these checks per citation key:

- [ ] Every `\cite{key}` in `thesis.tex` has a corresponding entry in `tex/biblio.bib`.
- [ ] Every key in `tex/biblio.bib` has a corresponding row in `citation_ideas.csv`.
- [ ] Every row in `citation_ideas.csv` has a corresponding PDF at `ref/<key>.pdf`.
  (If PDF is missing: status = "PDF missing" — flag to user, do not mark as verified.)
- [ ] `Original_quote_or_core_statement` in `citation_ideas.csv` is not empty and contains extracted PDF text (not a paraphrase written from memory).
- [ ] `Inspiration_for_thesis` explains how the source connects to this thesis specifically.
- [ ] The claim in `thesis.tex` that uses the citation is consistent with the `Original_quote_or_core_statement` — no overclaiming.
- [ ] No BibTeX `note` field has been deleted or shortened from its original extracted quote.

**How to verify a suspicious citation:**
```bash
# OCR and extract text from the source PDF
ocrmypdf --skip-text ref/<key>.pdf /tmp/<key>.ocr.pdf
python3 -c "
import pdfplumber
with pdfplumber.open('/tmp/<key>.ocr.pdf') as pdf:
    for page in pdf.pages:
        print(page.extract_text())
" | grep -i "<keyword from claim>"
```

---

## Phase 4 — Terminology Sweep

- [ ] Open `requirements/terminology/field_terms.md` and extract all defined terms.
- [ ] For each term: check that the first occurrence in `thesis.tex` introduces it as "Full Term (ABBREV)".
- [ ] After first occurrence: only the fixed abbreviation or short form is used (no synonyms).
- [ ] No undefined abbreviation is used without a prior introduction.
- [ ] Check each chapter independently — a term introduced in Chapter 2 may be used without re-definition in Chapter 3, but must not be re-defined differently.
- [ ] Flag any term used in the paper that is not yet listed in `field_terms.md` — add it.

---

## Phase 5 — Style and Language

- [ ] **Tense rules:**
  - Background / literature review: simple present tense ("Smith (2021) shows...")
  - Completed experiments: simple past ("The model achieved...")
  - Section introductions / signposting: simple present ("This chapter describes...")

- [ ] **Tone:**
  - No exaggeration: flag "fully solves", "guarantees", "perfectly", "revolutionizes".
  - No unsupported conclusions: every claim of improvement must cite evidence or a table/figure.
  - Prefer `this thesis` / `this study` over "I" or "we".

- [ ] **Prose vs. bullets:**
  - Main text chapters use paragraph prose, not bullet lists.
  - Bullet lists are acceptable only in methodology enumerations or contribution lists.

- [ ] **AI artifact check:**
  - Flag templated phrases: "In conclusion, it can be seen that...", "It is worth noting that...", "This paper aims to...".
  - Flag over-structured paragraphs that read as bullet lists in disguise (every sentence starting with a transition word).

- [ ] **Results vs. Discussion language:**
  - Results: "X was Y" — no interpretation.
  - Discussion: interpretation is grounded in a cited mechanism or comparison to related work.

---

## Phase 6 — Placeholder Cleanup

- [ ] Search `thesis.tex` for all remaining `[To be completed]` markers.
  ```bash
  grep -n "\[To be completed\]" thesis.tex
  ```
- [ ] For each match: either fill the content or add a `todo.md` task if blocked.
- [ ] Check all `\ref{}` and `\cite{}` calls compile without `??` warnings (undefined labels).
- [ ] Check all table placeholders have their final header row (no column named `TBD` in headers).
- [ ] Check all figure placeholders have a real `\includegraphics{}` or a clearly marked `[Figure pending: description]` with a `todo.md` task.

---

## Phase 7 — File Integrity

- [ ] All file paths referenced in `AGENTS.md` resolve to existing files.
- [ ] `tex/biblio.bib` compiles without errors (`bibtex` or `biber` run cleanly).
- [ ] All keys in `tex/biblio.bib` appear at least once in `thesis.tex` (no orphan entries).
- [ ] `citation_ideas.csv` has no rows with an empty `BibTeX_key` column.
- [ ] `requirements/feedbackv1.md` (and later rounds): every "Status: pending" item has a corresponding open task in `todo.md`.
- [ ] `todo.md`: no completed task (`[x]`) still has a corresponding "Status: pending" in a feedback file.
- [ ] `.gitignore` is present and includes `ref/*.pdf` and `.venv/`.

---

## End-of-Review Summary Template

After all phases, produce:

```md
## Review Summary — YYYY-MM-DD

### Hard Veto Items
- [ ] All clear / [list remaining blockers]

### Issues Fixed This Round
- [Phase] [chapter/file]: [what was fixed]

### Issues Deferred to Next Round
- [Phase] [chapter/file]: [what was deferred and why]

### Open Placeholders
- thesis.tex line XX: [To be completed] in [section]

### Pending Citations (PDF missing)
- [BibTeX key]: PDF not yet in ref/
```

## Modification Log
- 2026-04-24: Initial checklist created from accumulated AGENTS.md + paper_guidelines.md rules. Phased methodology added to prevent context overflow on long documents.
