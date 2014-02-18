Code and Raw Data for Acromegaly and Cushing Analyses
========================================================

This data was analysed at first on the mbni and felix servers to generate counts tables.  The rest of the analysis was performed locally once the counts table was generated.  See the **processing** folder for the code used in the generation of these alignments and counts tables.

Data Files
------------

Data files are located in the **data** directory
The raw data in this analysis is located in **data/raw** and is the following files:

* **patient_table.csv** contains the measured parameters for these patients.
* **patient_legend.txt** describes the units used for measurements in the patient table.
* **patient_sample_mapping.csv** maps the patients to their corresponding samples.
* **transcript_counts_table.csv** has the transcript level counts table.
* **exon_counts_table.csv** has the exon level counts table.  These data has not yet been incorporated into our analysis.
* **acromegaly_patient_IGF1.csv** has the IGF-1 levels for the acromegaly patients.

Data files generated by these scripts are located in the **data/processsed** directory.

Script Files
---------------
Script files are saved in **scripts** folder and were analysed in this order

### counts_table_filtering.Rmd

This file filters the counts table to show only the most abundant transcript.  It starts with the file **data/raw/transcript_counts_table.csv** and then ends up with **data/processed/filtered_transcript_counts_table.csv.**

### deseq_analysis_outlier.Rmd

This file performs the DESeq analysis both including and removing the one outlier patient who was accidentally included in the analysis.  This script takes the files **data/processed/filtered_transcript_counts_table.csv.** and **data/raw/patient_sample_mapping.csv** and generages annoted DESeq results files for both cushing and acromegaly, as well as lists of statistically significant genes.

### goseq-analysis.Rmd

This script searches KEGG and GO for enriched categories and pathways.  This generates a variety of Gene Ontology Analysis files and the data for Table 2.

### heatmaps.Rmd 

This generates the heatmap used in Figure 2.

## barplots.Rmd

This script generates all the barplots used in Figures 3, 4 and Supplementary Figures 1 and 2.

### acromegaly_clinical_analysis.Rmd

This script analyses the clinical characteristics of the groups, generating the table for Table 1 and Figure 1.


### GEO_comparasons.Rmd

This script compares our significant genes to another similar dataset.  This set treated adipocytes with growth hormone in vitro and did microarrays after 48h of treatment.

### igf_analysis.Rmd

This takes measured IGF-1 levels from acromegaly patients and compares it to *IGF1*  expression from WAT explants.

GSEA Analysis
---------------
For analysis by GSEA which is an external java program, we prepared the input files by running the script **GSEA_inputs_CushingAcromegaly.Rmd**.  This used version 2.0.13 of GSEA.  The standard settings were sorting ascending by t-test, with 1000 permutations of the phenotype.  The input files located in data/processed were:

* GSEA_pheno_acromegaly.txt
* GSEA_pheno_acromegaly.txt
* GSEA_Acromegaly_input_htseq_DEseq2.txt
* GSEA_Cushing_input_htseq_DEseq2.txt

The expression dataset was selected from either acromegaly or cushing.  The gene sets databases tested were:

* For KEGG gseaftp.broadinstitute.org://pub/gsea/gene_sets/c2.cp.kegg.v4.0.symbols.gmt
* For GO annotations gseaftp.broadinstitute.org://pub/gsea/gene_sets/c5.all.v4.0.symbols.gmt
* For transcription factors gseaftp.broadinstitute.org://pub/gsea/gene_sets/c3.tft.v4.0.symbols.gmt
* For miRNA gseaftp.broadinstitute.org://pub/gsea/gene_sets/c3.mir.v4.0.symbols.gmt
* For REACTOME gseaftp.broadinstitute.org://pub/gsea/gene_sets/c2.cp.reactome.v4.0.symbols.gmt

WIth the default 1000 permutations, based on phenotype (Cushing versus Control or Acromegaly versus Control), and setting collapse dataset to gene symbols to be false.  The permutation type was based on phenotype.  The remainder of the settings were the defaults, such as 1000 permutations, and excluding gene sets <15 or >500 members.
The chip platform was gseaftp.broadinstitute.org://pub/gsea/annotations/GENE_SYMBOL.chip.  The metric for ranking genes was tTest.

Figures
-----------
The figures generated for the manuscript, via the running of these scripts are in the **figures** directory.  These figures are modified for final publication in the **manuscript** folder using Adobe Illustrator CS6.

Manuscript
------------
The manuscript files, including the manuscript, the figures, tables and supplementary data are in the **manuscript** directory.  Within this directory are the files generated for uploading the raw and processed data to the Gene Expression omnibus (in the folder **manuscript/GEO_submission**).
