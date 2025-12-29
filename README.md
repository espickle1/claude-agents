# Claude Agent Library for the Maresso Group

## Prerequisites

1. Claude Pro or Team account
2. PubMed MCP server connected (Settings → Connections → PubMed) [(instructions: Claude.ai)](https://support.claude.com/en/articles/12614801-using-the-pubmed-connector-in-claude)

## Repository Structure

```
claude-agents/
├── agents/
│   ├── literature-survey-agents/   # PubMed literature search workflows
│   │   └── verb/
│   └── reference-agents/           # Article reference analysis workflows
│       ├── subject/
│       ├── verb/
│       └── object/
├── examples/                       # Sample outputs
└── utils/                          # Helper scripts (Colab notebooks)
```

## How to Use

### Literature Survey Agents

Search and summarize recent literature from PubMed.

**Step 1: Download Files**
* One agent file from `/agents/literature-survey-agents/verb/`
* `VERB.pubmed-search-skill.md` from the same directory

**Step 2: Upload to Claude**

Start a new conversation and upload both files.

**Step 3: Execute**

* Command the agent to start with `Execute the uploaded agent and skill` on the first line.
  + I used Sonnet 4.5: Opus 4.5 used up tons more resources for imperceptible performance improvement.
* Then customize the agent runtime with parameters on subsequent lines. For example:

```
Execute the uploaded agent and skill
1. Change search period to last 6 months.
2. Return 15 articles.
3. Exclude review articles.
```

**Output:** Claude generates a downloadable markdown report with article summaries, relevance assessments, and citations.

---

### Reference Analysis Agents

Analyze how a journal article uses its references and extract key learnings.

**Step 1: Prepare Materials**
* Article text in markdown format
* Reference abstracts in markdown format (use `utils/reference_pubmed_id_extractor.ipynb` to generate)

**Step 2: Download Files**

From `/agents/reference-agents/`:
* `AGENT.read_references.md`
* One SUBJECT file from `/subject/` (e.g., `SUBJECT.analysis.md`)
* Both VERB files from `/verb/`
* One OBJECT.field file from `/object/` (or use the template to create your own)

**Step 3: Upload to Claude**

Start a new conversation and upload:
1. AGENT.read_references.md
2. Your chosen SUBJECT file
3. Both VERB files
4. OBJECT.field file
5. Your article markdown
6. Your abstracts markdown

**Step 4: Execute**

```
Execute AGENT.read_references.md
SUBJECT: analysis
VERB: read_references
OBJECT: field, article, abstracts
```

**Output:** Claude generates a structured digest with key learnings and references organized by function.

---

## Examples

See `/examples/` for sample outputs from both agent types.

## Utilities

See `/utils/` for helper scripts:
* `pdf_to_markdown_and_text.ipynb` — Convert PDFs to Claude-friendly markdown
* `reference_pubmed_id_extractor.ipynb` — Extract reference PMIDs and abstracts from PMC articles

## Future Directions

* ~~Literature survey agent~~ ✓
* ~~Reference analysis agent~~ ✓
* Add automatic (scheduled and conditional) agent execution feature

**Questions, comments? Contact James**
