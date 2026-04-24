# Agent Guidelines (Paper Workflow Entry Point)

## -1. First-Time Initialization (Run Once for New Users)
% Reason: Give the agent a concrete checklist to run when a new user says "initialize" or "set up my thesis workspace", so setup is guided interactively rather than manually.

When the user says anything like **"initialize"**, **"set up my workspace"**, or **"I just cloned this"**, run through the following steps in order. Ask one question at a time — do not dump a list of questions at once.

### Step A — Check required tools
Check whether the following are available in the current shell. Report what is missing and ask the user before installing anything:
- `git` — for version control
- `python3` — for the citation PDF pipeline
- `ocrmypdf` and `pdfplumber` — Python PDF tools (install into `.venv`, see §3.2)
- A LaTeX compiler (`pdflatex` or `xelatex`) — for compiling `thesis.tex`

If tools are missing, tell the user which ones and ask: _"Do you want me to set up the Python environment now?"_

### Step B — Identify the thesis file
Ask the user:
> "Do you already have a `.tex` file for your thesis, or should I help you start from the template in `thesis.tex`?"

- If they have one: ask where it is and copy or link it into the project root.
- If they don't: point them to `thesis.tex` and explain the `[To be completed]` placeholder convention.

### Step C — Identify source PDFs
Ask the user:
> "Do you have any reference PDFs already? If so, tell me the paper title or BibTeX key and I'll help you rename them to `ref/<BibTeX key>.pdf`."

- For each PDF: create or update the corresponding row in `citation_ideas.csv` and the entry in `tex/biblio.bib`.
- Remind the user that PDFs are gitignored (copyright) — they stay local only.

### Step D — Fill in the research topic
Ask the user to describe their thesis in a few sentences, then help them fill in `paper_theme.md`:
- Thesis title
- One-sentence summary
- Main RQ and Sub-RQs
- Key contributions
- Scope / delimitations

### Step E — Set up terminology
Ask: _"What field is your thesis in? I'll pre-fill a few starter terms in `requirements/terminology/field_terms.md`."_

### Step F — Confirm official instructions
Ask: _"Does your institution have a PDF with thesis formatting requirements? If so, drop it in the project root and tell me the filename — I'll update the reference in AGENTS.md."_

### Step G — First commit
After steps A–F are done, offer to run:
```bash
git init
git add .
git commit -m "init: thesis workspace from template"
```

% Reason: End initialization with a clean first commit so the user's git history starts after setup, not mid-configuration.

---

## 0. Document Roles (Single Source of Truth)
% Reason: Lock a single authoritative entry file and supporting-document map so later edits do not create conflicting workflow sources.
- Workflow entry: `AGENTS.md`
- Writing guidelines: `requirements/paper_guidelines.md`
- Paper main theme: `paper_theme.md`
- Terminology: `requirements/terminology/field_terms.md`
- Citation planning: `citation_ideas.csv`
- Task checklist: `todo.md`
- Official instructions: `[your-institution-instructions].pdf`
- Official BibTeX: `tex/biblio.bib`
- Final review checklist: `requirements/final_checklist.md`
% Reason: Align workflow paths with actual repository directory names so agents do not search missing paths.

## 1. Fixed Order Before Modifying Paper Content
% Reason: Force a stable pre-read sequence so paper edits stay aligned with thesis scope, terminology, citation intent, and open tasks.
1. Read `paper_theme.md` to ensure changes align with main theme.
2. Read `requirements/terminology/field_terms.md` to lock terminology.
3. Read `citation_ideas.csv` to confirm claim-citation pairing.
4. Read corresponding task in `todo.md` to avoid duplicate work.

## 2. Paper Modification Boundaries
- Modify paper content only in `thesis.tex` (or your main LaTeX/Word file).
- After modifications, sync your file with Overleaf if applicable.

