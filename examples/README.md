## Example 1: Going through large body of literature
_Prompt_:
```
Claude, execute uploaded agent and skill. 
1. Change search period to last 18 months.
2. Prioritize research on antibiotic-bacteriophage synergy. 
3. Include at least 3 articles with phage cocktails in research.
4. Return 15 matches.
```
_Output_: [Bacteriophage Therapy Literature Report](https://github.com/espickle1/claude-agents/blob/main/examples/bacteriophage-therapy-literature-report-2024-2025.md)[^1]

## Example 2: Searching with specific criteria
_Prompt_:
```
Execute uploaded agent and skill. 
1. Change search period to last 6 months. 
2. Prioritize research on urinary tract infection. 
3. Strong preference for articles with at least one author based out from Baylor College of Medicine. 
4. No review articles.
```
_Output_: [Recent Literature: Bacteriophage Therapy for Urinary Tract Infections (Baylor College of Medicine Focus)](https://github.com/espickle1/claude-agents/blob/main/examples/bacteriophage_uti_baylor_literature_2025-12-19.md)

[^1]: Claude on paid plans comes with "memory" function and has access to **all** of your previous chats. Since I have used Claude to help me code software for wastewater surveillance in the past, Claude tried to tie search results to wastewater surveillance without me prompting. Yes, one can edit Claude's "memory" to modify this feature.
