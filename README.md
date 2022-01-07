# MODEC
MODEC is an integrative clustering method utilizing gene-level omics data and clinical features for cancer subtype identification. It comprehensively uses Manifold Learning and Deep Embedded Clustering, and simultaneously takes clinical features into consideration.
1. Joint representation space computation algorithm can be used to calculate a fixed rank joint subspace from omics data. The rank and number of omics data types can be customarized.
2. After preprocessing clinical data and merge it with the joint subspace, it can be passed into the Deep Embedded Clustering Module to get the predicted labels.
3. Datasets: We uploade the calculated joint subspace and preprocessed clinical data in the folder using three cancer cohorts, LGGs, BRCA and STAD. Also we provide the PAM50 subtype data at the same time.
4. Original data availability: 
   (1) gene-level and clinical datasets are downloaded from the TCGA portal. https://www.cancer.gov/about-nci/organization/ccg/research/structural-genomics/tcga
   (2) PAM50 subtype data are downloaded through TCGABiolinks R package. https://bioconductor.org/packages/release/bioc/html/TCGAbiolinks.html