## 3. Citation Change Triad (Must Complete Simultaneously)
% Reason: Force bibliography, citation-planning notes, and local source PDFs to change together so claim-citation evidence does not drift across files.
- Update `tex/biblio.bib`.
- Update `citation_ideas.csv` (specify: why cite, where to place, original quote).
- New PDF files in `ref/` must use BibTeX key as filename.
- Each time you add or modify an entry in `citation_ideas.csv`, open the corresponding PDF in `ref/` to verify against original text.
- If `citation_ideas.csv` contains a key but no corresponding PDF in `ref/`, first obtain the PDF before modifying citation ideas.

### 3.1 Citation Verification Process (Fixed)
% Reason: Require direct source-text verification before claim placement so citation notes stay grounded in the actual PDF wording.
1. Locate BibTeX key in `citation_ideas.csv`.
2. Open `ref/<BibTeX key>.pdf` to verify original sentences.
3. Fill or modify `Original_quote_or_core_statement` and `Inspiration_for_thesis`.
4. Finally verify consistency among "claim – original text – placement location".

### 3.2 Citation Text Extraction Pipeline (Mandatory: `OCRmyPDF` + `pdfplumber`)
% Reason: Reduce citation misquote risk by enforcing machine-extracted evidence before writing claim-citation mapping.
% Reason: Make PDF extraction robust across machines by requiring a tool self-check first and avoiding silent fallback to weaker ad hoc extraction.
0. Before extracting text, self-check whether `ocrmypdf`, `pdfplumber`, and optionally `pdftotext` are available in the current environment.
1. If the required PDF tools are missing, ask the user one short question before installation: `Required PDF extraction tools are missing. Do you want me to install them in the project .venv first?`
2. Prefer installing Python-side PDF tools into the project `.venv` rather than the global Python environment when feasible.
% Reason: Make the environment choice explicit before any future tool installation so agents do not drift back to global Python and create machine-specific dependency state.
2.1. If the project does not yet contain a `.venv`, create a project-local `.venv` first and then install Python-side tooling into that environment.
3. `pdftotext` may be used as a quick helper when already available, but it does not replace the mandatory `OCRmyPDF` + `pdfplumber` verification workflow for citation-grounding tasks.
% Reason: When the user names a source PDF directly, the workflow must still force a text-first verification step before trusting any remembered or handwritten citation note.
3.1. If the user says a claim, quote, or citation idea comes from a specific PDF, first generate a corresponding `.txt` extraction for that PDF, then verify whether the original wording actually supports the statement before editing `citation_ideas.csv` or `thesis.tex`.
3.2. For files in `ref/`, name the extracted text file with the same BibTeX key, preferably as `/tmp/<BibTeX key>.txt` or `/tmp/<BibTeX key>.ocr.txt`, so the mapping between PDF, text evidence, and CSV row remains unambiguous.
3.3. If the extracted text does not clearly support the user-provided wording, do not copy the wording into `citation_ideas.csv` as-is; instead, revise it to match the source text or flag the mismatch explicitly.
4. Before editing citation rows, run OCR preprocessing for the corresponding file in `ref/`:
   - `ocrmypdf --skip-text ref/<BibTeX key>.pdf /tmp/<BibTeX key>.ocr.pdf`
5. Extract text using `pdfplumber` from the OCR-processed file (or original PDF if already searchable).
6. Locate the exact sentence(s) supporting the claim, then paste key evidence into `Original_quote_or_core_statement`.
7. Update `Inspiration_for_thesis` with a concise thesis-specific interpretation of the extracted sentence.
8. If extracted text cannot support the existing claim, revise claim placement or change citation before modifying `thesis.tex`.
9. Only after steps 4–8 are complete, finalize the `citation_ideas.csv` edit.

## 4. File Management Rules
% Reason: Prevent duplicate rule files and version drift that would otherwise create multiple conflicting "latest" documents.
- Keep only one main file per category; merge historical versions into `requirements/modification_summary.md`.
- Delete duplicate files (same content copies) to avoid "dual version truth".
- Historical feedback files (e.g., `feedback_v1.md`, `feedback_v1.1.md`) may be retained for item-by-item completion tracking.

