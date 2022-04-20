# MODEC
MODEC is an integrative clustering method utilizing gene-level omics data and clinical features for cancer subtype identification. It comprehensively uses Manifold Learning and Deep Embedded Clustering, and simultaneously takes clinical features into consideration.

1. Joint representation space computation algorithm can be used to calculate a fixed rank joint subspace from omics data. The rank and number of omics data types can be customarized.

3. After preprocessing clinical data and merge it with the joint subspace, it can be passed into the Deep Embedded Clustering Module to get the predicted labels.

5. Datasets: We uploade the calculated joint subspace and preprocessed clinical data in the folder using three cancer cohorts, LGGs, BRCA and STAD. Also we provide the PAM50 subtype data at the same time.

7. Original data availability: 
   (1) gene-level and clinical datasets are downloaded from the TCGA portal. https://www.cancer.gov/about-nci/organization/ccg/research/structural-genomics/tcga
   
   (2) TCGA subtype data are downloaded through TCGABiolinks R package. https://bioconductor.org/packages/release/bioc/html/TCGAbiolinks.html
   
5. Input data format and example code for joint representation subspace calculation

   Use STAD cohort for instance. First read in omics data as Data_stad1, Data_stad2, Data_stad3. After selecting the same samples in all the datasets, drop nan value, normalize datasets and prepare the datasets with columns as markers while rows corresponding to samples, we generate a list including these omics datasets as:
   
   Data_stad_test_gene_protein_miRNA_mDNA = [Data_stad1, Data_stad2, Data_stad3]
  
   Given customized rank r and number of clusters k (using k we can get a silhouette score by applying k-means clustering). Please make sure r is greater or equal to k. We can get the joint subspace, silhouette score and corresponding rank as outputs.
   
   Ujoint, sil, rank = joint_view_fixedrank(Data_stad_test_gene_protein_miRNA_mDNA, k,r)
   
6. Input data for DEC: using combination of joint subspace from joint representation subspace calculation. For example, try to use STAD_rank20_joint.txt with columns as markers while rows corresponding to samples.

7. Output format: the output from MODEC will be clustering labels as numbers. We can map them to the subtype contained in the TCGA dataset to measure the clustering performance. The optimal matching is obtained by applying Hungarian method.

8. We use clinical matrix from TCGA database for survival and enrichment tests.
