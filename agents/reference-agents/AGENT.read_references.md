---
type: agent
name: read_references
version: 1.0
created: 2024-12-29
description: Workflow for processing journal articles and reference abstracts
components:
  verb:
    - VERB.read_references.action.md
    - VERB.read_references.description.md
  subject:
    - SUBJECT.analysis.md
    - SUBJECT.survey.md
    - SUBJECT.retrieval.md
    - SUBJECT.evaluate.md
    - SUBJECT.writing.md
    - SUBJECT.discussion.md
  object:
    - OBJECT.field.md
    - OBJECT.article.md
    - OBJECT.abstracts.md
output: RESULT.references.Author.Year.md
---

# AGENT.read_references.md — Master Workflow Guide

## Overview

This workflow processes a journal article and its reference abstracts to produce a structured digest showing how the article uses its references and what key learnings emerge.

**Linguistic paradigm:** SUBJECT + VERB + OBJECT → RESULT

---

## Architecture Diagram

```
┌─────────────────────────────────────────────────────────────────────┐
│                            SUBJECT                                  │
│                       (reader intent)                               │
│                        Select ONE:                                  │
├─────────────────────────────────────────────────────────────────────┤
│  SUBJECT.analysis.md      Deep mechanistic understanding           │
│  SUBJECT.survey.md        Broad landscape mapping                   │
│  SUBJECT.retrieval.md     Extract specific information              │
│  SUBJECT.evaluate.md      Assess support/refutation                 │
│  SUBJECT.writing.md       Inform own writing                        │
│  SUBJECT.discussion.md    Comprehensive for peer discussion         │
└─────────────────────────────────────────────────────────────────────┘
                                   │
                                   ▼
┌─────────────────────────────────────────────────────────────────────┐
│                             VERB                                    │
│                   (processing instructions)                         │
├─────────────────────────────────────────────────────────────────────┤
│  VERB.read_references.action.md       Procedures and logic          │
│  VERB.read_references.description.md  Settings and templates        │
└─────────────────────────────────────────────────────────────────────┘
                                   │
                                   ▼
┌─────────────────────────────────────────────────────────────────────┐
│                            OBJECT                                   │
│                    (materials acted upon)                           │
├─────────────────────────────────────────────────────────────────────┤
│  OBJECT.field.md          Field context (reusable per domain)       │
│  OBJECT.article.md        Journal article with citations            │
│  OBJECT.abstracts.md      Reference abstracts                       │
└─────────────────────────────────────────────────────────────────────┘
                                   │
                                   ▼
┌─────────────────────────────────────────────────────────────────────┐
│                            RESULT                                   │
│                        (output produced)                            │
├─────────────────────────────────────────────────────────────────────┤
│  RESULT.references.Author.Year.md                                   │
└─────────────────────────────────────────────────────────────────────┘
```

---

## File Inventory

### SUBJECT Files (select one per article)

| File | Intent | Use when you want to... |
|------|--------|-------------------------|
| SUBJECT.analysis.md | Deep mechanistic understanding | Understand how something works in detail |
| SUBJECT.survey.md | Broad landscape mapping | Map concepts, methods, and connections across the field |
| SUBJECT.retrieval.md | Extract specific information | Find concrete values, parameters, or data points |
| SUBJECT.evaluate.md | Assess support/refutation | Evaluate evidence for or against a claim |
| SUBJECT.writing.md | Inform own writing | Learn argument structure and rhetorical patterns |
| SUBJECT.discussion.md | Comprehensive understanding | Prepare for peer discussion with full coverage |

### VERB Files (both required)

| File | Type | Contains |
|------|------|----------|
| VERB.read_references.action.md | Procedure | Execution sequence, logic rules, integration instructions |
| VERB.read_references.description.md | Configuration | Purpose codes, category definitions, templates, formats |

### OBJECT Files (all three required)

| File | Type | Preparation |
|------|------|-------------|
| OBJECT.field.md | Field context | Select pre-drafted template or create for new field |
| OBJECT.article.md | Article text | Rename uploaded article markdown |
| OBJECT.abstracts.md | Reference abstracts | Rename uploaded abstracts markdown |

### RESULT File (output)

| File | Contains |
|------|----------|
| RESULT.references.Author.Year.md | Key Learnings, Reference Index, References by Function, Unindexed References |

---

## Quick Start

### Step 1: Gather materials

- [ ] Journal article in markdown/text format → save as OBJECT.article.md
- [ ] Reference abstracts in markdown/text format → save as OBJECT.abstracts.md

