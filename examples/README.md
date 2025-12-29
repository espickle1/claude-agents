## Example 1: Going through large body of literature
Skill: [VERB.pubmed-search-skill.md](https://github.com/espickle1/claude-agents/blob/main/agents/literature-survey-agents/verb/VERB.pubmed-search-skill.md)\
Agent: [AGENT.bacteriophage-therapy-literature-agent.md](https://github.com/espickle1/claude-agents/blob/main/agents/literature-survey-agents/verb/bacteriophage-therapy-literature-agent.md)\
Prompt: 
```
Claude, execute uploaded agent and skill. 
1. Change search period to last 18 months.
2. Prioritize research on antibiotic-bacteriophage synergy. 
3. Include at least 3 articles with phage cocktails in research.
4. Return 15 matches.
```
Output: [Bacteriophage Therapy Literature Report](https://github.com/espickle1/claude-agents/blob/main/examples/bacteriophage-therapy-literature-report-2024-2025.md)[^1]

## Example 2: Searching with specific criteria
Skill: [VERB.pubmed-search-skill.md](https://github.com/espickle1/claude-agents/blob/main/agents/literature-survey-agents/verb/VERB.pubmed-search-skill.md)\
Agent: [AGENT.bacteriophage-therapy-literature-agent.md](https://github.com/espickle1/claude-agents/blob/main/agents/literature-survey-agents/verb/bacteriophage-therapy-literature-agent.md)\
Prompt:
```
Execute uploaded agent and skill. 
1. Change search period to last 6 months. 
2. Prioritize research on urinary tract infection. 
3. Strong preference for articles with at least one author based out from Baylor College of Medicine. 
4. No review articles.
```
Output: [Recent Literature: Bacteriophage Therapy for Urinary Tract Infections (Baylor College of Medicine Focus)](https://github.com/espickle1/claude-agents/blob/main/examples/bacteriophage_uti_baylor_literature_2025-12-19.md)

## Example 3: Exploring a very different topic (higher level mathematics)
Skill: [VERB.pubmed-search-skill.md](https://github.com/espickle1/claude-agents/blob/main/agents/literature-survey-agents/verb/VERB.pubmed-search-skill.md)\
Agent: [AGENT.protein-language-model-literature-search-agent.md](https://github.com/espickle1/claude-agents/blob/main/agents/literature-survey-agents/verb/protein-language-model-literature-search-agent.md)\
Prompt:
```
Claude, execute uploaded skill and agent:
1. No reviews.
2. No preprints.
3. Search period: 2025/01/01 to 2025/08/01.
4. Ignore memory and do not user our chat history during search. Do not restrict search to topics that are relevant to me.
5. Give me at least two (but no more than four) articles with heavy mathematical basis, specifically graph theory and algebraic structures.
```
Output: [Protein Language Models with Mathematical Foundations](https://github.com/espickle1/claude-agents/blob/main/examples/protein-LLM-mathematical-foundations-2025.md)[^2]

## Example 4: Analyzing article references
(this example is from John's Microbiology Spectrum article on F21 and ROS repair)\
Agent: [AGENT.read_references.md](https://github.com/espickle1/claude-agents/blob/main/agents/reference-agents/AGENT.read_references.md)\
Subject: [SUBJECT.analysis.md](https://github.com/espickle1/claude-agents/blob/main/agents/reference-agents/subject/SUBJECT.analysis.md)\
Verb: [VERB.read_references.action.md](https://github.com/espickle1/claude-agents/blob/main/agents/reference-agents/verb/VERB.read_references.action.md), [VERB.read_references.description.md](https://github.com/espickle1/claude-agents/blob/main/agents/reference-agents/verb/VERB.read_references.description.md)\
Object: [OBJECT.field.microbial_dna_repair.md](https://github.com/espickle1/claude-agents/blob/main/agents/reference-agents/object/OBJECT.field.microbial_dna_repair.md)\
Prompt:
```
Claude, execute uploaded agent and files:

Execute AGENT.read_references.md
SUBJECT: analysis
VERB: read_references
OBJECT: field, article, abstracts

1. Ignore memory and start new.
2. Give me more details than default.
```
Output: [RESULT.references.Taylor.2024.md](https://github.com/espickle1/claude-agents/blob/main/examples/RESULT.references.Taylor.2024.md)[^3]

[^1]: Claude on paid plans comes with "memory" function and has access to **all** of your previous chats. Since I have used Claude to help me code software for wastewater surveillance in the past, Claude tried to tie search results to wastewater surveillance without me prompting. Yes, one can edit Claude's "memory" to modify this feature.
[^2]: We can get through literature with heavy non-alphabet characters (higher-level mathematics). Now, how much of that math Claude actually understands is still unknown. But there should be enough texts in most articles for this agent to function.
[^3]: The reference analysis agent uses a linguistic paradigm (SUBJECT-VERB-OBJECT) to separate reader intent from processing logic from input materials. This allows mixing and matching components for different analysis goals.
