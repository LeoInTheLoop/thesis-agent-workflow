# Thesis Complete Workflow

> One repository. Everything your AI agent needs to help you write a thesis — without losing track, repeating itself, or overloading on context.

---

## Why This Exists

Writing a thesis with AI assistance usually breaks down in one of these ways:

- You paste context into every new chat and the AI forgets what it said last session
- Citations drift — the AI paraphrases a source it never actually read
- Supervisor feedback gets scattered across emails, docs, and chat logs
- Terminology is inconsistent between chapters because nothing enforces it
- You lose track of what's done, what's pending, and what's blocked on a PDF

This template fixes all of that in one repo:

| Problem | What this workflow provides |
|--------|----------------------------|
| AI loses context between sessions | `AGENTS.md` — single entry point the agent reads every time |
| Citation misquotes | PDF → OCR → extract → verify pipeline before any claim is written |
| Feedback gets lost | `requirements/feedbackv1.md` — supervisor comments tracked item by item |
| Inconsistent terminology | `requirements/terminology/field_terms.md` — agent checks this before every edit |
| Scattered writing rules | `requirements/paper_guidelines.md` — style, structure, evidence rules in one file |
| No version history | Git-first: every draft, revision round, and submission is a tagged commit |
| Overleaf + local out of sync | `thesis.tex` lives in the repo; sync with Overleaf manually or via script |

Everything the AI needs is here. You don't brief it from scratch each session — it reads the files.

---

## Before You Start

Install three things — that's all you need to do manually:

| Tool | Why | Install |
|------|-----|---------|
| [Git](https://git-scm.com) | Version control for your thesis | `brew install git` / [git-scm.com](https://git-scm.com) |
| [Python 3](https://www.python.org) | Citation PDF extraction pipeline | `brew install python3` / [python.org](https://www.python.org) |
| [VSCode](https://code.visualstudio.com) | Editor + Claude Code terminal | [code.visualstudio.com](https://code.visualstudio.com) |

LaTeX and Python libraries will be set up by the AI during initialization.

---

## Get Started (3 steps)

**1. Clone this template**

```bash
git clone https://github.com/your-username/your-thesis-repo.git
cd your-thesis-repo
```

**2. Open in VSCode and start Claude Code**

```bash
code .
claude
```

**3. Say this to the agent:**

```
Initialize my thesis workspace.
```

The agent reads `AGENTS.md` and guides you through the rest — checking your tools,
setting up your thesis file, adding your reference PDFs, and filling in your research topic.
It asks one question at a time.

---

## What the Agent Will Ask You

After you say "initialize", expect questions like:

- _"Do you already have a `.tex` file, or should I start from the template?"_
- _"Do you have any reference PDFs? Tell me the paper title and I'll rename and register them."_
- _"Describe your thesis in a few sentences — I'll help you fill in `paper_theme.md`."_
- _"What field is your thesis in? I'll pre-fill some starter terms."_
- _"Does your institution have a formatting requirements PDF?"_

Once that's done, the agent commits the initial setup and you're ready to write.

---

## Recommended VSCode Extensions

Install with one command:

```bash
code --install-extension James-Yu.latex-workshop \
     --install-extension eamodio.gitlens \
     --install-extension GitHub.vscode-pull-request-github \
     --install-extension streetsidesoftware.code-spell-checker \
     --install-extension janisdd.vscode-edit-csv \
     --install-extension yzhang.markdown-all-in-one
```

| Extension | Purpose |
|-----------|---------|
| LaTeX Workshop | Compile and preview `.tex` files |
| GitLens | Line-by-line git history |
| GitHub Pull Requests | Manage PRs from inside VSCode |
| Code Spell Checker | Catch typos in `.tex` and `.md` |
| CSV Editor | Edit `citation_ideas.csv` as a table |
| Markdown All in One | Preview workflow `.md` files |

---

## File Structure (after initialization)

```
your-thesis-repo/
├── AGENTS.md                    ← AI workflow rules (the agent reads this)
├── thesis.tex                   ← your main LaTeX file
├── paper_theme.md               ← research topic, RQs, contributions
├── citation_ideas.csv           ← citation planning + verification log
├── todo.md                      ← task checklist
├── ref/                         ← source PDFs (gitignored — stay local)
│   └── Smith2021.pdf
├── tex/
│   └── biblio.bib               ← BibTeX bibliography
└── requirements/
    ├── paper_guidelines.md      ← writing rules
    ├── feedbackv1.md            ← supervisor feedback + your responses
    ├── modification_summary.md  ← history of major changes
    └── terminology/
        └── field_terms.md       ← canonical term list for your field
```

---

## Using GitHub to Track Progress

```bash
# After each writing session
git add thesis.tex
git commit -m "draft: Chapter 2 related work"
git push

# New branch for each revision round
git checkout -b revision-v2
```

Tag versions before submission:
```bash
git tag submission-final
git push --tags
```

---

## License

MIT — free to use, adapt, and share.
