# Simulated Human-to-Gorilla Respiratory Disease Linkage & Risk Analysis

**A reproducible epidemiology and data-science portfolio project exploring temporal exposure linkage, illness patterns, statistical testing, and logistic-regression classification using fully synthetic data.**

<p>
  <img alt="Python" src="https://img.shields.io/badge/Python-3.10%2B-blue">
  <img alt="Jupyter" src="https://img.shields.io/badge/Jupyter-Notebooks-orange">
  <img alt="SQLite" src="https://img.shields.io/badge/SQL-SQLite-lightgrey">
  <img alt="Data" src="https://img.shields.io/badge/Data-100%25%20Synthetic-purple">
  <img alt="Project type" src="https://img.shields.io/badge/Project-Epidemiology%20Simulation-teal">
</p>

> [!CAUTION]
> **SIMULATION ONLY — NOT EVIDENCE OF REAL TRANSMISSION.** Every health event, tourist record, exposure link, attribution label, statistical result, model coefficient, and policy-scenario output in this repository is synthetic. Nothing here estimates actual zoonotic transmission, illness incidence, or intervention effectiveness in wild mountain gorillas.

## Project overview

Respiratory pathogens can cross human–great-ape interfaces, and published research has documented human metapneumovirus infection in wild mountain gorillas. This project builds a **synthetic analytical workflow** to demonstrate how researchers might organize exposure and illness records, explore temporal proximity, quantify group-level patterns, and evaluate a classification model.

The workflow combines:

- Pandas data preparation and exploratory analysis;
- SQL-based temporal linkage with SQLite;
- non-parametric tests, correlation analysis, and effect-size summaries;
- logistic regression with a train/test evaluation and cross-validation;
- seasonal summaries, visualizations, and exploratory intervention scenarios.

The model's target is a **rule-generated tourism-attribution label**, not an independently verified transmission event. The distinction is critical to interpreting every result below.

## ⚠️ Data transparency

The datasets used in this project are **synthetic** and were created strictly for educational, analytical, and portfolio purposes. They do not represent real gorilla health records, tourist health records, exposure logs, clinical histories, or verified transmission chains.

The data structure, biological context, and analytical assumptions were informed by published research on great-ape respiratory disease and human–wildlife interfaces. However, **all event linkages, attribution labels, statistical findings, model coefficients, and policy-scenario outputs are generated from synthetic data and must not be interpreted as real-world findings**.

This project demonstrates how temporally linked exposure and illness records could be analyzed. A comparable study using appropriate authorized field data could follow a similar workflow, but its conclusions would depend on validated measurements, appropriate study design, and independent evidence of exposure or transmission.

Any future research involving real institutional or field health data would require appropriate data-access permission, research authorization, and applicable ethical or regulatory approvals.

## Research questions

1. How do the number of symptomatic tourist visits and the timing of simulated gorilla illness events relate under a defined temporal-linkage rule?
2. How do simulated respiratory-event counts and severity summaries vary by age category?
3. How sensitive are tourism-proximity labels to the chosen exposure window?
4. How well can a logistic-regression model reproduce the project's rule-generated attribution labels?
5. What can—and cannot—be inferred from the exploratory masking and policy-scenario analyses?

## Data and analytical design

The saved notebooks report **19,836 synthetic gorilla illness-event records**, **105 simulated gorilla identities** represented in the age-category summaries, and **3,287 daily observations** for the same-day symptom correlation. The linkage workflow joins symptomatic tourist visits to illness events in the same simulated group when the visit occurred from 0 to 14 days before the illness event.

The project's `tourism_attributed`, `tourism_possible`, and `non_tourism` classes are operational labels assigned by deterministic rules. They are **not laboratory-confirmed transmission sources**.

## Key results — simulated findings

### 1. Temporal linkage and attribution sensitivity

Using the notebook's 14-day exposure window, the SQL linkage produced:

