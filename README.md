# Social Media Usage & Perception: A Multivariate Analysis

A full exploratory and multivariate statistical study of how people use and perceive social media, built from an original survey. The project goes from questionnaire design and data collection through descriptive statistics, Principal Component Analysis (PCA), Multiple Correspondence Analysis (MCA), and unsupervised clustering, ending in six concrete, interpretable user profiles.

![R](https://img.shields.io/badge/R-276DC3?style=flat-square&logo=r&logoColor=white)
![FactoMineR](https://img.shields.io/badge/FactoMineR-1f6f43?style=flat-square)
![RMarkdown](https://img.shields.io/badge/R_Markdown-198CE7?style=flat-square&logo=rstudio&logoColor=white)
![License](https://img.shields.io/badge/license-MIT-black?style=flat-square)

> Note: the analysis report itself is written in French. This README summarizes it in English.

---

## Overview

The goal is to understand the structure behind people's attitudes toward social media: how usage intensity, perceived usefulness, dependence, and concern over data privacy relate to one another, and whether the population can be segmented into distinct behavioral types. Rather than looking at questions one at a time, the study uses multivariate methods to surface the underlying dimensions that organize the responses, then turns those dimensions into named user profiles.

The analysis is structured around three questions:

1. **What are the main dimensions that link or oppose users' attitudes?** Answered with PCA on perception and behavior items.
2. **How do concrete practices and qualitative profiles associate?** Answered with MCA on categorical usage items.
3. **Can users be grouped into distinct, homogeneous segments?** Answered with hierarchical clustering on the PCA coordinates.

---

## Dataset

The data comes from an original online questionnaire (Google Forms), collected in October 2025.

- **53 respondents**, predominantly students aged 20 to 24.
- Strong geographic concentration in the Grand Tunis area (Nord-Est region), reflecting urban density.
- Two blocks of questions:
  - **Likert-scale items (1 to 5)** on perceptions and behaviors (privacy, dependence, routine, perceived benefits, sense of security).
  - **Binary items (Yes / No)** on concrete practices (daily use, professional use, following the news, account deactivation, screen-time reduction).

Raw responses are in `survey_responses.csv`.

---

## Methodology

| Step | Method | Purpose |
|------|--------|---------|
| Descriptive statistics | Frequency tables, bar charts (`ggplot2`) | Characterize the sample (age, occupation, region) |
| PCA (ACP) | `FactoMineR::PCA` on 15 Likert items | Find the latent dimensions of perception and behavior |
| MCA (ACM) | `FactoMineR::MCA` on 10 binary items | Associate concrete practices with qualitative profiles |
| Clustering | `cluster::agnes` (Ward), validated with `NbClust` | Segment users into homogeneous groups |
| Profiling | `FactoMineR::catdes` | Statistically characterize each cluster |

Dimension selection was done rigorously, cross-checking the Kaiser criterion, the elbow (scree) rule, and cumulative inertia. The number of clusters (6) was chosen from the inertia-gap in the dendrogram and confirmed against the 26 indices in `NbClust`.

---

## Key findings

**The two main dimensions (PCA)**

- **Axis 1: degree of integration and usefulness.** Opposes intensive, routine, "fused" usage (checking on waking and before sleep, difficulty disconnecting, perceived benefits for news and opportunities) against detachment.
- **Axis 2: climate of trust and security.** Independent of usage frequency, this axis captures digital distrust: concern over data and lack of consent at one pole, a sense of security at the other.

**Six user profiles (clustering)**

1. **The Utilitarian Addict**, admits dependence but justifies it by the tool's usefulness.
2. **The Reluctant Worrier** (the largest group), permanent distrust yet stays on by social necessity.
3. **The Sovereign Detached**, the most autonomous and privacy-protective, no routine dependence.
4. **The Indifferent**, total disengagement, sees social media as a non-event.
5. **The Automatic Routiner**, mechanical, habit-driven use with no professional goal.
6. **The Confident Professional**, uses platforms pragmatically for career, with the lowest concern level in the study.

Crossing the profiles with age showed a coherent pattern: the youngest respondents are the most career-focused (whether by addiction or strategy), while the oldest show the greatest detachment, pointing to a form of digital maturity gained over time.

---

## Repository structure

```
.
├── social_media_analysis.Rmd    # Full analysis (R Markdown source)
├── survey_responses.csv         # Raw survey data
└── README.md
```

---

## How to run

**Requirements:** R (>= 4.0) and the following packages:

```r
install.packages(c(
  "FactoMineR", "factoextra", "ggplot2",
  "dplyr", "cluster", "NbClust"
))
```

**Steps:**

1. Clone the repository and open `social_media_analysis.Rmd` in RStudio.
2. In the data-loading chunk, set the `read.csv(...)` path to `survey_responses.csv` (the source currently points to a local path, update it to the file in this repo).
3. Knit the document to HTML, Word, or PDF, or run the chunks interactively.

---

## Limitations

The sample is small (53 respondents) and geographically concentrated, so results are exploratory rather than generalizable. As noted in the report, adding one variable, each respondent's most-used platform, would have allowed the theoretical profiles to be tied to real applications (for example, testing whether messaging-app users cluster into the "technical sociability" profile). This is the main avenue for a follow-up study.

---

## Authors

- **Mohamed Ali Aoun** , [GitHub](https://github.com/daliaoun)
- **Ameni Ben Youssef**

Academic project, Master's in AI & Data Science, Université Paris Dauphine-PSL (Tunis).