### Step 2: Select or create field context

- [ ] Use existing OBJECT.field.md for your domain, OR
- [ ] Create new OBJECT.field.md using template below

### Step 3: Select intent

- [ ] Choose one SUBJECT.*.md matching your reading goal
- [ ] Add Runtime Specification if desired (optional for most intents)

### Step 4: Process

Provide Claude with:
1. SUBJECT.*.md (your selected intent)
2. VERB.read_references.action.md
3. VERB.read_references.description.md
4. OBJECT.field.md
5. OBJECT.article.md
6. OBJECT.abstracts.md

### Step 5: Receive output

- [ ] Review RESULT.references.Author.Year.md
- [ ] Follow up on Unindexed References if needed
- [ ] Curate and save for future reference

---

## Templates

### OBJECT.field.md Template (Blank)

```markdown
---
type: object
name: field
domain: [Field Name]
version: 1.0
created: [YYYY-MM-DD]
last_modified: [YYYY-MM-DD]
---

# OBJECT.field.md — [Field Name]

## Field Identity

Primary discipline: 
Subfield: 
Specific focus: 

## Foundational Concepts

- 
- 
- 

## Reference Ecosystem

Established knowledge base: 

Active frontier: 

Adjacent fields: 
```

### OBJECT.field.md Template (Pre-populated Example)

```markdown
---
type: object
name: field
domain: Microbial DNA Repair
version: 1.0
created: 2024-12-29
last_modified: 2024-12-29
---

# OBJECT.field.md — Microbial DNA Repair

## Field Identity

Primary discipline: Molecular microbiology
Subfield: DNA damage and repair mechanisms in bacteria
Specific focus: Discovery of novel DNA repair/protection proteins from phage and metagenomic sources

## Foundational Concepts

- Reactive oxygen species (ROS) cause DNA damage including strand breaks and nucleotide alterations
- RecA-dependent homologous recombination is a primary bacterial DNA repair mechanism
- Bacteriophages encode functional proteins that can complement or substitute for host functions

## Reference Ecosystem

Established knowledge base: ROS biology, canonical bacterial DNA repair pathways (RecA, RecBCD), E. coli genetics and mutant collections

Active frontier: Phage-derived proteins with novel functions, functional genomics screening of metagenomic libraries, structure-based function prediction for uncharacterized proteins

Adjacent fields: Structural biology, Bioinformatics, Phage therapy
```

---

## RESULT Structure

```markdown
---
type: result
source_agent: read_references
paper: [First Author] et al. [Year]
title: [Full title]
pmcid: [PMCxxxxxxx or "N/A"]
pmid: [xxxxxxxx or "N/A"]
doi: [10.xxxx/xxxxx]
date_read: [YYYY-MM-DD]
subject_used: [analysis|survey|retrieval|evaluate|writing|discussion]
---

## Key Learnings
[1-7 insights based on SUBJECT intent]

## Reference Index
[All references with identifiers and links]

## References by Function
### A. Background Information
### B. Prior Knowledge on Specific Subject
### C. Methods
### D. Results
### E. Discussion

## Unindexed References — MANUAL LOOKUP REQUIRED
[Citations not found in OBJECT.abstracts.md]
```

---

## Reference Category Definitions

| Category | Location | Description |
|----------|----------|-------------|
| A | Background | Early Introduction; field-level context |
| B | Prior Knowledge | Late Introduction; topic-specific prior work |
| C | Methods | Methods section; techniques, tools, protocols |
| D | Results | Results section; comparison, validation, contextualization |
| E | Discussion | Discussion section; interpretation, extension, contrast |

---

## Citation Purpose Codes

| Code | Purpose | Description |
|------|---------|-------------|
| (a) | Orientation | Introduces topic; refreshes reader memory |
| (b) | Positioning | Point article aims to support or refute |
| (c) | Methodological | Links to detailed procedures |
| (d) | Evidentiary | Establishes what is already known |
| (e) | Extensional | Provides follow-up resources |

---

## Collaboration

RESULT files can be:
- Curated individually
- Shared among team members
- Aggregated for literature reviews
- Used as input for future synthesis tasks

---

## Troubleshooting

| Issue | Check |
|-------|-------|
| Missing references in output | OBJECT.abstracts.md may be incomplete; see Unindexed References |
| Key Learnings don't match intent | Verify correct SUBJECT.*.md was loaded |
| Categories seem misassigned | Section inference may need article with clearer headers |
| Output format incorrect | Verify VERB.read_references.description.md was loaded |