| Output | Saved result |
|---|---:|
| Synthetic gorilla illness events processed | 19,836 |
| Events with at least one symptomatic tourist visit in the same group within the window | 19,223 (96.9%) |
| Rule-labelled `tourism_attributed` | 18,519 (93.36%) |
| Rule-labelled `tourism_possible` | 704 (3.55%) |
| Rule-labelled `non_tourism` | 613 (3.09%) |
| Mean linkage-confidence score | 0.810 |
| Median linkage-confidence score | 0.870 |

The attribution rate changes substantially with the exposure window:

| Window | Rule-labelled attributed | % attributed | Rule-labelled possible | % possible |
|---:|---:|---:|---:|---:|
| 5 days | 15,022 | 75.73% | 0 | 0.00% |
| 7 days | 16,782 | 84.60% | 0 | 0.00% |
| 10 days | 17,577 | 88.61% | 679 | 3.42% |
| 14 days | 18,519 | 93.36% | 704 | 3.55% |
| 21 days | 19,365 | 97.63% | 307 | 1.55% |

**Interpretation.** Widening the temporal window increases the proportion classified as tourism-attributed from 75.73% at 5 days to 97.63% at 21 days. This sensitivity is a useful diagnostic of the rule-based workflow, but it also shows that the resulting attribution proportion depends strongly on the analyst-defined window. Temporal proximity alone cannot establish infection source or transmission direction.

### 2. Age category and respiratory-event counts

The Kruskal–Wallis test output was **H = 55.8102, p < 0.001** across six age categories. The notebook's group summaries are:

| Age category | Simulated individuals (n) | Mean respiratory events per individual | Median | Reported bootstrap 95% interval for the mean |
|---|---:|---:|---:|---:|
| Infant | 25 | 321.880 | 379.0 | 256.739–371.325 |
| Silverback | 6 | 183.167 | 176.0 | 167.996–203.846 |
| Juvenile | 16 | 133.875 | 142.0 | 115.062–147.377 |
| Subadult | 13 | 99.000 | 93.0 | 91.923–110.160 |
| Adult female | 37 | 81.270 | 79.0 | 78.297–84.460 |
| Adult male | 8 | 67.750 | 73.5 | 47.619–81.378 |

**Interpretation.** Infants have the highest mean event count in the simulated records (321.88 per individual), followed by silverbacks (183.17). These are event counts in the generated dataset, not incidence rates adjusted for time at risk. The reported `η² = 0.6525` is produced by a custom mean-based calculation after a Kruskal–Wallis test; it should **not** be interpreted as a validated Kruskal–Wallis effect size without methodological correction.

### 3. Same-day tourist symptoms and lag analysis

| Analysis | Saved result |
|---|---:|
| Same-day Spearman correlation | ρ = −0.1176 |
| Daily observations | n = 3,287 |
| Reported p-value | Printed as 0.000000; report as p < 0.001, not p = 0 |
| Lag scan | 0–21 days |
| Peak absolute correlation in saved output | 0 days, ρ = −0.118 |

**Interpretation.** The saved lag scan identifies the strongest absolute correlation at **zero days**, and that association is weak and negative. The notebook output therefore does **not** support the earlier README statement that a positive 7–14-day lag is the biologically meaningful signal. This scan is exploratory; daily autocorrelation, seasonal patterns, multiple lag testing, and the synthetic nature of the data limit inference.

### 4. Severity distribution across age categories

The event-level chi-square test reports **χ² = 294.0925**, 5 degrees of freedom, **p < 0.001**, and **Cramér's V = 0.1351**.

| Age category | Respiratory events | Severe/fatal events | Severe/fatal (%) | Fatal (%) |
|---|---:|---:|---:|---:|
| Infant | 8,047 | 1,999 | 24.8% | 8.0% |
| Silverback | 1,099 | 283 | 25.8% | 7.5% |
| Subadult | 1,287 | 201 | 15.6% | 4.8% |
| Adult male | 542 | 84 | 15.5% | 3.3% |
| Juvenile | 2,142 | 290 | 13.5% | 3.8% |
| Adult female | 3,007 | 407 | 13.5% | 3.4% |

