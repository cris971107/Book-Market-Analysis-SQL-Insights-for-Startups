# A/B Test Analysis
Analyzed the performance of a new recommendation engine through an A/B test to determine if it significantly improved user conversion across the sales funnel.
---

## ⚙️ Project Type Flags

- [x] Exploratory Data Analysis (EDA)
- [x] SQL Analysis / Querying
- [x] Dashboard / Data Visualization
- [ ] Data Pipeline / ETL
- [ ] Predictive Modelling / Machine Learning
- [ ] Data Cleaning / Wrangling
- [ ] End-to-End (multiple of the above)
- [ ] Other: ___________

---

## Table of Contents
1. [Project Overview](#1-project-overview)
2. [Objectives](#2-objectives)
3. [Repository Structure](#3-repository-structure)
4. [Data Processing & Methodology](#4-data-drocessing-and-methodology)
5. [Key Insights](#5-key-insights)
6. [Deliverables](#6-deliverables)
7. [Final Verdict & Recommendations](#8-final_recomendations)
8. [Author](#7-author)

---

## 1. Project Overview

This report summarizes the statistical evaluation of an A/B test conducted to measure the impact of a new recommendation system on user behavior. By leveraging detailed event logs and user data, the analysis identifies whether the proposed changes successfully optimized the purchasing funnel or adversely affected the user experience.

---

## 2. Objectives

Primary Objective:
Compare the conversion rates and activity levels of the control group (System A) against the test group (System B).

Secondary Objective 1:
Utilize hypothesis testing (z-tests) to determine if observed differences are statistically significant or merely due to random chance.

Secondary Objective 2:
Clean and process raw interaction data to ensure metrics such as total event sums and counts are accurate for final evaluation.

---

## 3. Repository Structure

```
[project-root]/
│
├── docs/                     # Original, unmodified source data - never edited
│
├── notebooks/                # Jupyter, R Markdown, or Colab notebooks
│
└── visuals/                  # Exported charts, dashboard screenshots, ERD diagrams


```



---



## 4. Data processing and methodology

The analysis utilized a refined dataset, referred to in the code as res_clean, which aggregated user interactions.

Metric Definition: The core metrics focused on the total sum of events (sum) and the frequency of interactions (count) per unique user.

Refinement Logic: Data was processed to eliminate outliers and ensure that only relevant events within the experimental window were included in the final z-test.

# Methods Used

Descriptive statistics for event distribution per user.

Funnel analysis (Login -> Product Page -> Cart -> Purchase).

Z-test for independent proportions (Alpha = 0.05).

`visuals/Captura de pantalla 2026-03-04 000520.png`


<img width="1237" height="347" alt="Captura de pantalla 2026-03-04 000520" src="https://github.com/user-attachments/assets/099547b0-04fa-453f-9509-09ed71cd0560" />

---


## 5. Key insights

<!--
  Findings + implications. Not just what happened - what it means.

  WHAT GOOD LOOKS LIKE:
  ✅ "Return rates, not sales volume, explain Region A's underperformance.
      Region A's return rate on home goods was 34% - more than double the
      company average. Revenue was not lost at the point of sale; it was
      lost post-sale through refunds. This points to a fulfilment or
      product quality issue specific to that region, not a demand problem."

  WHAT TO AVOID:
  ❌ "Region A had lower revenue than other regions in Q4."
     (That's an observation. It describes what happened.
      An insight says what it means and where to look next.)

  Aim for 3–6 insights. Quality over quantity.
-->

The data revealed a clear trend regarding the experimental group:

Performance Degradation: The new system did not just fail to improve metrics; it actively worsened the user experience or the efficiency of the purchase funnel.

Statistical Confidence: The p-value decreased slightly during the final stages of analysis. In statistical terms, a lower p-value strengthens the rejection of the null hypothesis, confirming that the negative impact observed was not a random fluke but a consistent result of the new system.

`visuals/Captura de pantalla 2026-03-03 234335.png`
<img width="1013" height="541" alt="Captura de pantalla 2026-03-03 234335" src="https://github.com/user-attachments/assets/2779e75f-c676-41e7-954f-43ae299933a9" />

---


## 6. Deliverables

| Deliverable | Description | Location |
|-------------|-------------|----------|
| Code | Jupyter Notebook containing EDA, Funnel Visualizations, and Z-test results. | `notebooks/Sprint-15S-2.ipynb` |



---


## 7. Final verdict and recommendations

Result: The A/B test is considered a failure in terms of optimization.

Action: It is strongly recommended not to deploy the new recommendation system. Further investigation is needed to understand why the algorithm interfered with the purchase process.


---


## 8. Author

**Cristian Barrientos**

- 🔗 [https://www.linkedin.com/in/cristian-barrientos-pomposo/](https://www.linkedin.com/in/cristian-barrientos-pomposo/)
- 💼 [https://github.com/cris971107](https://github.com/cris971107)
- 📧 cristian971107@hotmail.com



