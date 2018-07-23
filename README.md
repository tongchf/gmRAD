# gmRAD: an integrated  pipeline to call SNP genotypes across a hybrid population for genetic mapping  with RADseq data
# Introduction
gmRAD is used to call SNP genotypes across a hybrid population with RAD-seq data for genetic linkage mapping. It takes five steps as following to finish the whole work.  
        1. Clustering the first reads of each parent;  
        2. Building the reference sequence within a cluster for each parent;  
        3. Generating the parental SNP catalogs;  
        4. Calling SNP genotypes across the individuals in the whole population;  
        5. Filtering the SNP data by considering segregation ratio and missing data.  
# Usage
To run gmRAD, users should install the three prerequisite packages: [LOCAS](http://ab.inf.uni-tuebingen.de/software/locas/), [BWA](http://bio-bwa.sourceforge.net/) and [SAMtools (with BCFtools)](http://samtools.sourceforge.net/), and prepare a parameter setting file, namely `parameter.ini`. The parameter file contains three parts, i.e., folders, parameters and fastq files. As the first part, 'folders' gives the paths to gmRAD itself, LOCAS, SAMtools, BCFtools and fastq files. The second part 'parameters' includes the number of threads used for parallel computing, the edit distance allowed in clustering and mapping reads, the estimated percent of genome repeat regions, the minimum score of an SNP genotype, the percent of non-missing genotypes required at an SNP and the minimum p-value allowed for testing the segregation ratio of an SNP. The third part 'fastq files' presents the first read files and the second read files for all individuals including the two parents.  A typical parameter file looks as following:  

        [folders]  
        GMRAD_FOLD:/home/tong/gmRAD  
        LOCAS_FOLD:/home/tong/locas_binaries  
        BWA_FOLD:/home/tong/bwa-0.7.5a  
        SAMTOOLS_FOLD:/home/tong/samtools-1.4.1  
        BCFTOOLS_FOLD:/home/tong/bcftools-1.4.1  
        RADDATA_FOLD:/home/tong/exampledata  

[parameters]
THREADS: 4
EDITDST: 5
GENOMEREPEAT: 30
GQ: 30
MISPCT: 90
PVALUE: 0.01

[fastq files]
FEMALEPARENT: female_1.fq   female_2.fq
MALEPARENT: male_1.fq   male_2.fq

PROGENY1:  sample01_1.fq  sample01_2.fq
PROGENY2:  sample02_1.fq  sample02_2.fq
PROGENY3:  sample03_1.fq  sample03_2.fq
PROGENY4:  sample04_1.fq  sample04_2.fq
PROGENY5:  sample05_1.fq  sample05_2.fq
PROGENY6:  sample06_1.fq  sample06_2.fq
PROGENY7:  sample07_1.fq  sample07_2.fq
PROGENY8:  sample08_1.fq  sample08_2.fq
PROGENY9:  sample09_1.fq  sample09_2.fq
PROGENY10:  sample10_1.fq  sample10_2.fq
PROGENY11:  sample11_1.fq  sample11_2.fq
PROGENY12:  sample12_1.fq  sample12_2.fq
PROGENY13:  sample13_1.fq  sample13_2.fq
PROGENY14:  sample14_1.fq  sample14_2.fq
PROGENY15:  sample15_1.fq  sample15_2.fq
PROGENY16:  sample16_1.fq  sample16_2.fq
PROGENY17:  sample17_1.fq  sample17_2.fq
PROGENY18:  sample18_1.fq  sample18_2.fq
PROGENY19:  sample19_1.fq  sample19_2.fq
PROGENY20:  sample20_1.fq  sample20_2.fq