## 5. Revision Implementation Process (Item-by-Item)
% Reason: Make reviewer-comment handling traceable item by item so each external comment can be mapped to a concrete thesis change and status.
When handling supervisor/reviewer "revision comments", follow this format:

1. Retain original comments in the corresponding feedback file without deletion.
2. Add "Corresponding Changes" section below original comments, specifying:
   - Action (rewrite/add/delete/rearrange)
   - Location (file + chapter/section)
   - Evidence (modified key sentences or line numbers)
   - Status (completed/pending)
3. If one comment requires multiple actions, number them (1.1 / 1.2 / 1.3).
4. Synchronously update `todo.md`: convert pending actions to checkable tasks.
5. If citation changes are involved, simultaneously execute "citation change triad".

Suggested template:

```md
### Original Comment
<Paste original comment>

### Corresponding Changes
- Action: <rewrite/add/delete/rearrange>
- Location: <filename + chapter>
- Modified content: <key modified sentences>
- Status: <completed/pending>
```

## 6. Modification Log Requirements (for .md rule files)
Append to the bottom of modified `.md` files:

```md
## Modification Log
- YYYY-MM-DD: Modification highlights + implementation method (e.g., structure rewrite, terminology standardization, citation deduplication, file merging).
```

## 7. `%` Change Annotation Rule (Mandatory)
% Reason: Preserve rationale history alongside rule edits so later revisions can extend prior intent instead of silently replacing it.
- Each newly modified rule point must include a `%` note nearby to explain *why* the change is made.
- Recommended format:

```md
% Reason: <why this change is needed; what risk or confusion it prevents>
```

- Place the `% Reason` line immediately below the modified rule (or in the closest adjacent line) so later editors can trace intent quickly.
- Before any future edit, first check all related `% Reason` notes to ensure the new change does not break existing rules or previous design intent.
- If a new change supersedes an old `% Reason`, keep both notes and mark the old one as superseded instead of deleting history.
- Old `% Reason` notes may only be appended to, never deleted, replaced, or overwritten.
% Reason: Make rationale preservation explicit so editors do not collapse multiple revision intents into one rewritten `% Reason` and lose traceability.

## 8. Writing Style + Prewrite Framework Mode (Mandatory)
% Reason: Lock a single drafting style so thesis sections can be filled quickly without switching between TODO notes and prose, reducing structure drift across chapters.
- Use thesis-style prose first, not checklist-style TODO bullets, when drafting `thesis.tex`.
- Draft with complete academic sentences and inline placeholders, e.g., `[To be completed]`, so later edits are fill-in replacements rather than rewrites.
- Keep contribution emphasis consistent with your research questions (adapt to your own topic).

% Reason: Ensure missing figures/tables do not block writing flow and that every placeholder has a stable insertion point for later replacement.
- When a section needs a table or figure, insert real LaTeX `table`/`figure` environments immediately (with caption + label + placeholder body), instead of writing only "Figure/Table to be added".
- In prose, always reference placeholders using `Table~\ref{...}` / `Figure~\ref{...}`.
- Table placeholders must include final header structure and at least one `TBD` row.
- Figure placeholders should use a visible boxed placeholder text describing what will be inserted.

% Reason: Keep narrative and evidence aligned with research questions and avoid overclaiming before final numbers are filled.
- In Results/Discussion/Conclusion drafts, write claim-shaped sentences with placeholders (e.g., "The results show [To be completed]"), and avoid absolute wording like "fully solve" or "guarantee".
- If a metric is not yet finalized, keep the sentence but mark only the value fragment as `[To be completed]`.
- Do not leave isolated TODO bullets in thesis chapters unless the content is strictly workflow metadata outside the main text.

## Modification Log
- YYYY-MM-DD: Initial template created. Adapt file paths and writing guidelines to your own project.
