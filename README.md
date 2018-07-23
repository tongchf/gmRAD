# gmRAD: an integrated  pipeline to call SNP genotypes across a hybrid population for genetic mapping  with RADseq data
# Introduction
gmRAD is used to call SNP genotypes across a hybrid population with RAD-seq data for genetic linkage mapping. It takes five steps as following to finish the whole work.  
        1. Clustering the first reads of each parent;  
        2. Building the reference sequence within a cluster for each parent;  
        3. Generating the parental SNP catalogs;  
        4. Calling SNP genotypes across the individuals in the whole population;  
        5. Filtering the SNP data by considering segregation ratio and missing data.  
# Usage
To run gmRAD, users should install the three prerequisite packages: [LOCAS](http://ab.inf.uni-tuebingen.de/software/locas/), BWA and SAMtools (with BCFtools).
