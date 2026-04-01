# RCC-immuno-genomincs
Study of DP T cells in Renal cancer, data taken from [1]
This multi omics project in the field of cancer genomics immunology studied the behavior of DP T cells in Renal cell carcinoma. 

# Addressing the issues
To map the Progenitor Engine of the Tumor Immune Response following questions had to be addressed

(1). The Double Positive (DP) population found in tumor cells of Renal Cell Carcinoma (RCC)
Authors of the study identified a small population of T-cells expressing both CD4 and CD8 markers (Double Positive, or DP). DP cells found in tumor tissue could represent a functional source of new immune cells, triggered by the tumor environment.

(2). Multi-Omic Integration
To address these issues, distinct layers of single-cell data from had to be integrated: 
 - Transcriptomics data (scRNA-seq) was used to identify cell populations 
 - TCR Sequencing data (scTCR-seq) was used to track families (clonotypes) across different states
 - Cell Cycle Scoring was used to identify which cells were actively dividing.

(3) The Evidence
To answer these and other related questions, following functionality had to be used
 - The Genetic Fingerprint (Clonal Sharing) -> By identifying shared TCR sequences, we proved that cells in the DP cluster shared identical genetic parents with cells in the mature CD8 and CD4 clusters
 - The Expansion Ratio (Source vs. Sink)  -> Size of these families needed to be quantified. Top clones showed a massive imbalance, where a handful of DP cells (the "Source") were linked to thousands of CD8/CD4 cells (the "Sink")
 - The Metabolic Engine (Proliferation) -> Using dot plots of known proliferation markers, the DP cells were found to be the only group in a state of high-velocity division
 - The Lineage Bifurcation (PAGA Trajectory) -> Using PAGA trajectory analysis, connectivity between clusters was mathematically modelled.

Using the findings from above points the study concluded that DP cells in RCC represent a progenitor reservoir with following functions:
 - Recognize tumor antigens
 - Amplifies the response through rapid division
 - Refills the army of effector cells that are exhausted or killed by the tumor.

# Processing flow
Complete processing flow is represented by Flow diagram (Figure 1)

![Complete processing flow](Images/Flow_diagram.png)
**Figure 1: Complete processing flow**

## Comments on processing flow

### Phase 1 (The Input)

Before any operations could be done, following issues needed to be resolved:
 - Barcode mismatch between the inputs (scRNA-seq, scTCR-seq)
 - Creation of unified data object with TCR and single cell data

#### UMAP plots

The different cell lineages are best illustrated by UMAP plots. 

![UMAP plot I](Images/UMAP_plot_I.png)

**Figure 2: UMAP plot I (cell type/patient)** 

![UMAP plot II](Images/UMAP_plot_II.png)

**Figure 3: UMAP plot II (cell cycle/T cell functional identity)**

**Observation on UMAP plot II**

Plot on the left (cell cycle) shows T-cells that are actively proliferating (G2S, M phase) vs. others (G1 phase) concentrated in the top middle cluster, which coincides with the top middle cluster (marked PROLIF) of the UMAP plot on the right. Both plots show cells that are actively proliferating occupying the same cluster on different plots. Cell cycle distribution may also be visualized with stacked bar plot.

![Cell cycle distribution](Images/Cell_cycle_distribution.png)

**Figure 4: Cell cycle distribution**


### Phase 2 (TCR data) - Identifying shared clonotypes

In order to establish clonal relationship between different cell lineages, shared clonotype category is required. This enables us to view which clonotypes are shared between DP and CD4/CD8 lineages. These relationships are illustrated with UMAP plots.

![Shared clonotypes](Images/Clonal_evidence_of_DP_transition.png)

**Figure 5: Shared clonotypes UMAP plot**

The CD4 Transition plot shows dots concentrated more toward the top and far-left islands, whereas the CD8 Transition (Right) plot shows red dots are much more dense in the lower-right clusters. 
Small, dense cluster in the center-right is intense in both plots. This is the DP progenitor pool is feeding both lineages simultaneously.

### Phase 3 (scRNA data) - Identify dividing cells

In this phase, proliferating cells were identifies using well-known marker genes 

![Proliferation](Images/Stemness_and_proliferation.png)

**Figure 6: Proliferation of cell lineages** 

**Observation**

The DP group has the lowest total cell count, it has the highest concentration of actively dividing cells. These cells are in a state of rapid cell cycle (mitosis), creating the seeds that then differentiate and expand into the massive CD8 and CD4 lineages, as seen on Figure 5.  This proves that the DP population is the Progenitor Engine.

CD4 group shows the highest expression of  classic marker for stem-like memory T-cells . This implies that CD4 cells are acting as the long-term pool, required to maintain presence of these cell lineages in the tumor.

## Phase 4 (Integration) - Detailed Functional analysis

### Clonotypes summary

In this section, the most frequent clonotypes found in this assay were identified and quantificated. The summary is provided in the Table 1.


![Clonotypes](Images/Clonotypes.png)

**Table 1: Frequency of Clonotypes** 

References:
[1] Functionally heterogeneous intratumoral CD4+CD8+ double positive T cells can give rise to single positive T cells, PRJNA1389917, https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE314072
