---
author-meta:
- Trang T. Le
- Hoyt Gong
- Patryk Orzechowski
- Elisabetta Manduchi
- Jason H. Moore
date-meta: '2019-08-02'
keywords:
- markdown
- publishing
- manubot
lang: en-US
title: Expanding polygenic risk scores to include automatic genotype encodings and
  gene-gene interactions
...






<small><em>
This manuscript
([permalink](https://lelaboratoire.github.io/rethink-prs-ms/v/76100775f1d55d7efad51a80d6eb46447a386658/))
was automatically generated
from [lelaboratoire/rethink-prs-ms@7610077](https://github.com/lelaboratoire/rethink-prs-ms/tree/76100775f1d55d7efad51a80d6eb46447a386658)
on August 2, 2019.
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
Polygenic Risk Scores (PRS) are aggregation of genetic risk factors of specific diseases and have been successfully used to identify subgroups of individuals who are more susceptible to those diseases.
While several studies have focused on identifying the correct genetic variants to include in PRS, most existing statistical models focus on the marginal effect of the variants on the phenotypic outcome but do not account for the effect of gene-gene interactions.
Here, we propose a novel calculation of the risk score that expands beyond marginal effect of individual variants on the phenotypic outcome.
The Multilocus Risk Score (MRS) method effectively selects alternative genotype encodings and captures epistatic gene-gene interactions by utilizing an efficient implementation of the model-based Multifactor Dimensionality Reduction technique.
On a diverse collection of datasets, MRS outperforms the standard PRS in the majority of the cases, especially when at least two-way interactions between genes are present.
Our findings suggest that more precise models that incorporate epistatic interactions are necessary and will yield greater utility for polygenic risk profiling.

## Introduction

As the field of traditional genomics rapidly expands its sequencing technologies and translational abilities, novel applications of genomic data are starting to arise in addressing disease burden. 
Beginning with the completion of the Human Genome Project in 2003, increased interest in cataloguing genomic data spurred the innovation of massively parallel, chip-based genotyping arrays. 
Leveraging these technologies, early researchers were able to characterize and categorize gene variants across millions of individuals internationally.
In particular, the advent of projects such as the International HapMap Project and the 1000 Genomes Project sought to document genetic variants involved in specific diseases of the human genome through genotyping and whole-genome sequencing techniques, respectively [@UKO9Qhy3; @MSp5fjte].
As such, the gross information of nucleotide polymorphisms within publicly available databases has rapidly increased in the beginning of the 21st century with the rise in omics sequencing capabilities.
This genomic information, coupled with functional genomics data on the transcriptome, epigenome and metabolome, has been touted to further drive precision medicine approaches using genetics.

Complementing the rapid growth in our understanding of human genetic variation was the emergence of genome-wide association studies (GWAS) in the early 2000s to identify gene variants associated with common human diseases. 
Non-candidate-driven in design, these observational studies carry out chip array genotyping across population subsamples to subsequently assay for phenotype signal association via statistical approaches in silico. 
GWAS have primarly sought to discern genetic association with various phenotypes of interest by studying single nucleotide polymorphisms (SNPs) and other DNA variants across the human genome [@iFUfVw9V; @5cdeEdUS; @12kQ0EOWQ].

In tandem with the movement towards precision medicine, the post-GWAS era strives to bring relevant population-derived gene variants into individual level metrics actionable in health delivery settings.
While GWAS indeed capture gene variants associated with a phenotype of interest on a population level, translating such results to personalized individual metrics of risk requires aggregating contributions of many gene variants in the form of polygenic risk scores (PRS).
Importantly, PRS provide an ability to explain inherited risk for disease in an individual by representing a weighted sum aggregate of risk alleles based on measured loci effect contributions derived from GWAS [@1Dlv3tAGh; @1GK3F1BxE]. 
In quantifying the effect of particular combinations of genetic SNP variants towards risk prediction, PRS offers a probabilisitic susceptibility value of an individual to disease. 
Such genetic risk estimation scores are central to clinical decision-making, serving to reinforce individual health management in heritable disease detection and early prevention of various adult-onset conditions. 
The utility of PRS scores have been demonstrated in previous studies towards disease risk stratification across leading heritable causes of death in the developed world [@mwTa2RUK; @JjyayEbB; @Z12fynub; @gkABDVTx]

For each SNP $j$ of an individual's genome of $n$ possible SNPs for analysis, the PRS score is calculated via a summation across $k$ selected SNPs as
$$PRS=\sum_{j=1}^{k} \beta_j \cdot SNP_j$$
where $\beta_j$ is the weighted risk contribution of the $j^\textrm{th}$ SNP derived from the association test parameters and $SNP_j$ represents the number of minor alleles (0, 1, or 2) at the $j^\textrm{th}$ locus.
Various approaches towards predicting risk of the same disease exist across PRS studies based on the above equation; models may vary according to the specific statistical model used to produce the weights $\beta_j$ for individual genetic variations, the $k$ with respect to the specification of genetic variants considered, and the ability of the PRS to generalize to the entire population [@1Dlv3tAGh].
Historically, PRS models have previously characterized genomic architecture in a dichotimous division of Mendelian monogenic and polygenic inheritance, in which either one or many gene perturbations give rise to disease phenotypes in an individual, respectively [@KQA5cNEZ; @1GK3F1BxE].

However, while such former PRS models arose from older sequencing technology and study design, a more realistic genetic architechture of common adult-onset disease acknowledges dynamic interactions among a continuum of common low-risk to rare high-risk gene variants to cumulatively drive overall risk of an individual [@LpJAX4ST].
When only considering rare (minor allele frequency, MAF < 0.5%), high-risk gene variants, such genomic variation only contributes approximately 1-10% towards adult-onset disease incidence [@1GK3F1BxE; @wBOguD8h].
Often, more relevant and complete sources of genetic risk is captured from complex smaller interactions of both common (MAF > 5%) and low-frequency (MAF > 0.5% and < 5%) genetic variants each contributing individual, appreciable effects [@132N8vjSs; @mOp2SAPs].
Existing standard multivariate categorical data analysis approaches fall short in handling such enormous possible gene interaction combinations with both linear and nonlinear effects. 
In this context, more robust and efficient methods towards a polygeneic risk calculation are necessary in capturing the overlap between context-dependent effects of both rare and common alleles on human genetic disorder.

With respect to better understanding the epistasis across an individual's genome, various statistical models have been designed with the intent of capturing high dimensional gene-gene (GxG) interactions. 
The Multifactor Dimensionality Reduction (MDR) method is one such nonparametric, model-free framework that addresses these challenges and has been extensively applied to detect nonlinear complex GxG interactions associated with individual disease [@E26QhGxD]. 
By isolating a specific pool of genetic factors from all polymorphism and cross-valiating prediction scores averaged across identified high risk multi-locus genotypes, the original MDR approach is able to categorize multi-loci genotypes, whether in the 1D or 2D, into two groups of risk based on some threshold value. 
While created with the primary intention towards GxG interaction detection by reducing dimensionality interactively in inferring genotype encodings, the MDR model has additionally demonstrated applicability as a risk score calculation model in constructing PRS scores [@93PfLXPZ].

Modifications built on top of the MDR framework have been proposed in order to better capture multiple significant epistasis models and potential missed interactions owning to limitations of the original model in the higher dimensions.
Model-Based Multifactor Dimensionality Reduction (MB-MDR) was formulated as a flexible GxG detection framework for dichotomous traits and unrelated individuals [@kN4MaLuT]. 
Rather than a direct comparison against a threshold level in the original MDR method, MB-MDR merges multi-locus genotypes exhibiting significant High or Low risk levels through association testing and adds an additional 'No evidence of risk' categorization. 
In comparison to the standard MDR framework which reveals at most one optimal epistasis model, the MB-MDR method flexibly weighs multiple models by producing a model list ranked with respect to statistical parameters.

In the present work, we aim to reformulate the PRS leveraging the MB-MDR approach to better capture alternative encodings and epistatic interactions of individual disease risk in a novel Multilocus Risk Score (MRS).
In observing prediction accuracy results on an evidence-based simulated dataset from HIBACHI, we demonstrate the improved performance of our multi-model weighted epistasis framework with inferred genotype encodings over existing PRS methods, showing great potential for more accurate identification of high risk individuals for a specific complex disease.

## Methods

### Multifactor Dimensionality Reduction (MDR) and model-based MDR (MB-MDR)
MDR is a nonparametric method that detects multiple genetic loci associated with a clinical outcome by reducing the dimension of a genotype dataset through pooling multilocus genotypes into high-risk and low-risk groups [@E26QhGxD].
Extended from the original MDR algorithm, MB-MDR was first introduced in 2009, and its current implementation efficiently and effectively detects multiple sets of significant gene-gene interactions in relation to a trait of interest while efficiently controlling type I error rates.

In addition to the test statistic and P values associated with each genotype combination, another important output of MB-MDR is the HLO matrices.
Briefly, in the case of a binary trait, for each genotype combination, an HLO matrix is a 3 x 3 matrix with each cell containing H (high), L (low) or O (no evidence), indicating risk of an individual whose genotype pairs fall into that cell [@S6nj6BFK].
For an example binary outcome problem, a genotype combination $SNP_1$ and $SNP_2$ will have an HLO matrix that looks like
$$ \begin{array}{l|ccc}
& SNP_1 = 0 & SNP_1 = 1 & SNP_1 = 2   \\
\hline
SNP_2 = 0 & O        & O        & O \\
SNP_2 = 1 & O        & H        & L \\
SNP_2 = 2 & O        & L        & H
\end{array}
$$
We discuss in the following subsection how these values were utilized in the formulation of the Multilocus Risk Score (MRS).

[More on the significance of SNP combination vs. significance of H/L/O here...]

### Multilocus Risk Score (MRS)
We apply the MB-MDR software [@S6nj6BFK; @16AnEAMje] v.4.4.1 to simulated datasets of $n$ individuals, $m$ SNPs to obtain the significance level of each combination of SNPs.
We let $k_d$ denote the number of significant combinations for a specific model dimension $d$ (e.g. $d = 2$ results in pairs of SNPs).
In this study, no significance threshold is imposed at the SNP combination level and, thus, $k_d$ reaches its maximum value of $C^d_m$ ($m$ choose $d$).

For each subject $i$ ($i = 1,2, \dotsm, n$), the $d$-way multilocus risk score is calculated as
$$MRS_d(i) = \sum_{j = 1}^{k_d} \gamma_j \times \textrm{HLO}_j(X_{ij})$$
where $\gamma_j$ is the test statistic of the $j^\textrm{th}$ genotype combination output from MB-MDR, $X_{ij}$ is the $j^\textrm{th}$ genotype combinations of subject $i$ and $\textrm{HLO}_j$ represents the $j^\textrm{th}$ recoded HLO matrix (1 = High, -1 = Low, 0 = No evidence).
As an example, consider a pair $X_{*j} = (SNP_{j_1}, SNP_{j_2})$ with $\gamma_j=8.3$ and corresponding HLO matrix of all O's except an L in the first cell.
Then, all subjects' current risks would remain the same except the ones with $SNP_{j_1} = SNP_{j_2} = 0$ where their risks are subtracted by 8.3.

In this study, we consider 1-way and 2-way interactions.
We denote by MRS the combined risk score MRS1 + MRS2.
We will compare the performance of the standard PRS method to the combined risk MRS and also its components, MRS1 and MRS2, separately.

### Mutual information and information gain
For a given simulated data set, we apply entropy-based methods to measure how much information about the phenotype is due to either marginal effects or the synergistic effects of the variants after subtracting the marginal effects.
A dataset's amount of main effect $ME$ can be measured as the total of mutual information between each genotype $SNP_j$ and the phenotypic class $Y$ based on Shannon's entropy $H$ [@yzGboP1g]:
$$ME = \sum_{j}^k I(SNP_j; Y) = \sum_{j}^k H(Y) - H(Y|SNP_j).$$

We measure the 2-way interaction information (i.e. degree of synergistic effects of genotypes on the phenotype) of each dataset by summing the pairwise information gain between all pairs of genetic attributes.
Specifically, if we let $X_j$ denote the $j^\textrm{th}$ genotype combination $(SNP_{j_1}, SNP_{j_2})$, the total 2-way interaction gain (i.e. synergistic effects $SE$) is calculated as 
$$SE = \sum_{j}^kIG(X_j; Y) = \sum_{j}^k \left(I(SNP_{j_1}, SNP_{j_2}; Y) - I(SNP_{j_1}; Y) - I(SNP_{j_2}; Y)\right),$$
where $IG$ measures how much of the phenotypic class $Y$ can be explained by the 2-way epistatic interaction within the genotype combination $X_j$.
We refer the reader to Ref. [@1FFMLUZxb] for more details on the calculation of the entropy-based terms.

### Simulated data
The primary objective of this data simulation process was to provide a comprehensive set of reproducible and diverse datasets for the current study.
Containing 1000 individuals and 10 SNPs, each dataset was generated in the following manner.
For an individual, each genotype was randomly assigned with 1/2 probability of being heterozygous (*Aa*, coded as `1`), 1/4 probability of being homozygous major (*AA*, coded as `0`) and 1/4 probability of being homozygous minor (*aa*, coded as `2`).
The binary endpoint for the data was determined using a recently proposed evolutionary-based method for dataset generation called Heuristic Identification of Biological Architectures for simulating Complex Hierarchical Interactions (HIBACHI) [@pDXdtMFa].
This method uses Genetic Programming (GP) to build different mathematical and logical models resulting in a binary endpoint, such that the objective function called fitness is maximized. 
The unique feature of HIBACHI is explainability, as each generated model represents a formula for generating the endpoint. 
In this study, to arrive at a diverse collection of datasets, we aim to maximize the difference in predictive performance of all pairs of ten pre-selected classifiers from the extensive library of scikit-learn [@1iuWTU7i] (Table 1).
Therefore, we define the fitness function of HIBACHI as the difference in accuracy between two classifiers. In other words, the first classifier was supposed to perform as well as possible on the data while the second as bad as possible.

Table 1. Selected machine learning methods and their parameters.

| Algorithm      |                             Parameters                                         |
|:--------------:|:------------------------------------------------------------------------------:|
| GaussianNB     |'priors': {None,2}, 'var_smoothing': {1e-9, 1e-7, 1e-5, 1e-3, 1e-1, 1e+1}       |
| BernoulliNB    |'alpha': {1e-3, 1e-2, 1e-1, 1., 10., 100.},'fit_prior': {True, False}           |
| DecisionTree   |'criterion': {"gini", "entropy"}, 'max_depth': [1, 11], 'min_samples_split': [2, 21], 'min_samples_leaf': [1, 21]|
|ExtraTrees      |'n_estimators': {50,100}, 'criterion': {"gini", "entropy"},'max_features': [0.1, 1], 'min_samples_split': range(2, 21,2),'min_samples_leaf': range(1, 21,2), 'bootstrap': {True, False}|
|RandomForest    |'n_estimators': {50,100}, 'criterion': {"gini", "entropy"},'max_features': [0.1, 1], 'min_samples_split': range(2, 21,4), 'min_samples_leaf':  range(1, 21,5), 'bootstrap': {True, False}                 |
|GradientBoosting|  'n_estimators': {50,100},'learning_rate': {1e-3, 1e-2, 1e-1, 0.5, 1}, 'max_depth': {2,4,8}, 'min_samples_split': [2, 21], 'min_samples_leaf': [1, 21], 'subsample': [0.1, 1], 'max_features': [0.1, 1]|
|KNeighbors      |'n_neighbors': [1, 100], 'weights': {"uniform", "distance"} , 'p': {1, 2}   |
|LogisticRegression| 'C': {1e-3, 1e-2, 1e-1, 1., 10.}, 'solver' : {'newton-cg', 'lbfgs', 'liblinear', 'sag'}|
|XGBoost     | 'n_estimators'=100, 'max_depth': [2, 10], 'learning_rate': {1e-3, 1e-2, 1e-1, 0.5, 1.}, 'subsample': [0.05, 1], 'min_child_weight': [1, 20],
|MLPClassifier |: 'hidden_layer_sizes': {(10),(11),(12),(13),(14),(15),(10,5)},  'activation': {'logistic','tanh','relu'}, 'solver': ['lbfgs'], 'learning_rate': {'constant','invscaling'}, 'max_iter'=1000, 'alpha':np.logspace(-4,1,4)|

HIBACHI was run for 50 iterations with population of 500 individuals representing pairs of classifiers.
At each iteration, five randomly chosen settings for each of the classifiers (Table 1) were chosen among all potential options and served as hyperparameters for that method.
Each of the settings was analyzed using 5-fold cross-validation and the best set of hyperparameters for each classifier was considered for comparison. 
The best settings out of 5 for each classifiers were compared and the settings that maximized the difference in the fitness were promoted.
Each experiment in which one machine learning method was expected to outperform the other was repeated five times.
The results of each pair of classifiers were later averaged.

For each simulated dataset, after randomly splitting the entire data in two smaller sets (80% training and 20% holdout), we built the MRS model on training data to obtain the $\gamma$ coefficients and the HLO matrix, and then we calculated risk score for each individual in the holdout set.
We assess the performance of the MRS by comparing the area under the Receiving Operator Characteristic curve (auROC) with that of the standard PRS method on the holdout set.

### Manuscript drafting
This manuscript is collaboratively written using the Manubot software which supports open paper writing via GitHub with Markdown [@YuJbg3zO].
Manubot uses continuous integration to monitor changes and automatically update the manuscript.
As a result, the latest version of this manuscript is always available at [https://lelaboratoire.github.io/rethink-prs-ms/](https://lelaboratoire.github.io/rethink-prs-ms/).


### Availability
Detailed simulation and analysis code needed to reproduce the results in this study is available at [https://github.com/lelaboratoire/rethink-prs/](https://github.com/lelaboratoire/rethink-prs/).



## Results

### Datasets
[Patryk Orzechowski]

[simulated datasets of $n = 1000$ individuals, $p = 10$ SNPs]

### MRS outperforms standard PRS in the majority of simulated datasets

![MRS produces improved auROC in the majority (335 green lines) of the 450 simulated datasets (each line represents a dataset). In many datasets, the standard PRS method performs poorly (auROC < 60%) while the new method yields auROC over 90%. This improvement in performance can be seen at the second peak (~50% auROC increase) in the density of the difference between the auROCs from the two methods (right).](images/1_ori_vs_MRS_auROC_.svg){#fig:auroc_mrs_prs width="80%"}

In 335 out of 450 simulated datasets, MRS produces higher auROC compared to PRS (green lines, Fig. {@fig:auroc_mrs_prs}).
In 363 datasets where the standard PRS method performs poorly (auROC < 60%), MRS performs particularly well (auROC > 90%) in 102 datasets.
When MRS yields smaller auROC, the difference is small (3.3% ± 2.8%, purple lines/areas).
Across all datasets, the improvement of MRS over PRS is significant (P < $10^{-15}$) according to a Wilcoxon signed rank test.
To assess whether this improvement in performance correlates with the amount of interaction effects contained in each dataset, in the following section, we untangled the two components of MRS and test for the correlation between the difference in auROC and two entropy-based measures, main and interaction effect, of each dataset.

### Assess improvement in performance
Individually, MRS1 and MRS2 both significantly outperformed the standard PRS method (both P values < $10^{-15}$) according to a Wilcoxon signed rank test.
As the amount of main effects increases (Fig. {@fig:improvements} left column), MRS1 increasingly performs better than PRS, which is likely because encodings are inferred (top left).
Meanwhile, MRS2's accuracy remain mostly similar to that of PRS (middle left).
On the other hand, when the amount of interaction effects increases (Fig. {@fig:improvements} right column), MRS1 performs mostly on par to PRS while MRS2 increasingly performs better than PRS.
Combining the gain from both MRS1 and MRS2, MRS's performance progressively increases compared to the standard PRS.

![Combining 1-way (MRS1) and 2-way (MRS2) risk scores, MRS shows increasing outperformance to standard PRS as dataset contains more main and interaction effects.](images/improvements_train_ms.svg){#fig:improvements width="70%"}

## Discussion

We introduce a Multilocus Risk Score (MRS) method to improve the performance of the standard PRS in disease risk stratification of patient populations. 
While PRS holds much promise for development of new precision medicine approaches by identifying high risk individuals who may benefit from prioritized interventions, one of its current limitations is the model simplicity [@1GK3F1BxE].
As a first step towards addressing this issue and increasing comprehensiveness of risk profiling models, in this study, we developed a new applied MRS method from the MB-MDR framework that enables automatic genotype encodings and takes into account multiple models for detecting gene-gene (GxG) interactions. 
Utilizing the efficient implementation of MB-MDR, MRS automatically infers the genotype encodings and simultaneously computes the risk of variant combinations.
Through comparing method performance on a diverse collection of simulated data, we demonstrate the robust polygenic risk profiling ability of MRS and suggest the importance of flexible, precise methods in better capturing epistasis behind individual patient risk.

We showed that the MRS method outperformed standard PRS in many of the simulated datasets, highlighting the importance of genotype encodings and consideration of epistasis.
We further examined the association between this improvement and the amount of two-way epistatic effect induced in the binary phenotypic outcome.
Appropriate phenotype encodings are important for improving the accuracy when there is a large amount of main effects of the variants on the phenotypic outcome.
Meanwhile, inclusion of epistatic terms significantly increases the accuracy from PRS, especially when two-way interactions are present in the data.
Although we only considered up to two-way GxG interactions, it is straightforward to incorporate higher order interactions (e.g. three-way, four-way) into MRS.
However, preliminary analyses on the simulated datasets for such higher order interactions did not show significant improvement from the current MRS (results not shown).
We also recommend estimating the computational expense prior to implementing high order interactions, especially for larger datasets encountered in practice.

Although MRS captures the improvements of MB-MDR in reporting polygenic risk profiles, there are three primary limitations.
First, MRS has not been applied to real-world data.
Although we compensated the lack of real data with a diverse set of simulated datasets, a future study analyzing real-world data will prove beneficial to quantify the new MRS model's utility in practice.
Second, accounting for epistasis, in principle, is largely more computationally expensive compared to investigating solely main effects.
Therefore, even with fast and efficient software, pre-selecting the variants (e.g. based on specific pathways or prior knowledge) will prove beneficial for accurate MRS computing when analyzing datasets containing a larger number of variants.
However, we hope the promising preliminary results will open the doors to future approaches that encompass main and interaction effects and improve scalability.

Finally, we caution that a risk score model should be evaluated based on not only sensitivity and specificity but also with respect to potential clinical efficacy, and any genetic risk should be interpreted in aggregate with other risk factors.
Future works focusing on gene-environment interactions with time-dependent risk factors will be crucial in order to communicate risk properly for preventive interventions.

In conclusion, MRS enhances the predictive capacity of current risk profiling model for complex diseases with polygenic architectures.
While there is much work left to do to improve the personal and clinical utility of general risk profiling framework, we highlight that more comprehensive models that infer proper genotype encodings and account for epistatic effects greatly improve the prediction efficiency and affords new opportunities for more accurate clinical prevention.


## Acknowledgement

We thank Dr. Kristel Van Steen and Aldo Camargo for their helpful responses to our inquires about the MB-MDR software.

## References {.page_break_before}

<!-- Explicitly insert bibliography here -->
<div id="refs"></div>
