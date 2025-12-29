---
type: result
source_agent: read_references
paper: Taylor et al. 2024
title: "Gene discovery from microbial gene libraries I: protection against reactive oxygen species-driven DNA damage"
pmcid: PMC11536983
pmid: 39283089
doi: 10.1128/spectrum.00365-24
date_read: 2024-12-29
subject_used: analysis
---

## Key Learnings

- F21 is a 183-amino-acid protein derived from accidental reverse-orientation cloning of a 552bp segment of an Alcanivorax recQ helicase gene; BLASTp returns no sequence homology to known proteins, making this a genuinely novel sequence

- Authors demonstrate F21 expression significantly reduces ROS-induced DNA damage in ∆recA mutants (TUNEL assay, P < 0.0001 after 1-hour recovery with induction), indicating F21 can function independently of the canonical RecA-dependent repair pathway

- Structural prediction via ESMFold reveals F21 is dominated by anti-parallel beta-sheet forming a stable platform, with a region (residues 157-169) showing structural similarity to a helix-turn-helix DNA binding motif (RMSD 1.37 Å, TM-score 0.44 versus CBASS-associated protein PDB: 7T5W)

- Computational DNA binding analysis (pyDockDNA) identifies a binding interface with up to 7 potential hydrogen bonds between F21 and dsDNA; DRNApred assigns 0.73 average probability of DNA interaction for residues 162-168

- F21 contains a predicted zinc-coordinating pocket (His9, His54, Cys56 within ~3.5 Å) consistent with metal-dependent DNA binding proteins, though direct biochemical confirmation of zinc binding is not provided

- F21 expression enables bacteria to reduce extracellular H₂O₂ levels overnight (Amplex Red assay, P < 0.0001), but authors acknowledge whether H₂O₂ reduction drives DNA protection or results from improved cell viability remains unresolved — the causal direction is not established

- Evidence for direct DNA binding is suggestive but indirect: computational predictions and gel shift assay show band changes with F21-containing lysate, but no purified protein binding studies or mutagenesis of predicted binding residues were performed

---

## Reference Index

- [1] Auten & Davis 2009 | PMID: 19390491 | https://pubmed.ncbi.nlm.nih.gov/19390491
- [2] Lesser 2006 | PMID: 16460273 | https://pubmed.ncbi.nlm.nih.gov/16460273
- [3] Poetsch 2020 | PMID: 31993111 | https://pubmed.ncbi.nlm.nih.gov/31993111
- [4] Chatterjee & Walker 2017 | PMID: 28485537 | https://pubmed.ncbi.nlm.nih.gov/28485537
- [5] Wigley 2013 | PMID: 23202527 | https://pubmed.ncbi.nlm.nih.gov/23202527
- [6] Begley & Samson 2004 | PMID: 15279801 | https://pubmed.ncbi.nlm.nih.gov/15279801
- [7] Su et al. 2019 | PMID: 31193309 | https://pubmed.ncbi.nlm.nih.gov/31193309
- [8] Durante et al. 1991 | PMID: 1674280 | https://pubmed.ncbi.nlm.nih.gov/1674280
- [9] Gu Liu et al. 2024 | PMID: 39315792 | https://pubmed.ncbi.nlm.nih.gov/39315792
- [10] Lin et al. 2023 | PMID: 36927031 | https://pubmed.ncbi.nlm.nih.gov/36927031
- [11] Holm et al. 2023 | PMID: 36419248 | https://pubmed.ncbi.nlm.nih.gov/36419248
- [12] Rohwer & Azam 2000 | PMID: 10698764 | https://pubmed.ncbi.nlm.nih.gov/10698764
- [13] Park et al. 2005 | PMID: 15967999 | https://pubmed.ncbi.nlm.nih.gov/15967999
- [14] Rodríguez-Lumbreras et al. 2022 | PMID: 36275623 | https://pubmed.ncbi.nlm.nih.gov/36275623
- [15] Lau et al. 2022 | PMID: 36156805 | https://pubmed.ncbi.nlm.nih.gov/36156805
- [16] Yan & Kurgan 2017 | PMID: 28132027 | https://pubmed.ncbi.nlm.nih.gov/28132027
- [17] Johnston 1987 | PMID: 3299106 | https://pubmed.ncbi.nlm.nih.gov/3299106
- [18] Triggs-Raine et al. 1988 | PMID: 3045098 | https://pubmed.ncbi.nlm.nih.gov/3045098
- [19] von Ossowski et al. 1993 | PMID: 8360921 | https://pubmed.ncbi.nlm.nih.gov/8360921
- [20] Terwilliger et al. 2020 | PMID: 32626851 | https://pubmed.ncbi.nlm.nih.gov/32626851
- [21] Yamamoto et al. 2009 | PMID: 20029369 | https://pubmed.ncbi.nlm.nih.gov/20029369
- [22] Baba et al. 2006 | PMID: 16738554 | https://pubmed.ncbi.nlm.nih.gov/16738554
- [23] Pettersen et al. 2021 | PMID: 32881101 | https://pubmed.ncbi.nlm.nih.gov/32881101

