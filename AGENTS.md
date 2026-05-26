# Agent Guidelines (Paper Workflow Entry Point)

## 0. Primary Workflow
- Main repo entry: `AGENTS.md` (this file — routing + hard boundaries only).
- Agent Skill entry: `.agents/skills/thesis-paper-workflow/SKILL.md`
% Reason: The detailed thesis workflow lives in an Agent Skills compatible layout; this file stays a thin routing + hard-boundary entry instead of duplicating every rule.

For thesis writing, review, citation, numeric consistency, final-submission, or reflection tasks, first use/read the skill and only load the relevant reference:
- `.agents/skills/thesis-paper-workflow/references/repo-map.md` — file roles + folder tree + **new-file routing rule**
- `.agents/skills/thesis-paper-workflow/references/paper-quality.md` — tone, chapter roles, claim/evidence/boundary
- `.agents/skills/thesis-paper-workflow/references/citation-evidence.md` — citation triad + PDF extraction pipeline
- `.agents/skills/thesis-paper-workflow/references/final-submission.md` — final-final checklist + numeric audit
- `.agents/skills/thesis-paper-workflow/references/reflection.md` — reflection chapter + AI disclosure
% Reason: Progressive disclosure keeps context small while preserving the detailed rules.

## 0.5. New-File Routing (Always-On)
% Reason: New files tend to land at the repo root by default; left uncorrected, the project accumulates duplicate-truth files that silently diverge.

Whenever a new file appears — created in this session, dropped in by the user, or produced by a tool — **before** reading or editing it as content:

1. Open `.agents/skills/thesis-paper-workflow/references/repo-map.md`.
2. Walk the **Canonical Folder Tree** + **New-File Routing Rule** (incl. the File-Type Routing Table).
3. If the file is already in the right place, proceed.
4. If the file is in the wrong place, ask the user once before moving:
   > "I found `<path>`. By the folder tree it belongs in `<expected path>` — should I move it?"
5. If the file type is not in the routing table, add a new row (with a `% Reason`) before placing the file, so future agents inherit the decision.

## 1. First-Time Initialization (Run Once for New Users)
% Reason: Give the agent a concrete checklist to run when a new user says "initialize" or "set up my thesis workspace", so setup is guided interactively rather than left to the user.

When the user says anything like **"initialize"**, **"set up my workspace"**, or **"I just cloned this"**, run the steps below in order. Ask one question at a time — do not dump a list of questions at once.

### Step A — Check required tools
Check whether the following are available in the current shell. Report what is missing and ask before installing:
- `git`
- `python3`
- `ocrmypdf` and `pdfplumber` (install into project `.venv`; see `references/citation-evidence.md`)
- A LaTeX compiler (`pdflatex` or `xelatex`)

If tools are missing: _"Do you want me to set up the Python environment now?"_

### Step B — Identify the thesis file
> "Do you already have a `.tex` file for your thesis, or should I help you start from the template in `thesis.tex`?"

- If they have one: copy or link it into the project root as `thesis.tex`.
- If they don't: point them to `thesis.tex` and explain the `[To be completed]` placeholder convention.

### Step C — Identify source PDFs
> "Do you have any reference PDFs already? Tell me the paper title or BibTeX key and I'll help you rename them to `ref/<BibTeX key>.pdf`."

For each PDF: add or update the row in `citation_ideas.csv` and the entry in `tex/biblio.bib`. Remind the user that `ref/*.pdf` is gitignored (copyright).

### Step D — Fill in the research topic
Help the user fill in `paper_theme.md`: title, one-sentence summary, main RQ + Sub-RQs, key contributions, scope/delimitations.

### Step E — Set up terminology
> "What field is your thesis in? I'll pre-fill starter terms in `requirements/terminology/field_terms.md`."

### Step F — Confirm official instructions
> "Does your institution have a thesis formatting requirements PDF? If so, drop it in the project root and tell me the filename — I'll record the path in this file's §2 sources-of-truth list."

### Step G — First commit
After A–F are done, offer:
```bash
git init
git add .
git commit -m "init: thesis workspace from template"
```
% Reason: End initialization with a clean first commit so the user's git history starts after setup, not mid-configuration.