**Interpretation.** The saved synthetic table has the highest severe/fatal percentage among silverbacks (25.8%) and infants (24.8%). Cramér's V of 0.1351 indicates a modest association under the reported calculation. Because the dataset contains repeated events for the same simulated individuals, a conventional event-level chi-square test may violate independence; a clustered or individual-level analysis is needed before inferential claims.

### 5. Severity in tourism-linked versus background-labelled events

The Mann–Whitney output reports **U = 24,904,593.5, p < 0.001**, with a reported Cohen's *d* of **0.1554**.

| Rule-defined category | Mean severity score | Median severity score |
|---|---:|---:|
| Tourism-linked | 1.861 | 2 (moderate) |
| Background | 1.720 | 1 (mild) |

The severity scale is 1 = mild, 2 = moderate, 3 = severe, and 4 = fatal. The standardized difference is small. More importantly, “tourism-linked” is assigned using temporal proximity and the project's linkage-confidence rule, not independent confirmation of etiology. The comparison describes the synthetic construction and its labels; it does **not** show that tourist-associated infections are more severe in real gorillas.

### 6. Annual masking-compliance association

Across nine annual observations (2015–2023), the saved Spearman analysis reports **ρ = 0.25, p = 0.51649, n = 9**. The result is not statistically significant at α = 0.05.

Mask-compliance values in the simulated records were approximately 41–42% during 2015–2019 and 87–88% during 2020–2023, while annual respiratory-event counts remained between 1,716 and 1,859. With only nine annual points, temporal aggregation, and potential confounding, this analysis cannot estimate the protective effect of masking. A non-significant result does not demonstrate that masking is ineffective.

### 7. Logistic regression: reproducing rule-generated labels

The model notebook reports a dataset with **19,836 rows and 22 features**. The target is generated from `attributed_source`:

| Label | Records | Proportion |
|---|---:|---:|
| `tourism_attributed` (positive class) | 18,519 | 93.4% |
| All other labels | 1,317 | 6.6% |

A stratified random split produced 14,877 training records and 4,959 test records. The saved test results were:

| Metric | Saved value |
|---|---:|
| Test ROC-AUC | 0.9841 |
| Test accuracy | 0.94 |
| Tourism-attributed precision | 1.00 |
| Tourism-attributed recall | 0.93 |
| Tourism-attributed F1 | 0.97 |
| Non-tourism precision | 0.52 |
| Non-tourism recall | 1.00 |
| Non-tourism F1 | 0.68 |
| Five-fold AUC values (displayed) | 0.984, 0.983, 0.985, 0.984, 0.984 |

The largest reported coefficient belongs to `n_sym_tourists_in_window` (coefficient = 12.7347; reported odds ratio = 339,304.7195). This extreme association is **not evidence of a biological effect**. The target label is constructed from linkage confidence, and linkage confidence itself incorporates the symptomatic-tourist count in the exposure window. The model is therefore using a feature that helps define its answer—a form of target leakage. The high AUC primarily shows that the model can reconstruct a deterministic label-generating rule.

The reported odds-ratio intervals should also not be used as inferential 95% confidence intervals: the notebook approximates them using the standard deviation of the coefficient vector rather than the coefficient-specific standard errors. Continuous and binary features are scaled in the pipeline, so exponentiated coefficients also require careful interpretation.

### 8. Policy-scenario diagnostic: current model is not intervention-ready

The notebook applied four scenarios, but every predicted probability remained **1.0000 (100.0%)**:

| Scenario | Predicted rule-label probability |
|---|---:|
| Baseline | 100.0% |
| Universal masking | 100.0% |
| 80% reduction in symptomatic tourists | 100.0% |
| Combined masking and screening | 100.0% |

These outputs show that the current scenario procedure is **uninformative** for comparing interventions. The dominant feature, `n_sym_tourists_in_window`, is not reduced in the screening scenario, and the model predicts a saturated probability for every tested input. These are not estimates of the effects of masking, screening, or other conservation-health policies.

### Selected visual outputs

