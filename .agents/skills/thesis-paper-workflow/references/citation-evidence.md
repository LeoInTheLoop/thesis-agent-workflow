# Citation and Evidence Workflow

Use this reference for citation edits, bibliography changes, literature claims, or PDF-backed evidence.

## Citation Triad

When adding or changing a citation, update all three together:

1. `tex/biblio.bib` — the BibTeX entry.
2. `citation_ideas.csv` — claim, original quote, placement, inspiration.
3. `ref/<BibTeX key>.pdf` — the source PDF, named with the BibTeX key.

If `citation_ideas.csv` contains a key but no corresponding PDF in `ref/`, obtain the PDF before changing the citation. Do not paraphrase from memory or from a secondary source when the primary PDF is available.

## Fixed Verification Process

1. Locate the BibTeX key in `citation_ideas.csv`.
2. Open or extract `ref/<BibTeX key>.pdf`.
3. Verify the original sentence(s) supporting the thesis claim.
4. Update `Original_quote_or_core_statement` with the verified extract.
5. Update `Inspiration_for_thesis` with a thesis-specific interpretation.
6. Check consistency among claim, original text, and placement location in `thesis.tex`.

Never update citation ideas from memory or from a secondary paraphrase when the PDF is available.

## Mandatory PDF Extraction Pipeline

Before citation-grounding edits, check tools:

```bash
ocrmypdf --version
.venv/bin/python -c "import pdfplumber"
pdftotext -v   # optional helper
```

If the project does not yet contain a `.venv`, create a project-local virtual environment **before** installing Python tooling. Ask the user one short question before installing anything globally:

> "Required PDF extraction tools are missing. Do you want me to install them in the project `.venv` first?"

If `pdfplumber` is missing, install it inside the project `.venv`:

```bash
.venv/bin/pip install pdfplumber
```

Run OCR preprocessing (idempotent):

```bash
ocrmypdf --skip-text ref/<BibTeX key>.pdf /tmp/<BibTeX key>.ocr.pdf
```

Extract text with `.venv/bin/python` and `pdfplumber` from the OCR output or the original searchable PDF. Save the extracted text with the matching key, e.g. `/tmp/<BibTeX key>.ocr.txt`, so the mapping between PDF, evidence text, and CSV row remains unambiguous.

`pdftotext` may be used as a quick helper when already available, but it does not replace the mandatory `OCRmyPDF` + `pdfplumber` workflow for citation grounding.

## User-Provided Wording Verification

If the user says a claim, quote, or citation idea comes from a specific PDF:

1. First generate the corresponding `.txt` extraction for that PDF.
2. Then verify whether the original wording actually supports the statement before editing `citation_ideas.csv` or `thesis.tex`.
3. If the extracted text does not clearly support the user-provided wording, do not copy the wording into `citation_ideas.csv` as-is. Either revise it to match the source text or flag the mismatch explicitly.

## Claim–Citation Boundary

- Do not move a citation to a sentence it does not support.
- Do not stack many citations when one to three precise sources cover the claim.
- Keep BibTeX keys readable (e.g., `AuthorYear` or `AuthorYearKeyword`); never `ref1`, `paper`, or `cite1`.
- Preserve original-quote notes in BibTeX `note` fields or in `citation_ideas.csv` unless intentionally superseded — do not silently shorten them.
- If extracted text does not support the desired claim, revise the claim or choose a better citation **before** editing thesis prose.