## 2. Active Sources of Truth
- Thesis source: `thesis.tex`
- Main theme / RQ boundary: `paper_theme.md`
- Terminology: `requirements/terminology/field_terms.md`
- Writing guidelines: `requirements/paper_guidelines.md`
- Citation plan: `citation_ideas.csv`
- Bibliography: `tex/biblio.bib`
- Source PDFs: `ref/<BibTeX key>.pdf` (gitignored)
- Final-review checklist: `requirements/final_checklist.md`
- Numeric audit: `requirements/numbers_consistency.md` (create on first numeric audit)
- Reflection draft: `requirements/reflection.md` (create when reflection chapter starts)
- Modification history: `requirements/modification_summary.md`
- Open tasks: `todo.md`
- Official instructions: `[your-institution-instructions].pdf` (record exact filename here)
% Reason: These are the canonical files. Anything else with overlapping content is either historical evidence or a mistake — route it via §0.5.

## 3. Hard Boundaries
- Modify thesis content only in `thesis.tex`. After paper-content edits, sync with your remote editor (e.g., Overleaf) via the project's sync script, never edit two copies in parallel.
% Reason: Split local-vs-remote files become a second source of truth and silently diverge.
- Before changing thesis prose, check `paper_theme.md` and `requirements/terminology/field_terms.md`.
% Reason: Preserve the fixed RQ scope and terminology after late-stage edits.
- Before changing citation claims, bibliography entries, or `citation_ideas.csv` rows, follow `references/citation-evidence.md`.
% Reason: Citation edits require BibTeX, citation-plan CSV, and source-PDF evidence to stay synchronized.
- Before changing metrics, thresholds, tables, figures, or numeric claims, consult `references/final-submission.md` and `requirements/numbers_consistency.md`.
% Reason: Late-stage metric drift between Abstract/Results/Discussion/Conclusion is the highest-risk final-submission failure mode.
- Treat versioned or archive-named folders (`requirements/feedback_v*/`, `requirements/review_round_*/`, `ppt/final/`, `reviewOthers/`, anything labelled `archive/`, `old/`, or `Status: superseded`) as historical evidence; do not resurrect tasks from them unless `requirements/final_checklist.md` or the user explicitly marks the item active.
% Reason: After multiple review rounds, old folders contain completed or intentionally excluded work; this boundary prevents duplicate or rejected work from returning.

## 4. Thesis Quality Boundary
- Keep the thesis contribution bounded to what `paper_theme.md` declares. Adjacent capabilities, broader generalisation, and downstream applications stay as limitations/future work unless new evidence is added.
- Use calm, evidence-led academic prose: `claim → evidence → boundary` in every paragraph that makes a claim.
- Keep Results, Discussion, and Conclusion roles distinct (Results observes; Discussion interprets; Conclusion synthesizes — no new numbers, no new citations).
- Report mixed results plainly: achieved / partially achieved / not measured / future work.
- Reflection chapters may use first-person; the body stays third-person academic. Do not let reflection voice bleed into the body.
% Reason: These are the recurring lessons from final review, opposition, number-audit, plagiarism, and reflection edits. Detailed rules live in `references/paper-quality.md`.

## 5. Rule-File Edit Protocol
- If this file or other rule `.md` files are modified, append a dated Modification Log entry.
- Newly modified rule points should include a nearby `% Reason` note explaining *why* the rule exists.
- Do not delete old `% Reason` rationale; append or supersede it instead.
- Before editing a rule, first check all nearby `% Reason` notes so the new change does not silently override prior intent.
% Reason: Preserve rationale history so future agents understand whether a rule is active workflow, historical evidence, or a superseded constraint.

## Modification Log
- YYYY-MM-DD: Initial template created. Adapt file paths and writing guidelines to your own project.
- 2026-05-27: Consolidated the detailed workflow into an Agent Skills compatible layout under `.agents/skills/thesis-paper-workflow/`; slimmed `AGENTS.md` to routing, sources of truth, hard boundaries, thesis-quality boundary, and rule-edit protocol; added §0.5 always-on New-File Routing rule backed by the Canonical Folder Tree + File-Type Routing Table in `references/repo-map.md`. Implemented by mirroring the downstream thesis project that already migrated to SKILL.md-based progressive disclosure.
