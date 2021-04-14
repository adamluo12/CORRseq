# CORRseq and SARAseq
Copy number variation detection by whole-exome-sequencing (WES) data.
## Author
Xizhi Luo, Fei Qin, Guoshuai Cai, Feifei Xiao
## Description
We have previously shown evidence of the genomic correlation structure in SNP array data and developed a novel chromosomal breakpoint detection algorithm, LDcnv, which showed significantly improved detection power through integrating the correlation structure in a systematic modeling manner. However, it remains unexplored whether the genomic correlation exists in WES data and how such correlation structure integration can improve CNV detection accuracy. 
Here, we proposed a correlation-based method, CORRseq, as a novel release of the LDcnv algorithm in profiling WES data. We also developed an alternative independent-based method in parallel, so as referred to SARAseq, which was built upon on our existing method modSaRa.
## General workflow
CORRseq requires WES read count data from both testing and control samples as inputs. Read counts are normalized using a median normalization approach to adjust exon length, GC-content, and mappability biases. Logarithm transformation of the ratios of normalized data from the testing and the pooled control samples is calculated. CORRseq implements a correlation-based algorithm (LDcnv) to identify CNVs. 
SARAseq only requires WES read count data from testing samples. Read counts are normalized using a PLF-based approach to mitigate observable biases (GC content, amplification efficiency, and exon size) and latent systemic biases and estimate the expected “null” read counts. Logarithm of the observed read counts and expected “nulls” are calculated. SARAseq uses an algorithm assuming independence (modSaRa) for the CNV identification.
![workflow](workflow.jpg)

### Prerequisite
CORRseq and SARAseq
```r
install.packages("devtools")
library(devtools)
install_github("FeifeiXiaoUSC/modSaRa",subdir="package")
install_github("FeifeiXiaoUSC/modSaRa2",subdir="Package")
install_github("adamluo12/LDcnv")
install_github("adamluo12/CORRseq")
install_github("adamluo12/SARAseq")
```
CODEX2 (https://github.com/yuchaojiang/CODEX2)
```r
devtools::install_github("yuchaojiang/CODEX2/package")
```
EXCAVATOR2:https://sourceforge.net/projects/excavator2tool/files/EXCAVATOR2_Package_v1.1.2.tgz/download
samtools: https://github.com/samtools/samtools/blob/develop/INSTALL

### Getting raw read count data
Using samtools (follow EXCAVATOR2's mannual), this requires linux enviroment (e.g., ubuntu OS).
```r
EXCAVATOR2> perl EXCAVATORDataPrepare.pl ExperimentalFilePrepare.w50000.txt processors 6 --target MyTarget_w50000 --assembly hg19
```
Using Rsamtools (follow CODEX2'S manual http://htmlpreview.github.io/?https://github.com/yuchaojiang/CODEX2/blob/master/demo/CODEX2.html)

Example outputs
```r
> Y_qc[1:5,1:5]
                  NA06994 NA07000 NA07056 NA07357 NA10847
1:2938187-2939417    1093     831     541     767    1072
1:3102653-3103043     152     356     136     291     160
1:3160585-3160735      82      63      33      90      90
1:3301632-3301902     264     227     157     181     245
1:3327905-3329375     969     962     405     655     867
```









