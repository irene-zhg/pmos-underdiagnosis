# Predicting County-Level PMOS Underdiagnosis Risk in the US
AI4ALL Ignite 2026 Portfolio Project | Group 14B  
Irene Zhang, Joyce Xu, Walter Valera, Vaishali Allibada, Andy Romero

A machine learning pipeline that predicts US counties at high risk of PMOS (formerly PCOS) underdiagnosis, using public health datasets encompassing social vulnerability, health access, health outcome, and geography.  

Valuable predictive model at the local, regional, and national level to raise awareness and deploy interventions to prevent further healthcare gaps. 

## Table of Contents - to be added

## Background and Problem Statement
Polyendocrine Metabolic Ovarian Syndrome (PMOS), previously known as Polycystic Ovarian Syndrome (PCOS), is the most common endocrine disorder in reproductive-age women, affecting approximately 170 million women worldwide at a cost of around $8B to the the US healthcare system in 2020 (WHO, 2026 and Silva et al., 2024). It is a complex disorder that affects reproductive, metabolic, dermatological, and psychological health. While no cure exists, early diagnosis and intervention can significantly reduce long-term risk of type-2 diabetes, insulin resistance, cardiovascular disease and infertility. 

Despite being a major public health challenge, PMOS is severely underdiagnosed, with roughly 70% of affected women undiagnosed (WHO, 2026). Prior research suggests that patterns of structural racism and social determinants of health drive this diagnostic inequity, but no existing dataset directly measures underdiagnosis. Our project provides one as the first national-level model, using a composite label engineered from literature, and trains machine learning models to predict it.

## Research Question
Which county-level social vulnerability and healthcare access factors best predict PMOS underdiagnosis risk across the United States, and which counties are most at risk?

  **Hypothesis**: Counties with greater social vulnerability and reduced healthcare access will have a higher predicted risk of PMOS underdiagnosis.
  
  **Motivation**: Identifying geographic patterns of underdiagnosis can support future targeted public health outreach and more equitable diagnostic and treatment access. 

## Approach
**1. Data Selection & Merge**: Three national CDC/NCHS datasets were merged on standardized FIPS county codes.\
* [Social Vulnerability Index (2022)](url)
* [PLACES County Data (2025)](url)
* [NCHS Urban-Rural Classification (2023)](url)\
187 missing PLACES values tied entirely to Kentucky and Pennsylvania. Higher rural codes suggest structural bias in CDC survey collection. For further EDA, see colab.

**2. Label Engineering**: No public dataset directly measures underdiagnosis, so a binary composite target label was engineered from three literature-backed signals.\

* **Signal 1**: High social vulnerability - top-quartile SVI index score (Silva et al., 2024)
* **Signal 2**: Low preventative healthcare engagement - bottom-quartile annual checkup or mammography rate (Silva et al., 2024)
* **Signal 3**: Rural/peri-urban NCHS classification - >= 4 NCHS code (Ramphul et al., 2025)\
Signals were built using select features from the datasets, and these features were dropped from model training to prevent data leakage.

Underdiagnosis risk (1) = Signal 1 **and** (Signal 2 **or** Signal 3) - yielded a 21.3% positive rate (671/3144 counties)\

**3. Feature Selection**: 25 literature-based features were used for modeling
| SVI 2022                                                                                                                                                                                         | PLACES 2025                                                                        | NCHS 2023  |
|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------|------------|
| RPL_THEMES<br>RPL_THEME1 through RPL_THEME4<br>EP_NOVEH<br>EP_AFAM<br>EP_UNINSUR<br>EP_LIMENG<br>EP_POV150<br>EP_UNEMP<br>EP_NOHSDP<br>EP_HISP<br>EP_MUNIT<br>EP_HBURD<br>EP_DISABL<br>EP_MINRTY | MAMMOUSE<br>CHECKUP<br>OBESITY<br>DIABETES<br>DEPRESSION<br>HIGHCHOL<br>FOODINSECU | CODE2023   |
|                                                                                                                                                                                                  |                                                                                    |            |
|                                                                                                                                                                                                  |                                                                                    |            |
**4. Training Models & Evaluation**