**Sensitivity to the analyst-defined exposure window**

![Sensitivity analysis for the temporal linkage window](outputs/figures/03_sensitivity_analysis.png)

*The chart reflects how synthetic rule-based attribution labels change as the selected time window changes. It does not measure real transmission risk.*

**ROC curve for classification of synthetic attribution labels**

![ROC curve for the rule-label classifier](outputs/figures/06_roc_curve.png)

*The high AUC must be interpreted in light of target leakage described above; it is not evidence of real-world prediction performance.*

## Core formulas

Equations use GitHub-supported `math` fences so they render directly in `README.md`.

### 1. Temporal exposure window

A tourist visit at time $t_v$ is considered temporally linked to an illness event at time $t_i$ when both events refer to the same group and:

```math
0 \leq t_i - t_v \leq W, \qquad W = 14\text{ days}
```

This is a linkage rule, not a causal transmission criterion.

### 2. Linkage-confidence score

For a temporally proximate event, the code constructs a heuristic score from the number and severity of symptomatic tourists and the lag:

```math
C = \min\left(1,\ 0.30 + 0.10\min(n,5) + s + \ell\right)
```

Here, $n$ is the number of symptomatic tourist visits in the window, $s$ is a symptom-severity bonus, and $\ell$ is a lag bonus. Non-proximate events receive $C=0$. This score is a hand-defined index, **not a calibrated probability**.

The label rule is:

```math
\begin{aligned}
C \geq 0.50 &\Rightarrow \text{tourism-attributed} \\
0.30 \leq C < 0.50 &\Rightarrow \text{tourism-possible} \\
C < 0.30 &\Rightarrow \text{non-tourism}
\end{aligned}
```

### 3. Spearman rank correlation

```math
\rho_s = \mathrm{corr}\left(\mathrm{rank}(X),\mathrm{rank}(Y)\right)
```

The saved same-day value is $\rho_s=-0.1176$, a weak negative rank association in the synthetic daily series.

### 4. Kruskal–Wallis test

```math
H = \frac{12}{N(N+1)}\sum_{j=1}^{k}\frac{R_j^2}{n_j} - 3(N+1)
```

Here, $N$ is the total number of observations, $k$ is the number of groups, $R_j$ is the sum of ranks for group $j$, and $n_j$ is its sample size. The saved age-category result is $H=55.8102$, with reported $p<0.001$.

### 5. Chi-square association and Cramér's V

```math
\chi^2 = \sum_{i}\sum_{j}\frac{(O_{ij}-E_{ij})^2}{E_{ij}}
```

```math
V = \sqrt{\frac{\chi^2}{N\min(r-1,c-1)}}
```

For the simulated age-category by severity table, the notebook reports $\chi^2=294.0925$ and $V=0.1351$. Dependence between repeated events from the same individual is not addressed by the simple event-level test.

### 6. Logistic regression and odds ratios

```math
P(Y=1\mid X) = \frac{1}{1+\exp\left[-\left(\beta_0+\sum_{j=1}^{p}\beta_jX_j\right)\right]}
```

```math
\mathrm{OR}_j = \exp(\beta_j)
```

Because the label is rule-generated from variables related to the predictors, these equations describe classification of synthetic labels—not estimation of a causal transmission probability.

### 7. ROC-AUC

The ROC curve plots sensitivity against the false-positive rate over classification thresholds. AUC summarizes ranking discrimination:

```math
\mathrm{FPR} = \frac{FP}{FP+TN}, \qquad
\mathrm{TPR} = \frac{TP}{TP+FN}
```

```math
\mathrm{AUC} = \int_0^1 \mathrm{TPR}(u)\,d u
```

The saved test AUC is 0.9841, but target leakage means it should not be presented as evidence of real-world transmission prediction.

## Workflow and repository structure

