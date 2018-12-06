# gmRAD: an integrated  pipeline to call SNP genotypes across a hybrid population for genetic mapping  with RADseq data
# Introduction
gmRAD is used to call SNP genotypes across a hybrid population with RAD-seq data for genetic linkage mapping. It takes five steps as following to finish the whole work.  
        1. Clustering the first reads of each parent;  
        2. Building the reference sequence within a cluster for each parent;  
        3. Generating the parental SNP catalogs;  
        4. Calling SNP genotypes across the individuals in the whole population;  
        5. Filtering the SNP data by considering segregation ratio and missing data.  
# Usage
To run gmRAD, users should install the three prerequisite packages: [LOCAS](http://ab.inf.uni-tuebingen.de/software/locas/), [BWA](http://bio-bwa.sourceforge.net/) and [SAMtools (with BCFtools)](http://samtools.sourceforge.net/), and prepare a parameter setting file, namely `parameters.ini`. The parameter file contains three parts, i.e., folders, parameters and fastq files. As the first part, 'folders' gives the paths to gmRAD itself, LOCAS, SAMtools, BCFtools and fastq files. The second part 'parameters' includes the number of threads used for parallel computing, the hamming distance for clustering the first reads, the edit distance for filtering mapped reads, the coverage depth of an allele for a heterozygote, the estimated percent of genome repeat regions, the minimum score of an SNP genotype, the percent of non-missing genotypes required at an SNP and the minimum p-value allowed for testing the segregation ratio of an SNP. The third part 'fastq files' presents the first read files and the second read files for all individuals including the two parents.  A typical parameter file looks as following:  

        [folders]  
        GMRAD_FOLD:/home/tong/gmRAD-1.1  
        LOCAS_FOLD:/home/tong/locas_binaries  
        BWA_FOLD:/home/tong/bwa-0.7.17  
        SAMTOOLS_FOLD:/home/tong/samtools-1.9  
        BCFTOOLS_FOLD:/home/tong/bcftools-1.9  
        RADDATA_FOLD:/home/tong/exampledata  
          
        [parameters]  
        THREADS: 4  
        HAMMDST: 5
        EDITDST: 5  
        ALLELDP: 3
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
        .......................................  
        PROGENY19:  sample19_1.fq  sample19_2.fq  
        PROGENY20:  sample20_1.fq  sample20_2.fq  
  
  Additionally, users need to install several perl modules, including `Parallel::ForkManager`, `Excel::Writer::XLSX`, `Switch` and `Statistics::Distributions`. The modules can be easily installed with the module of [cpan](https://www.cpan.org/) if it is installed in advance.  
  When the required software packages are installed and the parameter file is parepared and saved in a work directory, you can go to the work directory and get started with the command:  
  `perl PathToGmRAD/gmRAD.pl`
    
  Since it will take quite a few hours or even several days to finish a pratical computing, we usually run the command in background as  
  `nohup perl PathToGmRAD/gmRAD.pl &`
  
  You can run with the 'help' option (`perl PathToGmRAD/gmRAD.pl -h`) to show the usage of gmRAD:

        Usage: perl gmRAD.pl [Options]
        
        Options:
                --nocluster  skip the step for clustering the first reads of each parent  
                --nobuild    skip the step for building the parental reference sequences  
                --nocatalog  skip the step for generating parental SNP catalogs  
                --nocall     skip the step for calling SNP genotypes for all progeny
                --nofilter   skip the step for filtering the SNP genotype data  
                --help|h     help  
It can be seen that users can perform the analytical steps independently by adding some options described as above if some prerequisite files are avaiable.  For example, only to perform the clustering step and skip others, please type command:   
`perl PathToGmRAD/gmRAD.pl --nobuild --nocatalog --nocall --nofilter`  
To perform the second step only, we just type the following command:  
`perl PathToGmRAD/gmRAD.pl --nocluster --nocatalog --nocall --nofilter` 

# Test Data
       
We provide a test data for users to quickly grasp the use of gmRAD. All reads data files can be downloaded in a compressed file as [exampledata.tar.gz](http://www.bioseqdata.com/gmRAD/exampledata.tar.gz), including 2 parents and their 20 progeny samples. With the parameter file [parameters.ini](https://github.com/tongchf/gmRAD/blob/master/parameters.ini) attached at this site, we can perform the analysis process by inputting the command: `perl PathToGmRAD/gmRAD.pl`. When the computing finishes, we can obtain 6 segregation types of SNP genotype files, including aaxab_pct90pv01.txt, aaxbc_pct90pv01.txt, abxaa_pct90pv01.txt, abxab_pct90pv01.txt, abxac_pct90pv01.txt and abxcc_pct90pv01.txt, which contain 130, 34, 136, 28, 14 and 39 SNPs, respectively. In this test example, we cannot find the genotype file "abxcd_pct90pv01.txt", because no SNPs are generated in the segregation type of abxcd.

# Notes

1. Version 1.0 works with bwa v0.7.5a and samtools (bcftools) v1.4.1  
2. Version 1.1 works with bwa from v0.7.5a to 0.7.17 and samtools (bcftools) from v1.4.1 to 1.9
3. Version 1.2 provides parameter 'ALLELDP' for setting the coverage depth of an allele at heterzygous SNPs.

# References

Dan Yao, Hainan Wu, Yuhua Chen,Wenguo Yang, Hua Gao, ChunfaTong*. 2018. gmRAD: an integrated SNP calling pipeline for genetic mapping with RADseq across a hybrid population. Briefings in Bioinformatics, doi: 10.1093/bib/bby114 
