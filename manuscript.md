---
author-meta:
- Trang T. Le
- Hoyt Gong
- Patryk Orzechowski
- Elisabetta Manduchi
- Jason H. Moore
date-meta: '2019-07-17'
keywords:
- markdown
- publishing
- manubot
lang: en-US
title: Expanding polygenic risk scores to include gene-gene interactions
...






<small><em>
This manuscript
([permalink](https://lelaboratoire.github.io/rethink-prs-ms/v/0d5844beb46fb1d097035c9023061482ff255c79/))
was automatically generated
from [lelaboratoire/rethink-prs-ms@0d5844b](https://github.com/lelaboratoire/rethink-prs-ms/tree/0d5844beb46fb1d097035c9023061482ff255c79)
on July 17, 2019.
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

As the field of traditional genomics rapidly expands its sequencing technologies and translational abilities, novel applications of genomic data are starting to arise in addressing disease burden. 
Beginning with the completion of the Human Genome Project in 2003, increased interest in cataloguing genomic data spurred the innovation of massively parallel, chip-based genotyping arrays. 
Leveraging these technologies, early researchers were able to characterize and categorize gene variants across millions of individuals internationally.
In particular, the advent of projects such as the International HapMap Project [@UKO9Qhy3] and the 1000 Genomes Project sought to document haplotype [@MSp5fjte] structure (i.e. gene variants) involved in specific diseases of the human genome.
As such, the gross information of nucleotide polymorphisms within publicly available databases has rapidly increased in the beginning of the 21st century with the rise in omics sequencing capabilities.
This genomic information, coupled with additional high resolution marks for other individual biological variants (e.g. transcripts, epigenetic marks, metabolites) has been touted to further drive precision medicine approaches using genetics.

Complementing the rapid growth in our understanding of gene variants in the human genome was the emergence of using statistical techniques, formalized as genome-wide association studies (GWAS), to identify gene variants associated with common human diseases.
From a population perspective, GWA studies have sought to discern genetic connections to various phenotypes by studying genotypic variation at biallelic markers across the human genome [@iFUfVw9V; @5cdeEdUS; @12kQ0EOWQ].
Such non-candidate driven GWA studies consider gene variations (i.e. SNPs, deletions, intertions, CNVs) to resulting phenotype values to ultimately report allele frequency differences among a case and control group in the form of an odds ratio.
This technical revolution in the field of genomic medicine fueled our progressing capabilities to map associations of gene variants with disease on an increasingly granular level to single nucleotide polymorphisms (SNPs). 

In tandem with the movement towards precision medicine, the post-GWAS era strives to bring significant population-derived gene variants into individual level metrics actionable in health delivery settings.
While GWA studies indeed capture gene variants associated with a phenotype of interest on a population level, translating such results to personalized individual metrics of risk requires additional granularity on aggregating contributions of many gene variants in the form of polygenic risk scores (PRS).
Importantly, PRS have been one such approach developed to explain inherited risk for disease in an individual by representing a weighted sum aggregate of risk alleles based on measured loci effect contributions derived from GWAS studies [@1Dlv3tAGh; @1GK3F1BxE]. 
(sentence on origin and history & cite it)
In quantifying the effect of particular combinations of genetic SNP variants towards risk prediction, PRS offers a probabilisitic susceptibility value of an individual to disease. 
Such genetic risk estimation scores are central to clinical decision-making, serving to reinforce individual health management in heritable disease detection and early prevention of various adult-onset conditions. 
The utility of PRS scores have been demonstrated in previous studies towards disease risk stratification across leading heritable causes of death in the developed world [@mwTa2RUK; @JjyayEbB; @Z12fynub; @gkABDVTx]

$PRS=\sum_{i=1}^{n} \beta_i \cdot SNP_i$

Where $\beta$ refers to the weighted risk contribution of the loci gene variant and $n$ refers to the total quantity of GWAS *hits* across the genome. 
Various approaches towards predicting risk of the same disease exist across PRS studies based on the above equation; models may vary according to the $\beta$ weight according to the specific type of statistical model used to combine risk of individual variations, the $n$ with respect to the specification of genetic variants considered, and the ability of the PRS to generalize to the entire population [@1Dlv3tAGh].

Historically, PRS models have previously characterized genomic architechture in a dichotimous division of Mendelian monogenic and polygenic inheritance, in which either one or many gene perturbations give rise to disease phenotypes in an individual, respectively [@KQA5cNEZ; @1GK3F1BxE].
Yet while such classification models arose from former sequencing technology and study design, a more realistic genetic archtechture of common adult-onset disease acknowledges dynamic interactions among a continuum of common low-risk to rare high-risk gene variants to cumultatively drive overall risk of an individual [@LpJAX4ST].
When only considering rare (minor allele frequency, MAF < 0.5%), high-risk gene variants, such genomic variation only contributes approximately 1-10% towards adult-onset disease incidence [@1GK3F1BxE; @wBOguD8h].
Often, more relevant and complete sources of genetic risk is captured from complex smaller interactions of both common (MAF >5%) and low-frequency (MAF >0.5% and <5%) genetic variants each contributing individual, appreciable effects [@132N8vjSs; @mOp2SAPs].
Existing standard multivariate categorical data analysis approaches fall short in handling such enormous possible gene interaction combinations with both linear and nonlinear effects. 
In this context, more robust and efficient methods towards a polygeneic risk calculation are necessary in capturing the overlap between context-dependent effects of both rare and common alleles on human genetic disorder.

With respect to better understanding the epistasis across an individual's genome, various statistical models have been designed with the intent of capturing high dimensional gene-gene (GxG) interactions. 
The Multifactor Dimensionality Reduction (MDR) model is one such model that addresses these challenges and has been extensively applied to detect nonlinear complex GxG interactions associated with individual disease. 
By isolating a specific pool of genetic factors from all polymorphism and cross-valiating prediction scores averaged across identified high risk multi-locus genotypes, the original MDR approach is able to categorize multi-loci genotypes into two groups of risk based on some threshold value [@E26QhGxD]. 
MDR has been effective in identifying epistasis that may characterize genomic susceptibility in common diseases such as hypertension [@EDApk3zM] and Type 2 diabetes [@oTOXwsyb].

While created with the primary intention towards GxG interaction detection, the MDR model has additionally demonstrated applicability as a risk score calculation model in constructing PRS scores [@93PfLXPZ].
Modifications built on top of the MDR framework have been proposed in order to better capture multiple significant epistasis models and potential missed interactions owning to limiations of the original model in the higher dimensions.
Model-Based Multifactor Dimensionality Reduction (MB-MDR) was formulated as a flexible GxG detection framework for dichotomous traits and unrelated individuals [@kN4MaLuT]. 
Rather than a direct comparison against a threshold level in the original MDR method, MB-MDR merges multi-locus genotypes exhibiting significantly high or low risk levels through association testing and adds an additional category representing no evidence of risk. 

In this study we aim to reformulate the PRS using the MB-MDR approach in observing the model's separability of results on an evidence-based simulated dataset from HIBACHI.


## Methods

### Multifactor Dimensionality Reduction (MDR) and model-based MDR (MB-MDR)

MB-MDR is a feature selection method that detects multiple sets of significant gene-gene interactions in relation to a trait of interest, while efficiently controlling type I error rates.


### Multilocus Risk Score (MRS)
Compute risks from significant interactions
i = 1...n subjects
p SNPs
j = 1...k 
We apply the MB-MDR software [@S6nj6BFK] to obtain the significance level of each combination of SNPs.
[allow for parallel computation]
If we let $k$ be the number of significant combinations then, for each subject $i$, the $d$-way interaction risk score is calculated as
$$MRS_d(i) = \sum_{j = 1}^k \chi_j^2 \times HLO_j(X_{ij})$$
where $\chi_j^2$ is the test statistic of each genotype combination $j$ from a $\chi_j^2$ test with one degree of freedom for the simulated binary trait, $X_{ij}$ is the $j^{th}$ genotype combinations of subject $i$ and $HLO_j$ represents the $j^{th}$ re-coded HLO-matrix (1 = High, -1 = Low, 0 = No evidence).
For example, if [...].
The maximum value of $k$ is $C^d_p$ (when no threshold is imposed).
 
The 
$$MRS(i) = \sum_{d = 1}^{\bar{d}} MRS_d(i)$$
In this study, we consider 1-way and 2-way interactions, i.e. $\bar{d} = 2$, and hence, the combined risk is simply the total of the first two: $MRS = MRS_1 + MRS_2$.


### Simulated data
[Patryk...]

[objective: simulate a diverse collection of datasets]

For each simulated and real-world dataset, after randomly splitting the entire data in two smaller sets (80% training and 20% holdout), we built the MRS model on training data to obtain the $\chi^2$ coefficients and calculated risk score for each individual in the holdout set.
We assess the performance of the MRS by comparing the area under the Receiving Operator Characteristic curve (auROC) with that of the standard GRS method where

### Mutual information and information gain
We measure the interaction information (i.e. degree of synergistic effects of genetic attributes on the phenotype) of each dataset by summing up the pairwise information gain between all pairs of genetic attributes.
Specifically,... phenotypic class $C$...
$$IG(G_1, G_2; C) = I(G_1, G_2; C) - I(G_1;C) - I(G_2,C),$$
where $I$ represents the mutual information between two attributes.

two-way epistatic interactions




## Results

### MRS outperforms standard PRS

![MRS produces improved auROC in the majority (335 green lines) of the 450 simulated datasets (each line represents a dataset). In many datasets, the original method performs poorly (auROC < 60%) while the new method yields auROC over 90%. This improvement in performance can be seen at the second peak (~50% auROC increase) in the density of the difference between two methods (right).](images/ori_vs_MRS_auROC_.svg){#fig:auroc_mrs_prs}

To assess whether this improvement in performance correlates with , in the following section, we untangled the two components in MRS and apply information theory to 

### Assess improvement in performance

As the amount of main effects increases (Fig. {@fig:improvements} left), MRS1 increasingly performs better than PRS, which is likely because encodings are inferred (top left).
Meanwhile, MRS2's accuracy remain similar to that of PRS (middle left).
On the other hand, when the amount of interaction effects increases (right), MRS1 performs mostly on par to PRS while MRS2
Combinging the gain from both MR1 and MRS2, MRS's performance progressively increases compared to the standard PRS.

![Combining 1-way (MRS1) and 2-way (MRS2) risk scores, MRS shows increasing outperformance to standard PRS as dataset contains more main and interaction effects](images/improvements_train_ms.svg){#fig:improvements}



## References {.page_break_before}

<!-- Explicitly insert bibliography here -->
<div id="refs"></div>
