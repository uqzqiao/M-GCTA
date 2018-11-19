# M-GCTA #
*This document is under developement. Your ideas and suggestions are always welcome! 

M-GCTA is an user-friendly M-GCTA software package, which can be used to estimate the proportion of phenotypic variance due to tagged maternal (or paternal) and offspring genetic effects on offspring phenotypes using large studies where genome-wide genotype data are available on mother- (or father-) offspring pairs. 

## Getting started ##

### Download ###
The executable files are provided in this directory. See ```M-GCTA_beta_0.1.0.tar.gz```  
The executable files below only support a 64-bit operating system on the x86_64 CPU platform.
* The current version is beta 0.1.0; 64-bit
* The source code will be released soon.

### Who do I talk to? ###
If you have any questions or trouble getting the method to work, try first to check if it is reported or addressed in the **GCTA website** [http://cnsgenomics.com/software/gcta/#Overview] and the **GCTA forum** [http://gcta.freeforums.net/thread/1/welcome-gcta-discussion-board]. M-GCTA is built on GCTA Version 1.26.0 and you may find it familiar to use if you are an experienced GCTA user. 

In emergencies, please contact Zhen Qiao (z.qiao1@uq.edu.au). I am currently preparing for my PhD thesis, apologzie for any (potential) delay in response. 

### How to cite this software? ###
The manuscript will be submitted soon. 

## Using M-GCTA ## 

### Main functions ###
1. Quality control (QC): M-GCTA includes several options for data cleaning and quality control, including the ability to detect and automatically remove cryptically related pairs of individuals who are meant to be unrelated. 

2. GREML analysis: M-GCTA allows users to construct genetic relationship matrices (GRM) indexing genetic similarity across the genome between parents and offspring, enabling the estimation of variance due to maternal (or alternatively paternal) and offspring genetic effects. 

Of note: M-GCTA is built on the basis of GCTA, so it inherently adopted all GCTA functions. The users can tailor the analysis to their needs, but please bear in mind that this is a subject for further inquiry. 

### QC step ###
This step is to extract unrelated mother-/father-offspring pairs.

For mother-offspring pairs

`mgcta64 --bfile test --prep-mat --grm-cutoff 0.025 --founders --pheno test.phen --mpheno 2 --thread-num  10 --make-bed --out test`

For father-offspring pairs

`mgcta64 --bfile test --prep-pat --grm-cutoff 0.025 --founders --pheno test.phen --mpheno 2 --thread-num  10 --make-bed --out test`

 *--prep-mat: extracted mother-offspring pairs. If --pheno is presented, it will extracted mother-offspring pairs for which the offspring have phenotype data.
 
 *--prep-pat: similar as --prep-mat, but for father-offspring pairs.
 
 *--founders: the allele frequencies will be calculated based on founders only.
 
 *--grm-cutoff: the threshold used to remove related individuals (in mothers'/fathers' and children's GRM, as well as in the GRM between mothers/fathers and the offspring).
 
 *phenotype file format: test.phen (no header line; columns are family ID, individual ID and phenotypes)
```
F001  I0101  100
F002  I0201  101
F003  I0301  99
..
..
```
 
### GREML analysis ###
The step is to perform GREML analysis to estimate the proportion of phenotypic variance explained by maternal genotype, the child’s genotype, the covariance between the maternal and child’s genotype and an environmental component.
To be specific, this step first generates the GRM for all mother-/father-offspring pairs, and then extracts P/O/D grm from the whole GRM, and then performs the REML analysis.

For mother-offspring pairs

`mgcta64 --bfile test --mat --pheno test.phen --mpheno 1 --thread-num  10 --founders --out test`

For father-offspring pairs

`mgcta64 --bfile test --pat --pheno test.phen --mpheno 1 --thread-num  10 --founders --out test`

 *--mat: a flag to partition the phenotypic variance in offspring into components attributable to mothers’ genotypes, the children’s genotypes, and the covariance between the two.
 *--pat: similar as --mat, but for father-offspring pairs.
 
 *--pat: similar as --mat, but for father-offspring pairs.
 
 ..
 
