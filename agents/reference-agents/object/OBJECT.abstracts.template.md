---
type: object
name: abstracts
source_paper: [First Author] et al. [Year]
pmcid: [PMCxxxxxxx]
reference_count: [Number]
version: 1.0
created: [YYYY-MM-DD]
---

# OBJECT.abstracts.md — References for [Short identifier]

## Source Paper
- **Title:** [Full title]
- **PMCID:** [PMCxxxxxxx]
- **PMID:** [xxxxxxxx](https://pubmed.ncbi.nlm.nih.gov/xxxxxxxx/)
- **DOI:** [10.xxxx/xxxxx](https://doi.org/10.xxxx/xxxxx)

---

## References ([N] articles)

### [1] [Title of first reference]
- **PMID:** [xxxxxxxx](https://pubmed.ncbi.nlm.nih.gov/xxxxxxxx/)
- **DOI:** [10.xxxx/xxxxx](https://doi.org/10.xxxx/xxxxx)
- **Journal:** [Journal name] ([Year])

[Abstract text]

---

### [2] [Title of second reference]
- **PMID:** [xxxxxxxx](https://pubmed.ncbi.nlm.nih.gov/xxxxxxxx/)
- **DOI:** [10.xxxx/xxxxx](https://doi.org/10.xxxx/xxxxx)
- **Journal:** [Journal name] ([Year])

[Abstract text]

---

[Continue for all references...]

## Preparation Notes

**Recommended method:**
Use `utils/reference_pubmed_id_extractor.ipynb` with PMC ID to auto-generate this file.

**Manual preparation:**
1. Extract reference list from article
2. Look up each PMID in PubMed
3. Copy abstract for each reference
4. Number entries to match citation numbers in article

**If abstract unavailable:**
Write "No abstract available" — do not leave blank.
