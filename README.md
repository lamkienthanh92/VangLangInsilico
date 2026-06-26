VanLang InSilico Pipeline
Multi-Step Virtual Screening for Formalin Alternatives in IHC-Compatible Tissue Fixation
Department of Medical Laboratory Technology  |  Van Lang University, HCMC, Vietnam  |  2025
1.  Background
Formalin (10% neutral buffered formaldehyde) is the standard tissue fixative in surgical pathology, but formaldehyde is a Group 1 IARC carcinogen. This pipeline systematically identifies organic dialdehyde alternatives that preserve tissue morphology while remaining compatible with routine IHC markers (HER2, PD-L1).
This is a hypothesis-generating in silico study. All results require wet lab validation before any clinical application.

2.  Pipeline Overview
Five sequential notebooks (NB1-NB5), each evaluating one independent criterion. Only compounds passing all criteria advance.

Notebook	Method	Input	Output
NB1	Chemical & ADMET Filter (RDKit)	1,007 CIDs	154 compounds
NB2	Reactivity Scoring (TorchANI)	154 compounds	Top 30
NB3	Molecular Docking (AutoDock Vina 1.2.7)	Top 30	Top 10
NB4	SASA Epitope Analysis (FreeSASA)	Top 10	10/10 IHC OK
NB5	Feasibility + Grand Final Ranking	Top 10	Grand Final CSV

3.  Protein Targets
Target	PDB	Resolution	Epitope	LYS	Epitope SASA
HER2	1N8Z	2.5 A	Domain IV (res. 161-214)	5	2,988 A² (26.4%)
PD-L1	5X8M	2.9 A	IgV domain (res. 18-63)	4	2,874 A² (43.0%)

4.  Grand Final Top 3 Candidates
Rank	CID	SMILES	MW (Da)	Grand Score	Docking mean	Pen Rate
#1	91427	CCC(C=O)CC=O	114.1	64.21	-3.710 kcal/mol	0.354 mm/h
#2	87944034	O=CCCC#CCCC=O	138.2	64.03	-4.214 kcal/mol	0.324 mm/h
#3	21190979	CC(C)(C=O)CC=O	114.1	63.76	-3.433 kcal/mol	0.354 mm/h

5.  How to Run
-	Open Google Colab and set Runtime > Change runtime type > GPU (T4)
-	Paste each .py file into a single cell and run in order: NB1 > NB2 > NB3 > NB4 > NB5
-	All outputs saved automatically to Google Drive: MyDrive/VanLang_InSilico/

File	Runtime	GPU needed	Output
NB1_chemical_filter.py	5-10 min	No	NB1_final_shortlist.csv
NB2_reactivity_scoring.py	1-2 min	Yes	NB2_scored.csv
NB3_molecular_docking.py	4 min	No	NB3_docking_results.csv
NB4_sasa_epitope.py	< 1 min	No	NB4_sasa_results.csv
NB5_feasibility.py	< 1 min	No	NB5_grand_final.csv

6.  Dependencies
All packages install automatically via pip at the start of each notebook.

Package	Version	Purpose
RDKit	2026.03.3 (Colab built-in)	SMILES, descriptors, PAINS filter
TorchANI	2.2	Neural network potential ANI-2x (NB2)
AutoDock Vina	1.2.7 (pip)	Molecular docking (NB3)
FreeSASA	latest (pip)	SASA computation (NB4)
BioPython	latest (pip)	PDB parsing (NB3, NB4)
meeko	latest (pip)	Ligand PDBQT preparation (NB3)
pandas / numpy	Colab built-in	Data processing
matplotlib	Colab built-in	Visualization

7.  Reproducibility
-	Random seed: 42 (fixed throughout all notebooks)
-	PubChem API: accessed January-March 2025
-	PDB 1N8Z: HER2, 2.5 A, Homo sapiens - downloaded February 2025
-	PDB 5X8M: PD-L1, 2.9 A, Homo sapiens - downloaded February 2025
-	Platform: Google Colab, NVIDIA Tesla T4 (15.6 GB VRAM), Python 3.12

8.  Key Limitations
Step	Confidence	Main Limitation
NB1	High  ****	PAINS designed for drugs; may over-remove fixative scaffolds
NB2	Medium ***	Gasteiger charge is not DFT HOMO/LUMO; ANI-2x fallback
NB3	Medium ***	Rigid receptor; no entropy; lysine surface != true crosslink site
NB4	Low  **	Empirical SASA model; all compounds give 98-99% (poor discrimination)
NB5	Low-Med **	Kinetics proxy unvalidated; stability model inaccurate for glyoxal

9.  Citation
If you use this pipeline, please cite:

[Research Team]. VanLang InSilico Pipeline: Multi-step virtual screening for formalin
alternatives in IHC-compatible tissue fixation. Van Lang University, 2025.
github.com/lamkienthanh92/VangLangInsilico  |  DOI: [Zenodo - to be assigned]

Key tools: RDKit (Landrum 2006); AutoDock Vina 1.2.0 (Eberhardt, J Chem Inf Model 2021;61:3891); TorchANI ANI-2x (Devereux, J Chem Theory Comput 2020;16:4192); FreeSASA (Mitternacht, F1000Research 2016;5:189); Glyoxal as fixative (Richter, EMBO J 2018;37:139).

10.  License
MIT License - free to use for non-commercial academic research.
Copyright 2025 - Van Lang University, Department of Medical Laboratory Technology

VanLang InSilico Pipeline 2025  |  All results require wet lab validation before clinical application
