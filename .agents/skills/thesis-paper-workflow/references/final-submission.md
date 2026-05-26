# Final-Final Submission Workflow

Use this reference for final-submission readiness, the final-final checklist, numeric consistency, opposition/PPT/plagiarism follow-up, and post-review polish.

## Active Files

- Final checklist: `requirements/final_checklist.md`
- Number audit: `requirements/numbers_consistency.md` (create on first use)
- Reflection draft: `requirements/reflection.md` (create on first use)
- Modification history: `requirements/modification_summary.md`
- Official instructions: the institution-provided PDF (path recorded in `AGENTS.md` Section 0)

## Do Not Reopen Historical Work by Default

Treat the following as evidence archives unless reactivated by the user or by an active item in `requirements/final_checklist.md`:

- `requirements/feedback_v*/` — older supervisor/reviewer rounds.
- `requirements/review_round_*/` — older review rounds.
- `ppt/final/` and any archived defense decks.
- `reviewOthers/` and any peer-opposition evidence folders.
- Anything explicitly named `archive/`, `old/`, or marked `Status: superseded`.

## Final Quality Gate (in order)

1. **Instruction compliance** — Re-read the institution's formatting requirements PDF; walk `requirements/final_checklist.md` Phase 1–7.
2. **Tone and structure** — Tone is calm and evidence-driven; no unsupported absolute claims; Results observes, Discussion interprets, Conclusion synthesizes.
3. **Problem/RQ/Requirement chain** — Each RQ and each requirement has an answer or explicit status later in the thesis.
4. **Number audit** — Every value in the body matches `requirements/numbers_consistency.md`; no `MISMATCH` rows remain.
5. **Number completeness** — Each important number carries metric + split/protocol + unit.
6. **Mixed-status reporting** — Mixed results state clearly: achieved / partially achieved / not measured / future work.
7. **Abstract–Conclusion mirroring** — Abstract and Conclusion present the same method/result/limitation facts.
8. **Citation grounding** — For every `\cite{}`, the supporting `Original_quote_or_core_statement` in `citation_ideas.csv` actually grounds the sentence.
9. **Plagiarism / AI disclosure** — Run an originality check; declare AI assistance per institution policy and keep it consistent with `reflection.md`.
10. **Reflection** — If required, the reflection chapter exists in the right voice (see `reflection.md`).
11. **Opposition / defense prep** — Prepare a one-page contribution summary and a written list of known limitations *before* the meeting.

## Number-Change Rule

Before changing any quantitative result, table, figure, threshold, or claim involving metrics:

1. Search `thesis.tex` for **all** occurrences of the number (and its alternative formats — `83.2%` vs `83.2\%` vs `0.832`).
2. Open `requirements/numbers_consistency.md` and update the canonical row.
3. Keep metric, split/protocol, and unit consistent everywhere.
4. Update all appearances in a single editing pass; do not leave partial fixes between sessions.
5. Record the change in `requirements/modification_summary.md` if substantive.

## Numeric Consistency File Schema

`requirements/numbers_consistency.md` should track each canonical figure with at least:

| Field | Meaning |
|-------|---------|
| Value | Canonical figure (e.g., `83.2%`, `12.4 ms`) |
| Source | Experiment, table, or figure that produced it |
| Appearances | Every `thesis.tex` location citing the number |
| Status | `OK` / `MISMATCH` / `PENDING` |

## Reflection Placement

If the institution requires reflection at the end of the thesis, place it after the final appendix unless the official instructions say otherwise. Use:

```latex
\chapter*{Reflection}
\addcontentsline{toc}{chapter}{Reflection}
```

See `reflection.md` for content and voice rules.
