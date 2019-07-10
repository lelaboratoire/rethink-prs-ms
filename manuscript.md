---
author-meta:
- Trang T. Le
- Hoyt Gong
- Patryk Orzechowski
- Elisabetta Manduchi
- Jason H. Moore
date-meta: '2019-07-10'
keywords:
- markdown
- publishing
- manubot
lang: en-US
title: Expanding polygenic risk scores to include gene-gene interactions
...






<small><em>
This manuscript
([permalink](https://lelaboratoire.github.io/rethink-prs-ms/v/1d6dde4ea1ee544ebdc203b8e865b65cf203ec53/))
was automatically generated
from [lelaboratoire/rethink-prs-ms@1d6dde4](https://github.com/lelaboratoire/rethink-prs-ms/tree/1d6dde4ea1ee544ebdc203b8e865b65cf203ec53)
on July 10, 2019.
</em></small>

## Authors



+ **Trang T. Le**<sup>☯</sup><br>
    ![ORCID icon](images/orcid.svg){height="13px" width="13px"}
    [0000-0003-3737-6565](https://orcid.org/0000-0003-3737-6565)
    · ![GitHub icon](images/github.svg){.inline_icon}
    [trang1618](https://github.com/trang1618)
    · ![Twitter icon](images/twitter.svg){.inline_icon}
    [trang1618](https://twitter.com/trang1618)<br>
  <small>
     Department of Biostatistics, Epidemiology and Informatics, Institute for Biomedical Informatics, University of Pennsylvania, Philadelphia, PA 19104
  </small>

+ **Hoyt Gong**<sup>☯</sup><br>
    ![ORCID icon](images/orcid.svg){height="13px" width="13px"}
    [0000-0001-9339-4763](https://orcid.org/0000-0001-9339-4763)
    · ![GitHub icon](images/github.svg){.inline_icon}
    [hoytgong](https://github.com/hoytgong)
    · ![Twitter icon](images/twitter.svg){.inline_icon}
    [GongHoyt](https://twitter.com/GongHoyt)<br>
  <small>
     Life Sciences and Management, Wharton School, University of Pennsylvania
  </small>

+ **Patryk Orzechowski**<sup></sup><br>
    ![ORCID icon](images/orcid.svg){height="13px" width="13px"}
    [0000-0003-3578-9809](https://orcid.org/0000-0003-3578-9809)<br>
  <small>
     Department of Biostatistics, Epidemiology and Informatics, Institute for Biomedical Informatics, University of Pennsylvania, Philadelphia, PA 19104
  </small>

+ **Elisabetta Manduchi**<sup></sup><br>
    ![ORCID icon](images/orcid.svg){height="13px" width="13px"}
    [0000-0002-4110-3714](https://orcid.org/0000-0002-4110-3714)<br>
  <small>
     Department of Biostatistics, Epidemiology and Informatics, Institute for Biomedical Informatics, University of Pennsylvania, Philadelphia, PA 19104
  </small>

+ **Jason H. Moore**<sup>†</sup><br>
    ![ORCID icon](images/orcid.svg){height="13px" width="13px"}
    [0000-0002-5015-1099](https://orcid.org/0000-0002-5015-1099)
    · ![GitHub icon](images/github.svg){.inline_icon}
    [EpistasisLab](https://github.com/EpistasisLab)
    · ![Twitter icon](images/twitter.svg){.inline_icon}
    [moorejh](https://twitter.com/moorejh)<br>
  <small>
     Department of Biostatistics, Epidemiology and Informatics, Institute for Biomedical Informatics, University of Pennsylvania, Philadelphia, PA 19104
     · Funded by National Institutes of Health Grant Nos. LM010098, LM012601, AI116794
  </small>


<sup>☯</sup> --- These authors contributed equally to this work.

<sup>†</sup> --- Direct correspondence to jhmoore@upenn.edu.


## Abstract

This study expands the PRS to account for gene-gene interaction effects.


## Introduction

[@kmJZ4oOW]

As the field of traditional genomics rapidly expands its sequencing technologies and translational abilities, novel applications of genomic data are starting to arise in addressing disease burden. 

Beginning with the completion of the Human Genome Project in 2003, increased interest in
catalouging genomic data spurred the innovation of massively parallel, chip-based genotyping
arrays. 
Leveraging these technologies, early researchers were able to characterize and catalogue gene variants across millions of individuals internationally.
In particular, the advent of projects such as the International HapMap Project [@UKO9Qhy3] and the 1000 Genomes Project sought to document haplotype [@MSp5fjte] structure (i.e. gene variants) involved in specific diseases of the human genome.
As such, the gross information of nucleotide polymorphisms within publicly available databases has rapidly increased in the beginning of the 21st century with the rise in omics sequencing capabilities.
This genomic information, coupled with additional high resolution marks for other individual biological variants (e.g. transcripts, epigenetic marks, metabolites) has been touted to further complement precision medicine approaches using genetics.

Complementing the rapid growth in our understanding of gene variants in the human genome was the emergence of using statistical techniques, formalized as genome-wide association studies (GWAS), to identify gene variants associated with common human diseases.
From a population perspective, GWA studies have sought to discern genetic connections to various phenotypes by studying genotypic variation at biallelic markers across the human genome [@iFUfVw9V; @5cdeEdUS; @12kQ0EOWQ].
Such non-candidate driven GWA studies consider gene variations (i.e. SNPs, deletions, intertions, CNVs) to resulting phenotype values to ultimately report allele frequency differences among a case and control group in the form of an odds ratio.
This technical revolution in the field of genomic medicine fueled our progressing capabilities to map associations of gene variants with disease on an increasingly granular level to single nucleotide polymorphisms (SNPs). 

Nonetheless while GWA studies indeed capture gene variants associated with a phenotype of interest on a population level, translating such results to personalized individual metrics of risk requires additional granularity on aggregating contributions of many gene variants in the form of polygenic risk scores (PRS).
In tamdem with the movement towards precision medicine, the post-GWAS era strives to bring significant population-derived gene variant into individual level metrics actionable in clinical delivery settings.
Importantly, PRS have been one such approach developed to explain individual inherited risk for disease by __placing unique weights on a selection of SNPs from the GWAS__.

[put in PRS equation]. 

[This is just one way, the most basic. many have tried to reformulate the PRS in various ways.]

[cite common ones. Which ones are most common GRS scores?]


[In this study we aim to reformulate the PRS score with MDR reduction to better detect GxG
interactions. MDR as a form of feature engineering the proper encoding for detecting GxG
interactions]

[explain more technical details of MDR]

END OF INTRO -> rest is all methods & performing MDR


## Methods

### Multilocus Risk Score (MRS)
Compute risks from significant interactions
i = 1...n subjects
p SNPs
j = 1...k significant combinations
We apply the software... [@S6nj6BFK] to obtain the significance level of each combination of SNPs.
allow for parallel computation
The maximum value of $k$ is $C^d_p$.
For each subject $i$, the $d$-way interaction risk score is calculated as
$$R_d(i) = \sum_{j = 1}^k \chi_j^2 \times HLO_j(X_{ij})$$
where $\chi_j^2$ is the test statistic of each multi-locus combination $j$ from a $\chi_j^2$ test with one degree of freedom for the simulated binary trait, $HLO_j$ is the $j^{th}$ re-coded HLO-matrix and $X_j$ is one of $k$ combination of SNPs.




### Simulated data
[Patryk...]

For each simulated and real-world dataset, after randomly splitting the entire data in two smaller sets (80% training and 20% holdout), we built the MRS model on training data to obtain the $\chi^2$ coefficients and calculated risk score for each individual in the holdout set.
We assess the performance of the MRS by comparing the area under the Receiving Operator Characteristic curve (auROC) with that of the standard GRS method where




## Results
### Information gain

### iPRS outperforms standard PRS

![MM12 produces improved auROC in the majority (335 green lines) of the 450 simulated datasets (each line represents a dataset). In many datasets, the original method performs poorly (auROC < 60%) while the new method yields auROC over 90%. This improvement in performance can be seen at the second peak (~50% auROC increase) in the density of the difference between two methods (right).](images/ori_vs_MM12D_auROC_.pdf)








## References {.page_break_before}

<!-- Explicitly insert bibliography here -->
<div id="refs"></div>