```text
simulated-gorilla-zoonotic-analysis/
├── README.md
├── requirements.txt
├── environment.yml
├── data/
│   ├── raw/                 # Synthetic input tables
│   └── processed/           # Cleaned and linked synthetic tables
├── notebooks/
│   ├── 01_eda_and_preprocessing.ipynb
│   ├── 02_date_proximity_linkage.ipynb
│   ├── 03_statistical_analysis.ipynb
│   ├── 04_seasonal_analysis.ipynb
│   ├── 05_risk_modeling.ipynb
│   └── 06_final_dashboard.ipynb
├── src/
│   ├── linkage.py
│   ├── stats_utils.py
│   └── viz_utils.py
└── outputs/
    ├── figures/
    └── reports/
```

### Reproducing the workflow

```bash
git clone https://github.com/BrunoElDaroux/simulated-gorilla-zoonotic-analysis.git
cd simulated-gorilla-zoonotic-analysis
python -m pip install -r requirements.txt
jupyter lab
```

Run the notebooks in numerical order. The saved outputs were produced in a prior execution environment; rerunning the notebooks may change figures and results if dependencies, data, random states, or code differ. Check `environment.yml` for the pinned environment specification.

## Limitations and priorities for improvement

1. **Synthetic records only.** No results should be interpreted as real disease incidence, transmission, or conservation-policy evidence.
2. **Temporal proximity is not transmission.** The current 0–14-day, same-group linkage rule does not verify direct contact, pathogen identity, transmission direction, or a shared source.
3. **Sensitivity to window size.** Rule-labelled attribution changes from 75.73% at 5 days to 97.63% at 21 days.
4. **Target leakage in classification.** The predictor `n_sym_tourists_in_window` contributes to the rule that creates the target label. Rebuild the target from independent simulated ground truth and exclude label-construction variables from the features.
5. **Policy simulations are saturated.** All tested scenarios return 100%; redesign the scenario inputs and model before comparing policies.
6. **Repeated-event dependence.** Illness events are clustered within simulated individuals and groups. Use individual-level, clustered, or hierarchical analysis where appropriate rather than treating every event as independent.
7. **Evaluation split is not group- or time-blocked.** Random record-level splitting can place related events from the same simulated individual or group in both train and test folds. Re-evaluate with temporal holdout and group-aware validation after removing target-defining predictors.
8. **Lag analysis is exploratory.** The observed peak absolute correlation is at 0 days, not the claimed 7–14-day interval. Account for autocorrelation, seasonal structure, and testing across multiple lags.
9. **Effect-size and uncertainty calculations need review.** Recalculate a suitable rank-based effect size for the Kruskal–Wallis analysis and derive logistic-regression confidence intervals from valid coefficient standard errors.
10. **No causal policy evaluation.** This repository does not estimate the effect of masking, screening, or a minimum visitor distance. In particular, it does not contain a validated distance-to-gorilla exposure variable that would enable evaluation of a 7-metre rule.

## Selected literature

These sources provide biological and methodological context; they do not validate the synthetic data, attribution rules, or model results.

1. Palacios, G. et al. (2011). [Human Metapneumovirus Infection in Wild Mountain Gorillas, Rwanda](https://doi.org/10.3201/eid1704.100883). *Emerging Infectious Diseases*, 17(4), 711–713.
2. Scally, A. et al. (2012). [Insights into hominid evolution from the gorilla genome sequence](https://doi.org/10.1038/nature10842). *Nature*, 483, 169–175. This is genomic evolutionary context, not evidence that genomic similarity quantifies respiratory-disease susceptibility.
3. Grützmacher, K. et al. (2018). [Human Respiratory Syncytial Virus and Streptococcus pneumoniae Infection in Wild Bonobos](https://doi.org/10.1007/s10393-018-1319-4). *EcoHealth*, 15, 462–466. Comparative great-ape disease context.

## Author

**Bruno Rudahongerwa Rwarahoze**  
Former Data Entry Staff Member, Dian Fossey Gorilla Fund  
Portfolio project in data analysis, computational epidemiology, SQL, and machine learning.

---

*Documentation note: reported numbers reflect the outputs currently saved in the repository's notebooks. Re-run and validate the analytical pipeline before treating any value as a reproducible result.*
