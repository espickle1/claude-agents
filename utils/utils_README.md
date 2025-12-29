## Utility Scripts

Helper notebooks for preparing inputs for Claude agents. All notebooks run in Google Colab.

---

### pdf_to_markdown_and_text.ipynb

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/espickle1/claude-agents/blob/main/utils/pdf_to_markdown_and_text.ipynb)

Convert PDF files to Claude-friendly text formats.

**Input:** PDF file (uploaded via Colab interface)\
**Output:**
* `article_markdown.md` — Clean text optimized for Claude processing
* `article_human.txt` — Formatted with page numbers for human reference

**Use case:** Prepare journal article PDFs for the reference analysis agent.

---

### reference_pubmed_id_extractor.ipynb

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/espickle1/claude-agents/blob/main/utils/reference_pubmed_id_extractor.ipynb)

Extract reference PMIDs and abstracts from PubMed Central articles.

**Input:** PMC ID (e.g., `PMC11152113`)\
**Output:**
* `pmids_PMCxxxxxxx.md` — List of reference PMIDs with links
* `abstracts_PMCxxxxxxx.md` — Reference abstracts formatted for Claude digest

**Use case:** Generate the `OBJECT.abstracts.md` input file for the reference analysis agent.

---

## Workflow

For reference analysis, run these utilities in order:

1. **pdf_to_markdown_and_text.ipynb** → produces article markdown
2. **reference_pubmed_id_extractor.ipynb** → produces abstracts markdown
3. Upload both outputs to Claude with the reference analysis agent files
