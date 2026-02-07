% Figure marking agent plan

Read crystalline-churning-leaf.md
Here's the full plan as markdown:

Plan: Scientific Figure Generation Agent
Context
The user wants a new agent within the existing claude-agents markdown-based framework (SUBJECT/VERB/OBJECT pattern) that generates scientific figures from user-provided data, parameters, and descriptions. The agent will run on claude.ai using the Analysis tool (Python sandbox) for code execution and Claude's vision for visual inspection.

Key difference from existing agents: This agent is interactive and iterative — it presents multiple figure options in a first pass, then refines through repeated user feedback rounds until the user is satisfied. Existing agents (like read_references) are single-pass.

User Requirements Summary
Inputs: Numbers (csv/tsv/xls), parameters (figure type, layout, colors), descriptions (words, sample images, context)
Outputs: Clean, minimal figures. No backgrounds, few colors. One story per figure. Short titles/descriptions (one phrase each).
Statistics: Show p-values and comparison bars when values are given. Suggest appropriate statistical methods. User must provide all statistical values.
Workflow: First pass offers multiple figure options. Iterative refinement with user input at every step. Continues until user requests stop.
Files to Create

agents/figure-generation-agents/
  AGENT.generate_figure.md
  subject/
    SUBJECT.publication.md
    SUBJECT.exploratory.md
  verb/
    VERB.generate_figure.action.md
    VERB.generate_figure.description.md
    VERB.code-execution-skill.md
  object/
    OBJECT.data.template.md
    OBJECT.figure_spec.template.md
    OBJECT.style_guide.template.md
Total: 9 files

File-by-File Specification
1. AGENT.generate_figure.md — Master Orchestrator
Pattern to follow: agents/reference-agents/AGENT.read_references.md

YAML front matter:


type: agent
name: generate-figure
version: 1.0
created: 2026-02-07
description: Generates scientific figures from data and specifications through iterative refinement with user feedback
components:
  verb:
    - VERB.generate_figure.action.md
    - VERB.generate_figure.description.md
    - VERB.code-execution-skill.md
  subject:
    - SUBJECT.publication.md
    - SUBJECT.exploratory.md
  object:
    - OBJECT.data.md
    - OBJECT.figure_spec.md
    - OBJECT.style_guide.md (optional)
output: RESULT.figure.[Description].md
Body contains:

Purpose section (XML tag <agent_mission>)
Architecture diagram (SUBJECT + VERB + OBJECT flow)
File inventory table
Quick start (prepare data, choose subject, upload, execute, refine)
RESULT structure preview
Critical guidelines: clean output defaults, one story per figure, user-driven refinement loop
2. SUBJECT.publication.md — Journal-Quality Figures

type: subject
intent: publication
version: 1.0
created: 2026-02-07
description: Journal-quality figures for manuscript submission
compatible_verbs:
  - generate_figure
Body sections (matching existing SUBJECT pattern):

Intent: Publication-quality figure for journal submission
Reader Values: Precise axis labels with units, 8-12pt fonts, white background, colorblind-safe palette, vector-friendly, statistical annotations (p-values, comparison bars), proper legends, minimal chartjunk, one essential point per figure
Reader Tolerates: Multiple refinement cycles, strict style constraints, longer generation time
Reader Does Not Want: Decorative elements, 3D effects, gradient fills, busy backgrounds, multiple unrelated stories in one figure, excessive colors
Runtime Specification (optional): Target journal style
3. SUBJECT.exploratory.md — Quick Data Exploration

type: subject
intent: exploratory
version: 1.0
created: 2026-02-07
description: Quick data exploration and iteration
compatible_verbs:
  - generate_figure
Body sections:

Intent: Rapid visualization for data understanding
Reader Values: Speed, seeing all data, functional over beautiful, quick iteration
Reader Tolerates: Default styling, auto-generated labels, rough appearance
Reader Does Not Want: Excessive polish, slow generation, multiple refinement of aesthetics
Runtime Specification: None typical
4. VERB.generate_figure.action.md — Execution Phases (Core Logic)

type: verb
name: generate_figure
file: action
version: 1.0
created: 2026-02-07
description: Execution sequence for iterative figure generation with user feedback
requires: VERB.generate_figure.description.md
Seven execution phases:

Phase 1: Setup and Validation

Load SUBJECT, OBJECT.data, OBJECT.figure_spec, OBJECT.style_guide (if present)
Validate data columns match figure_spec variables
Confirm Analysis tool (Python sandbox) is available
Parse data format (CSV/TSV/JSON inline)
Phase 2: Data Understanding

