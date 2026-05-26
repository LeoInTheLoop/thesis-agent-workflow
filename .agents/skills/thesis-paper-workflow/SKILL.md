---
name: thesis-paper-workflow
description: Generic thesis workflow for drafting, revising, and submitting a long-form research thesis. Use when the user works on thesis prose, supervisor/reviewer/opposition comments, citation grounding, numeric consistency, reflection, the final-submission checklist, or any task involving tone, cross-chapter alignment, claims, results, discussion, conclusion, bibliography, or submission readiness.
---

# Thesis Paper Workflow

Use this skill to work on the thesis without re-loading every rule from scattered Markdown files. The detailed rules live in the focused reference files under `references/`; read only the ones the current task needs.

## First Decision

- For thesis prose edits (tone, chapter roles, claim/evidence/boundary, cross-chapter echo): read `references/paper-quality.md`.
- For citations, bibliography, literature claims, or source-PDF evidence: read `references/citation-evidence.md`.
- For final-submission checks, numeric consistency, plagiarism, opposition, or PPT follow-up: read `references/final-submission.md`.
- For reflection-chapter writing or AI-use wording: read `references/reflection.md`.
- For repository file roles and source-of-truth order: read `references/repo-map.md`.

When the task touches multiple areas, read only the relevant references. Do not load every reference by default.

## Always: New-File Triage

Whenever a new file appears — created this session, dropped in by the user, or produced by a tool — **before** reading or editing it as content, open `references/repo-map.md` and walk the **Canonical Folder Tree** + **New-File Routing Rule**. If the file is in the wrong location, ask the user once before moving it. This applies to every task type below.

## Core Workflow

1. Identify whether the request is paper prose, citation/evidence, final-submission, reflection, or file organization.
2. Read the relevant reference file(s) above.
3. Before editing `thesis.tex`, check thesis scope in `paper_theme.md` and terminology in `requirements/terminology/field_terms.md`.
4. Preserve the fixed contribution boundary recorded in `paper_theme.md`; adjacent capabilities and broader generalisation stay in limitations/future work unless new evidence is added.
5. After paper-content edits, sync with your remote editor (e.g., Overleaf) if applicable, using the project's sync script.
6. Update the active checklist or status file when the work completes.

## Editing Defaults

- Modify thesis content only in `thesis.tex` (the single authoritative LaTeX source) unless the user asks for support-file updates.
- Keep historical review, opposition, PPT, and old feedback folders as evidence archives; do not resurrect their tasks unless `requirements/final_checklist.md` or the user explicitly marks them active.
- Treat numeric results as evidence, not decoration: every important number needs a metric name, split/protocol, unit, and a role in answering an RQ or requirement.
- Use calm academic prose in the thesis body. Use natural first-person voice only in reflection-style text.

## Validation

- For prose: verify `claim → evidence → boundary` and chapter-role fit (Results observes, Discussion interprets, Conclusion synthesizes).
- For numbers: consult `requirements/numbers_consistency.md` (create it if missing — see `references/final-submission.md`).
- For citations: follow the PDF extraction and citation-triad workflow in `references/citation-evidence.md`.
- For final submission: update `requirements/final_checklist.md` and record the round in `requirements/modification_summary.md`.
