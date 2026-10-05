**nearby_features**
=

## Overview

Automated extraction of protein and residue features for candidate selection in protein screenings.

<img width="1631" height="918" alt="nearby_features" src="https://github.com/user-attachments/assets/bbbc4ab6-b709-4499-8adc-507df224b090" />

## Purpose

This tool was developed to extract and summarize biological information for a list of proteins and amino acid residues of interest, providing additional context for candidate characterization and selection.

It provides a quick overview of relevant protein features and retrieves domains and post-translational modifications that are spatially proximal to the residues of interest. Unlike a sequence-based approach, this analysis determines spatial proximity using the protein's predicted 3D structure, allowing the identification of features annotated to residues that are close in space but not necessarily in the amino acid sequence.

The tool provides additional context for screening hits, helping researchers prioritize candidates and identify potential correlations and patterns.

## Features

- **Summarize biological annotations:** Extract key protein-level features, including protein name, length, and subcellular location
- **Characterize residues of interest:** Determine whether the residue of interest falls within an oxidation-sensitive region and retrieve its predicted disorder value
- **Identify spatially proximal features:** Use AlphaFold-predicted structures to identify residues that are spatially proximal to the residue of interest in the folded protein, and retrieve functional domains and post-translational modifications annotated to those residues

### Data handling

- **Accession deduplication:** Reduce queries to public databases and minimize download time by deriving a unique list of protein accessions 
- **Local data caching:** Enable faster re-analysis with modified parameters or updated lists of hits

> **Scope:** The tool is currently tailored to the analysis of cysteines identified through redox screening, but the workflow can easily be adapted to other residues of interest.

## Usage

The tool takes an `.xlsx` file containing the list of screening hits to analyze. The input file should include two columns: **protein accession** and **residue position**.

### Running the analysis

Download and run the nearby_features.ipynb Jupyter Notebook. It imports and parses the input list, retrieves the required data from the AIUPred and UniProt REST APIs, and performs the analysis. The results are written to a new `.xlsx` file, with the analysis results appended to the original input data.

### Output

**Domains** are reported with the residue interval they span and the residue within the domain that is spatially closest to the residue of interest, followed by its distance in Å.

```Nuclear localization signal (750-763) - (763, 15.32 Å)```

**Post-translational modifications (PTMs)** are reported with the position of the modified residue and its distance from the residue of interest.

```Phosphoserine (522, 16.15 Å)```

**Disulfide bonds** report the positions of both cysteines involved in the bond, together with the distance of the cysteine closest to the residue of interest.

```Disulfide bond (60, 4.42 Å - 77)```

## References & acknowledgements

This tool uses data and resources provided through the following APIs and databases:

- **AIUPred v2:** [https://aiupred.elte.hu/](https://aiupred.elte.hu/)
- **EMBL-EBI Proteins API:** [https://www.ebi.ac.uk/proteins/api/doc/](https://www.ebi.ac.uk/proteins/api/doc/)
- **AlphaFold Protein Structure Database:** [https://alphafold.ebi.ac.uk/](https://alphafold.ebi.ac.uk/)

Sample data used to demonstrate the analysis are derived from the MS analysis of cell-cycle-dependent protein oxidation in [Vorhauser *et al.*, 2025](https://www.cell.com/molecular-cell/fulltext/S1097-2765(25)00646-X).