## Key Results 
1. Ran 3 National Datasets backed by research to identify key features that contribute to PMOS underdiagnosis.
2. Target engineered a risk predictor variable.
3. Identified PMOS underdiagnosis risk for all 3,144 U.S. Counties

## Fairness & Bias Audit

## Impact & Use
**National-Scale Approach**
* First step towards national county-level predictive model for PMOS underdiagnosis
**Awareness**
* Utilized AI/ML models to highlight need 
* Supports future research, resource allocation, policy in highly vulnerable areas
**Healthcare Infrastructure and Policy**
* Resource to further infrastructure and policy based on need and socioeconomic factors
  * Healthcare facilities, social vulnerability aid, etc.
* Supports equitable healthcare approaches and evidence-based public health planning 

## Limitations
**Target Engineering and Feature Configuration**
* Features used in as predictors come from the same datasets with which the target variable has been engineered
* Used features could contain inherent biases
**Data availability**
* PMOS is complex and cannot be diagnosed by a single test
* No available patient-level clinical datasets
**Data Bias**
* Used data comes from the CDC, an organization with its internal bias such as underrepresenting populations with lower healthcare engagement due to survey selection bias
**Geographical Scope**
* Limited to U.S. counties, cannot be simply extrapolated for other populations without consideration



## Data Sources & References
**Data:**
* Centers for Disease Control and Prevention (CDC). (2025). PLACES: Local Data for Better Health, County Data, 2025 Release. Atlanta, GA: U.S. Department of Health and Human Services. https://data.cdc.gov/500-Cities-Places/PLACES-Local-Data-for-Better-Health-County-Data-20/swc5-untb.
* Centers for Disease Control and Prevention / Agency for Toxic Substances and Disease Registry / Geospatial Research, Analysis, and Services Program (CDC/ATSDR/GRASP). (2022). CDC/ATSDR Social Vulnerability Index 2022 Database, United States. https://www.atsdr.cdc.gov/place-health/php/svi/svi-data-documentation-download.html.
* National Center for Health Statistics (NCHS). (2024). 2023 NCHS Urban-Rural Classification Scheme for Counties. Centers for Disease Control and Prevention. https://www.cdc.gov/nchs/data-analysis-tools/urban-rural.html.

**Literature:**
* Gadhoumi, K., et al. (2026). Strategies for mitigating artificial intelligence bias in healthcare: a systematic review. JAMIA Open, 9(3), ooag081. https://academic.oup.com/jamiaopen/article/9/3/ooag081/8701256. 
* Neven, A. C., et al. (2026). Prevalence of polycystic ovary syndrome: a global and regional systematic review and meta-analysis. Human Reproduction Update, 32(3), 277. https://academic.oup.com/humupd/article-abstract/32/3/277/8424333?redirectedFrom=fulltext. 
* Ramphul, R., et al. (2025). Identifying Geographic Cold Spots of PCOS Diagnosis in Texas. Journal of the Endocrine Society, 9(9), bvaf123. https://academic.oup.com/jes/article/doi/10.1210/jendso/bvaf123/8221502. 
* Silva, M., et al. (2024). Polycystic Ovary Syndrome Underdiagnosis Patterns by Individual-level and Spatial Social Vulnerability Measures. The Journal of Clinical Endocrinology & Metabolism, 110(6), 1657. https://academic.oup.com/jcem/article/110/6/1657/7819206. 
* Sung, Y. A., MD, MSCP, et al. (2026). Polycystic Ovary Syndrome: An Update on Diagnosis and Management. Cleveland Clinic Journal of Medicine, 93(3), 176. https://www.ccjm.org/Content/93/3/176. 
* Teede, H. J., et al. (2026). Polyendocrine metabolic ovarian syndrome, the new name for polycystic ovary syndrome: a multistep global consensus process. The Lancet, 6, PIIS0140-6736(26)00717-8. https://www.thelancet.com/journals/lancet/article/PIIS0140-6736(26)00717-8/fulltext. 
* World Health Organization (WHO). (2026). Polycystic ovarian syndrome. WHO Fact Sheets. https://www.who.int/news-room/fact-sheets/detail/polycystic-ovary-syndrome.

## Technologies Used
* Python
* pandas/NumPy
* scikit-learn
* XGBoost
* Plotly
* Streamlit
* Google Colab

## Next Steps