---

## References by Function

### A. Background Information

General knowledge establishing the broader context for this work.

- [1] Establishes ROS as cell signaling molecules that also provoke damage to cellular organelles and processes; provides framework for understanding oxidative threat
- [2] Extends ROS biology to marine environments; establishes that oxidative stress damages lipids, proteins, and DNA across diverse contexts
- [3] Reviews genomic distribution of oxidative DNA damage, repair mechanisms, and resulting mutagenesis; frames DNA damage as threat to genome stability
- [4] Comprehensive overview of DNA damage mechanisms and repair/tolerance pathways; establishes homologous recombination as common repair mechanism

### B. Prior Knowledge on Specific Subject

What was known about the narrow topic before this paper.

- [5] Describes RecBCD mechanism for processing double-strand breaks and loading RecA for homologous recombination; establishes the canonical bacterial repair pathway that F21 bypasses
- [6] Reviews network responses to DNA damage including scavengers and checkpoints; establishes that prevention mechanisms exist alongside repair
- [7] Demonstrates T4 phage DNA ligase alone mediates bacterial chromosome DSB repair via non-homologous end joining; key precedent for phage-encoded repair proteins
- [8] Shows T4 DNA ligase can repair potentially lethal damage when introduced into eukaryotic cells; extends phage repair capacity across domains
- [9] Describes construction of IMMФRTL phage gene libraries and introduction into ∆recA E. coli; establishes the screening platform used for F21 discovery

### C. Methods

Techniques, protocols, analytical approaches, or tools used in this paper.

- [10] ESMFold protein language model for atomic-level structure prediction from sequence; used to predict F21 structure
- [11] DALI server for structural homology search; used to identify structural similarities despite lack of sequence homology
- [12] TUNEL assay protocol for detecting DNA damage via 3'-OH end labeling in prokaryotes; primary method for quantifying DNA damage
- [13] Characterization of Hpx- mutants lacking H₂O₂ scavenging enzymes; provides model system with endogenous oxidative DNA damage
- [14] pyDockDNA web server for energy-based protein-DNA docking; used to model F21-DNA binding modes
- [16] DRNApred algorithm for sequence-based prediction of DNA-binding residues; used to identify probable binding residues in F21
- [21] Update on Keio collection of E. coli single-gene deletion mutants; source of ∆recA strain
- [22] Construction method for Keio collection in-frame knockouts; methodological basis for mutant strains used
- [23] UCSF ChimeraX for structure visualization; used for visualizing F21 structure, surface charge, and binding modes

### D. Results

References invoked to contextualize, compare, or validate findings.

- [15] Describes helix-turn-helix motif in CBASS immune signaling protein (PDB: 7T5W); F21 residues 157-169 show structural similarity (RMSD 1.37 Å) to this DNA-binding motif
- [17] Establishes zinc as essential cofactor in DNA binding domains (GAL4 protein); supports interpretation of F21's predicted His/Cys zinc-coordinating pocket as functionally relevant

### E. Discussion

References used to interpret findings, address limitations, or suggest implications.

- [7] Prior demonstration that phage-encoded proteins (T4 ligase) can mediate DNA repair; positions F21 within established precedent for phage repair functions
- [8] Extension of T4 ligase repair to eukaryotic cells; broadens implications of phage-derived repair proteins
- [18] Nucleotide sequence of katG encoding catalase HPI; comparative context for oxidative stress response proteins
- [19] Evolutionary analysis of catalase family showing independent origins; contextualizes diversity of ROS defense mechanisms
- [20] TAILΦR initiative for personalized phage therapy; situates this discovery within broader program of phage-derived therapeutic development

---

## Unindexed References — MANUAL LOOKUP REQUIRED

- None identified. All 23 citations matched to abstracts in OBJECT.abstracts.md.
