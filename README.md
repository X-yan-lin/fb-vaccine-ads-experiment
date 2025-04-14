# COVID-19 Facebook Ad Experiment Analysis

## Project Description

This study analyzes the comparative effectiveness of Facebook ad campaigns (rational argument vs. emotional appeal strategies) for promoting COVID-19 vaccine uptake. Using simulated data from a controlled experiment with 4,500 US participants completing both baseline and endline surveys, I examine:

- Treatment effects on vaccination intentions and uptake
- Potential psychological mechanisms driving behavior change
- Heterogeneous effects across demographic subgroups

## Key Findings 

Both emotional and rational Facebook ads significantly increased COVID-19 vaccine uptake, with emotional appeals proving more effective. Effects were consistent across demographic subgroups. Cluster analysis further confirmed that ad effectiveness did not vary meaningfully across population segments, suggesting broad applicability of these campaign strategies. These results demonstrate that targeted social media messaging—particularly emotion-based appeals—can effectively promote vaccination behavior at scale.

## Data Documentation

**Survey Instrument**  
Complete questionnaire available in:  
`/data/Survey Questions.xlsx`  

**Likert Scale Measures**  
Vaccine attitude questions were developed based on:  
[Krastev et al. (2023) *PLOS ONE*](https://journals.plos.org/plosone/article?id=10.1371/journal.pone.0295912)  

**Demographic Benchmarks**  
Population parameters were calibrated using:

1. **Age/Gender Structure**:  
   [U.S. Census Population Pyramid](https://www.census.gov/popclock/data_tables.php?component=pyramid)

2. **Social Media Patterns**:  
   - [Pew Research: Facebook User Statistics (2024)](https://www.pewresearch.org/short-reads/2024/02/02/5-facts-about-how-americans-use-facebook-two-decades-after-its-launch/)  
   - [Teen Social Media Use (Pew 2023)](https://www.pewresearch.org/internet/fact-sheet/teens-and-social-media-fact-sheet/)

3. **Race/Ethnicity**:  
   [Census QuickFacts](https://www.census.gov/quickfacts/fact/table/US/RHI225222)

4. **Income Distribution**:  
   [Statista Household Income Data](https://www.statista.com/statistics/203183/percentage-distribution-of-household-income-in-the-us/)

5. **Education Levels**:  
   [Census Educational Attainment](https://www.census.gov/newsroom/press-releases/2023/educational-attainment-data.html)

**Note**: All simulated data preserves the marginal distributions and covariance structure of these benchmark sources.


## Repository Structure

```
.
├── analysis/
│   ├── Clustering.Rmd
│   ├── Likert_Scale.Rmd
│   ├── Processed_Data.Rmd
│   └── Regression.Rmd
├── data/
│   ├── Stimulated/
│   │   ├── assignment_data.csv
│   │   ├── baseline_survey_data.csv
│   │   └── endline_survey_data.csv
│   ├── processed/
│   └── DataTask_Covid.Rmd
└── output/
    ├── figures/
    └── tables/
```

## Data Pipeline

### 1. Generate Simulated Data
Run the data simulation script to generate datasets for baseline, endline and assignment:

```bash
Rscript -e "rmarkdown::render('analysis/DataTask_Covid.Rmd')"
```

**Outputs:**
- `data/processed/baseline_survey_data.csv`
- `data/processed/endline_survey_data.csv` 
- `data/processed/assignment_data.csv`

### 2. Process Data 
Run process data script to generate a full dataset for analysis: 

```bash
Rscript -e "rmarkdown::render('analysis/Processed_Data.Rmd')"
```
**Outputs:**
- `data/processed/full_data_cleaned.csv`

### 3.1 Data Analysis (Treatment effects on vaccination intentions and uptake) 
Regression analysis to understand the effectivness of ad campaigns: 

```bash
Rscript -e "rmarkdown::render('analysis/Regression.Rmd')"
```
**Outputs:**
- `output/tables/balance_test.html`
- `output/tables/regression_results.html`

### 3.2 Data Analysis (Potential psychological mechanisms driving behavior change)
Kruskal-Wallis test & Pairwise Wilcoxon tests to understand the attitude changes among treated and control groups

```bash
Rscript -e "rmarkdown::render('analysis/Likert_Scales.Rmd')"
```
**Outputs:**
- `/output/figures/mean_change_heatmap.png`
- `/output/tables/kw_test_results.png`
- `/output/tables/pairwise_wilcoxon_results.png`

### 3.3 Data Analysis (Heterogeneous effects across demographic subgroups)
K-mode clustering to investigate ad effectiveness among specific demographic clusters 

```bash
Rscript -e "rmarkdown::render('analysis/Clustering.Rmd')"
```
**Outputs:**
- `/output/figures/elbow_plot.png`
- `/output/figures/effectiveness_cluster.png`
- `/output/tables/cluster_summary.png`
- `/output/tables/clustering * regression_results.html`


