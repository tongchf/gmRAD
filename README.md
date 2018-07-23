# gmRAD: an integrated  pipeline to call SNP genotypes across a hybrid population for genetic mapping  with RADseq data
# Introduction
gmRAD is used to call SNP genotypes across a hybrid population with RAD-seq data for genetic linkage mapping. It takes five steps as following to finish the whole work.  
        1. Clustering the first reads of each parent;  
        2. Building the reference sequence within a cluster for each parent;  
        3. Generating the parental SNP catalogs;  
        4. Calling SNP genotypes across the individuals in the whole population;  
        5. Filtering the SNP data by considering segregation ratio and missing data.  
# Usage
To run gmRAD, users should install the three prerequisite packages: [LOCAS](http://ab.inf.uni-tuebingen.de/software/locas/), [BWA](http://bio-bwa.sourceforge.net/) and [SAMtools (with BCFtools)](http://samtools.sourceforge.net/), and prepare a parameter setting file, namely `parameter.ini`. The parameter file contains three parts, i.e., folders, parameters and fastq files. As the first part, 'folders' gives the paths to gmRAD itself, LOCAS, SAMtools, BCFtools and fastq files. The second part 'parameters' includes the number of threads used for parallel computing, the edit distance allowed in clustering and mapping reads, the estimated percent of genome repeat regions, the minimum score of an SNP genotype, the percent of non-missing genotypes required at an SNP and the minimum p-value allowed for testing the segregation ratio of an SNP. The third part 'fastq files' presents the first read files and the second read files for all individuals including the two parents.   
