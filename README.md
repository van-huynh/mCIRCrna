# mCIRCrna
The goal is to integrate circadian transcriptomes with muscle snRNA-seq data to identify age and cell type dependent circadian gene signatures that demonstrate tissue chronicity in muscle.


## Table of Contents

- [mCIRCrna](#team-repo-template)
    - [Background](#background)
    - [Hypothesis](#hypothesis)
    - [Aims](#aims)
    - [Data](#data)
    - [Method](#method)
        - Circadian Regulated Genes
        - Differential Expressions
        - Tools
    - [Results](#results)
        - Circadian Regulated Genes
        - Differential Expressions
    - [References](#references)
    - [Team Members](#team-members)

## Background

Skeletal muscle is an endocrine organ that composes 40-60% of the adult body mass with  metabolic and overall health span implications for the [entire body](https://www.nature.com/articles/nrendo.2012.49). In aging it is well accepted that circadian rhythm declines and is dependent on [transcription reprogramming](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC4965692/). Because skeletal muscle is an endocrine organ consisting as a substantial portion of body mass, it poses as a promising organ for drug therapeutics, but its high cellular heterogeneity poses a challenge to safe druggable target. 

## Hypothesis

We hypothesize that we will be able to identify markers important to circadian rhythm and certain cell types if we cross- reference gene expression across age associated with circadian rhythm patterns from bulk transcriptomics to single cell muscle transcriptomics data.


## Aims

To identify circadian gene signatures that demonstrate tissue chronicity (2 fold expression changes over time) compared to age and cell type in muscle.

- Find genes that show chronicity (2 fold changes over time course ZT1-24) from CircAge RNA-seq transcriptomic database across age for young and old adult

- Cross reference signifcant genes that epress chronicity from CircAge RNA-seq transcriptomic to Myoatlas snRNA-seq muscle database for cell specific age related for young and old adult differential expression

## Data

- McCarthy JJ, Andrews JL, McDearmon EL, Campbell KS, Barber BK, Miller BH, Walker JR, Hogenesch JB, Takahashi JS, Esser KA. Identification of the circadian transcriptome in adult mouse skeletal muscle. Physiol Genomics. 2007 Sep 19;31(1):86-95. doi: 10.1152/physiolgenomics.00066.2007. Epub 2007 Jun 5. PMID: 17550994; PMCID: PMC6080860.

- Petrany MJ, Swoboda CO, Dun, C, Chetal K, Chen Z, Weirauch MT, Salomonis N, Millay DP. Single-nucleus RNA-seq identifies transcriptional heterogeneity in multinucleated skeletal myofibers. Nat Communications. 2020 Dec 11;11(6374). doi: 10.1038/s41467-02020063.

- CircAge: https://circaage.shinyapps.io/circaage/

- MyoAtlas: https://research.cchmc.org/myoatlas/

- Datasets: https://www.synapse.org/#!Synapse:syn21676145/files/

## Method

### Circadian regulated genes
Circadian gene expression data (McCarthy et.al. 2007) were acquired for male mouse C57B6/J gastrocnemius muscle 7-10 weeks of age. It was compared to CircAge bulk transcriptomics of C57B6/J-NIA mice skeletal muscle which measured gene expression from tissue collected every 4 hours for 48 hours in total darkness (DD), with the first time point being circadian time (CT) 18. 6 month (young adult) and 27 month (old-adult) data were used.

### Differential Expression
Filtered feature bc files for each age group (5 month and 24 month) from snRNA Sequencing were downloaded from https://www.synapse.org/#!Synapse:syn21676145/files/ deposited by Millay DP et al. R (version 4.1.1) package Seurat (version 4.1.1) was used to explore the gene expressions across cell types and ages. For each age group, nuclei with less than 200 or greater than 3200 expressed features and the features that were expressed in less than three cells were excluded. Data were normalized logarithmically using the NormalizeData() function. The top 2000 features with the highest expression variability across the nuclei were identifided using FindVariableFeatures() function, which were then used in Principle Component Analysis (PCA) with RunPCA() function. For cell clustering and Uniform Manifold Approximation and Projection (UMAP) visualization, 12 and 15 components were used for 5 month and 24 month, respectively. The cell clustering and UMAP were done using FindNeighbors(), FindClusters(), and RunUMAP() functions. Cell types were assigned manually as did by Millay DP et al. The datasets were subset to select populations of interest, which are muscle cells. 
The 5 month and 24 month datasets were then integrated using FindIntegrationAnchors(), creating a new integrated Seurat object. PCA and UMAP visualization were done as described above. The function FindMarkers() was used to determine differential expression between populations of interest across ages and between cell populations. The FeaturePlot() function was used for visualization of the results. 


### Tools
Seurat (version 4.1.1)
CircAge
R (version 4.1.1)
R Studio

## Results
We identified 32 circadian-regulated transcripts that have age- and cell-type-dependent differential expression patterns in mice skeletal muscle. Expression level of 28 genes differ in Type IIx Myonuclei, Type IIb Myonuclei, and Satellite Cells at 5 months and 24 months. Differential expression of 2 transcript is strictly between age, while 4 were exclusive between cell types.


![image](https://user-images.githubusercontent.com/107160194/183271995-ffd29786-3719-4034-b519-2aa3e0401c2f.png)
![image](https://user-images.githubusercontent.com/107160194/183272331-ee82a2fe-1cbe-43b4-baea-782a096e4c5f.png)
 > Example data: Pank1 is a Type IIB myonuclei marker that is significantly circadian only in old mice

## References
Ding, Haocheng, et al. Likelihood-based tests for detecting circadian rhythmicity and differential circadian patterns in transcriptomic applications. Briefings in Bioinformatics 22.6 (2021): bbab224.

McCarthy JJ, Andrews JL, McDearmon EL, Campbell KS, Barber BK, Miller BH, Walker JR, Hogenesch JB, Takahashi JS, Esser KA. Identification of the circadian transcriptome in adult mouse skeletal muscle. Physiol Genomics. 2007 Sep 19;31(1):86-95. doi: 10.1152/physiolgenomics.00066.2007. Epub 2007 Jun 5. PMID: 17550994; PMCID: PMC6080860.

Petrany MJ, Swoboda CO, Dun, C, Chetal K, Chen Z, Weirauch MT, Salomonis N, Millay DP. Single-nucleus RNA-seq identifies transcriptional heterogeneity in multinucleated skeletal myofibers. Nat Communications. 2020 Dec 11;11(6374). doi: 10.1038/s41467-02020063.

Hao Y, Hao S, Andersen-Nissen E, III WMM, Zheng S, Butler A, Lee MJ, Wilk AJ, Darby C, Zagar M, Hoffman P, Stoeckius M, Papalexi E, Mimitou EP, Jain J, Srivastava A, Stuart T, Fleming LB, Yeung B, Rogers AJ, McElrath JM, Blish CA, Gottardo R, Smibert P, Satija R (2021). “Integrated analysis of multimodal single-cell data.” Cell. doi:10.1016/j.cell.2021.04.048.

## Team Members

- Shufan Zhang | shufan0519@gmail.com | Team Leader  
- Lisa Shrestha | Member
- Van Nha Huynh | Member
- Kristen Coutinho | Member
- Russel Santos | Member
- Herminio Vazquez | Member

