# ref/ — Source PDFs

This folder holds the source PDFs for every reference in `tex/biblio.bib`.

## Naming Rule

**Filename = BibTeX key**

```
ref/
├── LeCun2015.pdf
├── Goodfellow2016.pdf
└── He2016.pdf
```

If the BibTeX key is `Smith2021`, the file must be `ref/Smith2021.pdf`.  
This is required by the citation verification pipeline in `AGENTS.md` Section 3.

## Why PDFs Are Not Committed to Git

Research papers are usually copyrighted. Committing them to a public repository
may violate the publisher's terms of use.

**Recommended approach:**
- Keep PDFs locally in this folder (they are listed in `.gitignore`)
- Store the download link or DOI in the BibTeX `url` or `doi` field
- A collaborator can re-download each PDF using the key and DOI

## Checklist Before Adding a New Citation

- [ ] PDF downloaded and renamed to `<BibTeX key>.pdf`
- [ ] Entry added to `tex/biblio.bib` with readable key
- [ ] Row added to `citation_ideas.csv` with claim + placement
- [ ] Quote verified via `ocrmypdf` + `pdfplumber` (see AGENTS.md §3.2)