Summarize dataset: column names, types, ranges, sample size, missing values
Cross-reference with figure_spec: validate requested variables exist
Identify statistical values provided by user (p-values, confidence intervals, etc.)
Present data summary to user for confirmation before proceeding
Phase 3: Figure Proposal (First Pass — Multiple Options)

Generate 2-3 distinct figure concepts based on data + spec + description
Each concept includes: figure type, what it emphasizes, layout sketch (text description), which variables mapped where
Present concepts to user with brief rationale for each
STOP and wait for user selection/feedback before proceeding
User may pick one, combine elements, or request entirely different options
Phase 4: Code Generation

Generate self-contained Python/matplotlib code for user's chosen concept
Apply SUBJECT style constraints and VERB defaults (see description.md)
Apply style guide overrides if OBJECT.style_guide provided
Code must: import all dependencies, embed data inline or load from provided format, apply clean defaults (white background, minimal colors, no grid unless requested), include statistical annotations (p-value bars, significance markers) when user provides values, save to file
Statistical guidance: if user's figure_spec mentions comparisons but no p-values provided, output a note suggesting appropriate statistical tests — do NOT compute statistics
Phase 5: Code Execution and Visual Inspection

Execute code via Analysis tool (Python sandbox)
If execution fails: capture error, fix code, re-execute (max 3 auto-fix attempts)
If execution succeeds: render figure, inspect using vision against checklist from description.md
Auto-fix obvious issues (clipped labels, overlapping text) without user input
Phase 6: Present to User and Collect Feedback

Show rendered figure to user
Provide short description: one phrase title, one phrase per subfigure, one phrase per figure-letter
STOP and wait for user feedback
User provides refinement input: words (change colors, make bars wider), numbers (new data, corrected values), or images (reference to match)
Incorporate ALL user input — do not ignore or partially apply feedback
Phase 7: Refinement Loop

Apply user's feedback to code modifications
Return to Phase 4 (Code Generation) with accumulated context
Preserve working code — modify targeted sections only
Repeat Phases 4-6-7 until user requests stop
No maximum cycle limit — user controls when to stop
Each cycle: present updated figure + updated description
Output Assembly (when user says stop):

Compile RESULT.figure.[Description].md with: YAML metadata, figure description (short phrases), final Python code, rendered figure (base64 or file ref), refinement history log
5. VERB.generate_figure.description.md — Settings and Templates

type: verb
name: generate_figure
file: description
version: 1.0
created: 2026-02-07
description: Style defaults, inspection checklist, figure description format, and output template
Body sections:

Inputs Table:

Input	File	Required
Figure intent	SUBJECT.*.md	Yes (one)
Data	OBJECT.data.md	Yes
Figure specification	OBJECT.figure_spec.md	Yes
Style guide	OBJECT.style_guide.md	No
Data-Bound Rule: All plotted values must come from OBJECT.data.md. Never fabricate data. Statistical values (p-values, CIs) must be provided by user — never compute them.

Clean Output Defaults (applied to ALL figures unless overridden):

Parameter	Default	Notes
background	transparent/white	No colored backgrounds
color_count	1-3 max	Minimum needed to distinguish groups
color_palette	grayscale first, then muted	Add color only when needed for meaning
figure_size	(8, 6) inches	
dpi	300	150 for exploratory
font_family	Arial/Helvetica	Sans-serif
axis_label_size	12pt	
tick_label_size	10pt	
title_size	14pt	
line_width	1.5pt	
grid	off	Unless user requests
spines	left + bottom only	Remove top + right
legend	only if >1 group	Minimal, outside plot area
file_format	PNG	SVG for publication
Figure Description Format (enforced):

Title: one phrase (e.g., "Effect of treatment X on cell viability")
Per subfigure: one phrase (e.g., "(A) Dose-response at 24h")
Per figure-letter: one phrase (e.g., "(B) Time course at 10 uM")
No multi-sentence descriptions. No paragraphs.
Statistical Annotation Rules:

