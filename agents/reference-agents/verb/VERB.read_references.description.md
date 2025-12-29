---
type: verb
name: read_references
file: description
version: 1.1
created: 2024-12-29
last_modified: 2024-12-29
description: Settings, templates, and output specifications
---

# VERB.read_references.description.md

## Purpose

Process a journal article and its reference abstracts to produce a structured digest showing how the article uses its references and what key learnings emerge.

---

## Inputs

| Input | Description | Required |
|-------|-------------|----------|
| SUBJECT.*.md | Reader intent (one of six) | Yes |
| OBJECT.field.md | Field context | Yes |
| OBJECT.article.md | Journal article with citations | Yes |
| OBJECT.abstracts.md | Abstracts of cited references | Yes |

---

## Output

RESULT.references.Author.Year.md

---

## Output Length Specifications

| Element | Length |
|---------|--------|
| Connection description | One sentence per citation |
| Key Learnings (analysis) | 3-7 |
| Key Learnings (survey) | 3-7 |
| Key Learnings (retrieval) | As needed to answer query |
| Key Learnings (evaluate) | 1-3 per claim evaluated |
| Key Learnings (writing) | 3-7 |
| Key Learnings (discussion) | 5-7 |

---

## Purpose Codes

| Code | Purpose | Description |
|------|---------|-------------|
| (a) | Orientation | Introduces topic reader may not know; refreshes or guides memory |
| (b) | Positioning | Brings up point that article aims to support or refute |
| (c) | Methodological | Links to detailed procedures too extensive to include |
| (d) | Evidentiary | Reminds reader what has already been established |
| (e) | Extensional | Provides follow-up resources on related topics |

---

## Location Categories

| Category | Location | Description |
|----------|----------|-------------|
| A | Background | Early Introduction; field-level context |
| B | Prior Knowledge | Late Introduction; topic-specific prior work |
| C | Methods | Methods section; techniques, tools, protocols |
| D | Results | Results section; comparison, validation, contextualization |
| E | Discussion | Discussion section; interpretation, extension, contrast |

---

## Location × Purpose Patterns

| Location | Common purposes | Less common purposes |
|----------|-----------------|---------------------|
| A. Background | (a) orientation, (d) evidentiary | (e) extensional |
| B. Prior Knowledge | (a) orientation, (b) positioning, (d) evidentiary | (e) extensional |
| C. Methods | (c) methodological | (d) evidentiary |
| D. Results | (b) positioning, (d) evidentiary | (c) methodological |
| E. Discussion | (b) positioning, (d) evidentiary, (e) extensional | (a) orientation |

---

## Identifier Fallback Order

When building Reference Index, use first available:

1. PMCID → format: `PMCID: PMCxxxxxxx | https://www.ncbi.nlm.nih.gov/pmc/articles/PMCxxxxxxx`
2. PMID → format: `PMID: xxxxxxxx | https://pubmed.ncbi.nlm.nih.gov/xxxxxxxx`
3. DOI → format: `DOI: 10.xxxx/xxxxx | https://doi.org/10.xxxx/xxxxx`
4. Citation only → format: `Citation only | No indexed link available`

---

## Reference Index Construction Rules

**CRITICAL: Use only information present in OBJECT.abstracts.md.**

Each reference entry must contain:
- Reference number [#]
- Title (quoted, from OBJECT.abstracts.md)
- Journal and year (from OBJECT.abstracts.md)
- Identifier and link (per fallback order above)

**Do NOT include author names unless they are explicitly present in OBJECT.abstracts.md.** Do not infer, recall, or hallucinate author names from external knowledge.

---

## Retrievable Categories Menu

For SUBJECT.retrieval.md when Runtime Specification is blank:

```
Retrievable items identified in this article:
□ Experimental conditions (concentrations, durations, strains)
□ Quantitative findings (measurements, statistics, p-values)
□ Sequence/structural information (lengths, features, identifiers)
□ Methodological parameters (assay specifications, tools)
□ Strain/reagent identifiers (collection numbers, plasmid names)
```

---

## RESULT Template

```markdown
---
type: result
source_agent: read_references
paper: [First Author] et al. [Year]
title: [Full title of paper]
pmcid: [PMCxxxxxxx or "N/A"]
pmid: [xxxxxxxx or "N/A"]
doi: [10.xxxx/xxxxx]
date_read: [YYYY-MM-DD]
subject_used: [analysis|survey|retrieval|evaluate|writing|discussion]
---

## Key Learnings

- [Learning 1]
- [Learning 2]
- [Additional learnings per SUBJECT requirements]

---

## Reference Index

- [1] "[Title]" | Journal (Year) | [Identifier per fallback order] | [Link]
- [2] "[Title]" | Journal (Year) | [Identifier per fallback order] | [Link]
[... continues for all references]

---

## References by Function

### A. Background Information

General knowledge establishing the broader context for this work.

- [#] [Connection description]

### B. Prior Knowledge on Specific Subject

What was known about the narrow topic before this paper.

- [#] [Connection description]

### C. Methods

Techniques, protocols, analytical approaches, or tools used in this paper.

- [#] [Connection description]

### D. Results

References invoked to contextualize, compare, or validate findings.

- [#] [Connection description]

### E. Discussion

References used to interpret findings, address limitations, or suggest implications.

- [#] [Connection description]

---

## Unindexed References — MANUAL LOOKUP REQUIRED

References cited in OBJECT.article.md but absent from OBJECT.abstracts.md.

- [#] [Citation as appears in article] — Reason: [Why unavailable]
```

---

## Internal Inconsistency Flag Format

```
[Internal inconsistency: Article states X; abstract indicates Y]
```

---

## Empty Section Handling

If a category (A-E) has no entries:

```
- None identified
```
