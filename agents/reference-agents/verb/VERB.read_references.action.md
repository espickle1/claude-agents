---
type: verb
name: read_references
file: action
version: 1.1
created: 2024-12-29
last_modified: 2024-12-29
description: Execution sequence and processing logic
requires: VERB.read_references.description.md
---

# VERB.read_references.action.md

## Execution Sequence

### Phase 1: Setup

1. Load SUBJECT.*.md file (one of six intent files)
2. Load OBJECT.field.md
3. Load OBJECT.article.md
4. Load OBJECT.abstracts.md
5. Confirm all files present before proceeding

### Phase 2: Citation Extraction

1. Scan OBJECT.article.md for parenthetical citation patterns: (1), (2, 3), (4), etc.
2. For each citation found:
   - Record citation number(s)
   - Record the sentence containing the citation
   - Infer section location (Introduction, Methods, Results, Discussion)

**Section inference rules:**

If explicit headers exist, use them.

If no explicit headers:
- Introduction: Opening paragraphs establishing context; ends where experimental work begins
- Methods: Paragraphs describing procedures, materials, experimental design
- Results: Paragraphs reporting findings, data, measurements, observations
- Discussion: Paragraphs interpreting findings, comparing to other work, stating implications

**Introduction scope tracking:**

Within Introduction, citations narrow from broad to specific. Track progression:
- Early Introduction → broad field context
- Mid Introduction → narrowing to subfield
- Late Introduction (just before Methods/Results) → specific subject, gap statement

### Phase 3: Context Capture

For each citation:

1. Start with the sentence containing the citation
2. Evaluate if sentence is self-sufficient:
   - Subject is clear (not pronoun-dependent)
   - No ambiguous "this/these/that" references
   - Meaning does not depend on prior sentence
3. If insufficient, expand backward one sentence
4. Repeat evaluation; expand further if needed
5. Stop when context is clear

Do not expand forward unless backward expansion is impossible.

Rarely will full paragraph be necessary.

### Phase 4: Abstract Matching

**Fields typically present in OBJECT.abstracts.md:**
- Reference number [#]
- Title
- PMID and/or DOI
- Journal name
- Year
- Abstract text

**Fields typically NOT present in OBJECT.abstracts.md:**
- Author names
- Volume/issue/page numbers
- Affiliations

For each citation number:

1. Locate corresponding entry in OBJECT.abstracts.md (entries numbered [1], [2], etc.)
2. If entry exists with abstract text → proceed to Phase 5
3. If entry exists but "No abstract available" → record this; use title only for Phase 5
4. If entry does not exist → add to Unindexed References list; skip Phase 5 for this citation

### Phase 5: Connection Description

For each citation with matched abstract:

1. Read the context (from Phase 3)
2. Read the abstract (from Phase 4)
3. Determine purpose(s) served — refer to VERB.read_references.description.md for purpose codes (a-e)
4. Determine location category — refer to VERB.read_references.description.md for categories (A-E)
5. Write connection description per length specified in VERB.read_references.description.md
6. If same reference appears multiple times, generate separate descriptions for each instance

**Citation format in output:** Always refer to references by number **[#]** or quoted title **"[Title]"**. Never use author names.

**Internal inconsistency check:**

Compare what OBJECT.article.md claims about the reference versus what the abstract states.

If conflict detected:
- Flag per format specified in VERB.read_references.description.md
- Include both the article's claim and the abstract's actual content

### Phase 6: Key Learnings Generation

1. Identify which SUBJECT.*.md is loaded
2. Apply corresponding generation rules from Subject Integration Logic below
3. Generate Key Learnings per count specified in VERB.read_references.description.md
4. If SUBJECT.retrieval.md or SUBJECT.evaluate.md is loaded and Runtime Specification is blank:
   - Generate menu of options (see Subject Integration Logic)
   - Pause for reader selection
   - Generate Key Learnings based on selection
5. Otherwise, generate Key Learnings directly

**Subject Integration Logic:**

**If SUBJECT.analysis.md:**
- Scan for mechanistic insights, causal claims, evidence quality
- Prioritize findings that explain how something works
- Include technical details relevant to mechanism
- Note where findings extend or challenge prior work
- Exclude broad context and tangential findings

**If SUBJECT.survey.md:**
- Scan for range of concepts, methods, connections
- Note relationships to adjacent fields
- Identify patterns across references
- Include entry points for further exploration
- Exclude deep mechanistic detail

**If SUBJECT.retrieval.md:**
- If Runtime Specification contains query → extract specific information matching query
- If Runtime Specification is blank → present retrievable categories menu (see description.md)
- After selection, generate learnings with concrete values and source locations

**If SUBJECT.evaluate.md:**
- If Runtime Specification contains claim → evaluate that claim
- If Runtime Specification is blank → generate evaluable claims menu from article's central assertions
- After selection, assess evidence strength, limitations, caveats

**If SUBJECT.writing.md:**
- Identify argument structure and rhetorical patterns
- Note how references build the case
- Extract novelty framing strategies
- Focus on transferable models
- Exclude findings unless relevant to writing structure

**If SUBJECT.discussion.md:**
- Comprehensive coverage required
- Include main findings, claims, evidence quality
- Note strengths and weaknesses
- Identify open questions, ambiguities, counterarguments
- Connect to broader field context

### Phase 7: Object Integration

Use OBJECT.field.md to inform processing:

1. **Field Identity** → Understand domain; calibrate scope recognition
2. **Foundational Concepts** → Citations matching these are likely Category A (Background)
3. **Reference Ecosystem:**
   - Established knowledge base → likely Categories A, B (evidentiary purpose)
   - Active frontier → likely Categories B, D, E (positioning purpose)
   - Adjacent fields → likely Category C (methodological) or E (extensional)

Apply this context when:
- Writing connection descriptions (use appropriate framing for field)
- Recognizing scope narrowing in Introduction
- Distinguishing foundational from frontier references

### Phase 8: Output Assembly

1. **Compile metadata from OBJECT.article.md header**
   - Author names ARE available here (e.g., "Taylor et al. 2024")
   - Use exactly as provided in OBJECT.article.md YAML header

2. Insert Key Learnings (from Phase 6)

3. **Build Reference Index from OBJECT.abstracts.md:**
   - List all references from OBJECT.abstracts.md
   - For each entry, extract ONLY fields present in OBJECT.abstracts.md:
     - Title (quoted)
     - Journal name
     - Year
     - PMID/DOI/PMCID (apply identifier fallback order per description.md)
   - **Do NOT add author names** — they are not in OBJECT.abstracts.md
   - Format links appropriately

4. Organize References by Function:
   - Group by location category (A-E)
   - Include connection descriptions (from Phase 5)
   - Cite references by **[#]** only, never by author name
   - References may appear in multiple categories if cited multiple times with different functions

5. Add Internal Consistency Notes section:
   - Reference by **[#]** and quoted title fragment
   - Never use author names

6. Add Unindexed References section (from Phase 4)

7. Format according to RESULT template (see description.md)

### Phase 9: Validation

Before finalizing output:

1. ☐ All citations from OBJECT.article.md accounted for
2. ☐ Each citation has connection description or is listed as unindexed
3. ☐ Key Learnings count matches SUBJECT requirements per description.md
4. ☐ No empty sections (if section has no entries, note per description.md)
5. ☐ All links formatted correctly
6. ☐ Internal inconsistencies flagged where detected
7. ☐ **No author names appear for cited references** — only [#] numbers and quoted titles used (source article metadata in header is exempt)