When user provides p-values: draw comparison bars with asterisks (* p<0.05, ** p<0.01, *** p<0.001) or exact p-values (user's choice)
When user provides values for comparison: draw bracket + p-value between compared groups
When user describes comparisons but provides no values: output guidance note suggesting appropriate tests (t-test, ANOVA, Mann-Whitney, etc.) — never compute
Statistical guidance format: "Suggested test: [test name] — [1-sentence rationale]"
Visual Inspection Checklist (Phase 5):

Check	Criterion	Auto-fix?
Labels	All axes labeled with units	Yes
Legibility	Text readable at target size	Yes
Data integrity	All data points visible, no clipping	Yes
Overlap	No overlapping text/elements	Yes
Color count	Minimum colors used	Yes
Background	Clean/white/transparent	Yes
Spines	Only left + bottom	Yes
p-values	Comparison bars correct when provided	Yes
Story count	One essential point per figure	Flag to user
RESULT Template:


---
type: result
source_agent: generate_figure
figure_description: [one-phrase title]
subject_used: [publication|exploratory]
data_source: [OBJECT.data identifier]
date_generated: YYYY-MM-DD
refinement_cycles: [count]
---

## Figure Description
[One phrase title]
[One phrase per subfigure/panel]

## Statistical Notes
[Which tests were suggested, if any]
[p-values displayed and their sources]

## Python Code
[Complete, self-contained, runnable code]

## Rendered Figure
[Base64-encoded image or file reference]

## Refinement History
| Cycle | User Feedback | Changes Made |
|-------|--------------|--------------|
| 1 | [selected option X] | [initial generation] |
| 2 | [change Y to Z] | [modified Y] |
6. VERB.code-execution-skill.md — Python Execution Skill
Pattern to follow: agents/literature-survey-agents/verb/VERB.pubmed-search-skill.md


type: skill
name: code-execution
version: 1.0
author: James
created: 2026-02-07
description: Python code generation and execution via Claude Analysis tool for scientific figure rendering
scope: code-execution
dependencies:
  - type: capability
    name: claude-analysis-tool
    description: Claude's built-in Python sandbox on claude.ai
    required: true
  - type: python-library
    name: matplotlib
    version: ">=3.5"
    required: true
  - type: python-library
    name: numpy
    version: ">=1.20"
    required: true
  - type: python-library
    name: pandas
    version: ">=1.3"
    required: true
  - type: python-library
    name: seaborn
    version: ">=0.12"
    required: false
used_by:
  - generate-figure
tags: [python, matplotlib, code-execution, visualization]
Body: Overview, prerequisites check, code generation guidelines (self-contained, deterministic), execution protocol, output capture, error handling (syntax errors, runtime errors, max 3 auto-fix attempts).

7. OBJECT.data.template.md

type: object
name: data
dataset: [Dataset identifier]
source: [Origin of data]
format: [csv_inline|tsv_inline|json_inline]
rows: [Number]
columns: [Number]
version: 1.0
created: YYYY-MM-DD
Body: Dataset description, Column definitions table (name, type, units), Data section (inline in code block), Preparation notes (how to convert from Excel/CSV).

8. OBJECT.figure_spec.template.md

type: object
name: figure_spec
figure_type: [bar|scatter|line|heatmap|violin|box|histogram|multi_panel|custom]
title: [One-phrase figure title]
version: 1.0
created: YYYY-MM-DD
Body:

Figure type
Variables: X, Y, grouping, error bars
Statistical annotations: which comparisons, p-values (user-provided numbers)
Layout: panels, aspect ratio
Description: context in user's own words, what story to tell
Reference images: describe or attach sample figures to emulate
9. OBJECT.style_guide.template.md

type: object
name: style_guide
target: [journal_name|custom]
version: 1.0
created: YYYY-MM-DD
Body: Color palette overrides, typography overrides, dimension constraints, journal-specific rules.

Implementation Order
VERB files first (they define the processing contract):
VERB.generate_figure.action.md
VERB.generate_figure.description.md
VERB.code-execution-skill.md
SUBJECT files (lightweight):
SUBJECT.publication.md
SUBJECT.exploratory.md
OBJECT templates:
OBJECT.data.template.md
OBJECT.figure_spec.template.md
OBJECT.style_guide.template.md
AGENT orchestrator last (references everything above):
AGENT.generate_figure.md
Verification
After creating all files:

Upload all 9 files to a claude.ai conversation
Provide a small test dataset (e.g., 3-group bar chart with p-values)
Execute: Execute AGENT.generate_figure.md / SUBJECT: publication / VERB: generate_figure / OBJECT: data, figure_spec
Verify: Phase 3 presents 2-3 options, figure is clean/minimal, p-value bars render correctly, refinement loop works with feedback
Verify descriptions follow one-phrase format