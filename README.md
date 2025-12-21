# Claude Agents & Skills

First agent: Advanced PubMed search that directly analyzes abstracts and metadata of articles from search results. 

## Prerequisites

1. Claude Pro or Team account
2. PubMed MCP server connected (Settings → Connections → PubMed) [(instructions: Claude.ai)](https://support.claude.com/en/articles/12614801-using-the-pubmed-connector-in-claude)

## How to Use

### Step 1: Download Files
- One skill file from `/skills/`
- One agent file from `/agents/`

### Step 2: Upload to Claude
Start a new conversation and upload both files.

### Step 3: Execute
- Command the agent to start with `Execute the uploaded agent and skill` on the first line.
- Then customize the agent runtime with parameters on subsequent lines. For example:
```
Execute the uploaded agent and skill
1. Change search period to last 6 months.
2. Return 15 articles.
3. Exclude review articles.
```

## Output

Claude generates a downloadable markdown report with article summaries, relevance assessments, and citations.

## Examples

See `/examples/` for sample outputs.

## Future Directions

Second agent: Citation analysis agent that looks up information about article references (for you!)

*Questions, comments? Contact James*
