# MODEC
MODEC is an integrative clustering method utilizing gene-level omics data for cancer subtype identification. It comprehensively uses Manifold Learning and Deep Embedded Clustering, and simultaneously takes clinical significance into consideration. MODEC subtypes are very competitive both for arrucate clustering ang clinical significant difference identification, which will be helpful in real world.

1. Joint representation space computation algorithm can be used to calculate a fixed rank joint subspace from omics data. The rank and number of omics data types can be customarized.

3. After preprocessing clinical data and merge it with the joint subspace, it can be passed into the Deep Embedded Clustering Module to get the predicted labels.

5. Datasets: We uploade the calculated joint subspace and preprocessed clinical data in the folder using three cancer cohorts, LGGs, BRCA and STAD. Also we provide the PAM50 subtype data at the same time.

7. Original data availability: 
   (1) Omics and clinical datasets are downloaded from the TCGA portal. https://www.cancer.gov/about-nci/organization/ccg/research/structural-genomics/tcga
   
   a. RNAseq data normalized counts (Illumina HiSeq platform, Gene-level, RPKM)
   
   b. miRNA expression for tumor samples (Illumina HiSeq platform, Normalized, miRgene-level, RPM)
   
   c. Methylation data of tumor samples at Gene level (Beta values, Illumina HM27 platform)
   
   (2) TCGA subtype data are downloaded through TCGABiolinks R package. https://bioconductor.org/packages/release/bioc/html/TCGAbiolinks.html
   
   Run the following code in R to get access to the available subtype datasets, using Breast Cancer cohort for example:
   #load the required package
   library(TCGAbiolinks)
   #get access to the required cancer cohort
   BRCA_path_subtypes <- TCGAquery_subtype(tumor = "brca")
   
5. Input data format and example code for joint representation subspace calculation

   Use BRCA cohort for instance, the data preprocessing step is introduced in the application example using BRCA cohort (https://github.com/Tiffanyytz/MODEC/blob/main/Data_preproccessing_step). First read in omics data as Data_brca1, Data_brca2, Data_brca3. After selecting the same samples in all the datasets, drop nan value, normalize datasets and prepare the datasets with columns as markers while rows corresponding to samples, we generate a list including these omics datasets as:
   
   Data_brca_list = [Data_brcam1, Data_brcam2, Data_brcam3]
   
   Given customized rank r and number of clusters k (using k we can get a silhouette score by applying k-means clustering). Please make sure r is greater or equal to k. We can get the joint subspace, silhouette score and corresponding rank as outputs.
   
   Z, sil, rank = joint_view_fixedrank(Data_brca_list, k,r)
   
6. Input data for DEC: using combination of joint subspace from joint representation subspace calculation. For example, try to use BRCA_rank40_joint.txt with columns as markers while rows corresponding to samples.

7. Output format: the output from MODEC will be clustering labels as numbers. We can map them to the subtype contained in the TCGA dataset to measure the clustering performance. The optimal matching is obtained by applying Hungarian method. The mapping algorithm is provided in the application example using BRCA cohort.

8. We use clinical matrix from TCGA database for survival and enrichment tests. We use several keywords to filter the features for this part.

This work has been published in Briefings in Bioinformatics, https://doi.org/10.1093/bib/bbac372.
