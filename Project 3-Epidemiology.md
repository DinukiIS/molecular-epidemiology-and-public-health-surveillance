# Project 3: Spatial-Temporal Predictive Modeling of Dengue Outbreaks

## 1. Executive Summary
This project outlines the development of an environmental epidemiology pipeline designed to quantify the impact of shifting climate variables on vector-borne disease dynamics. Using a 1,456-week historical dataset for San Juan, Puerto Rico, an interactive data science workflow was constructed to clean climate signals, evaluate biological lag correlations, and deploy a predictive Poisson Generalized Linear Model (GLM). The final model successfully identifies statistically significant climate thresholds that precede seasonal Dengue spikes.

## 2. Biological Logic & Time-Lagged Features
In mosquito-borne disease surveillance, immediate climate events do not trigger instantaneous clinical case reports. A distinct biological timeline must unfold:
1. Increased precipitation creates localized standing water breeding sites.
2. Larvae progress through life cycles to hatch into adult *Aedes aegypti* vectors.
3. Elevated temperatures accelerate both the mosquito replication cycle and the viral extrinsic incubation period (EIP).
4. Host exposure, infection, and clinical logging introduce a multi-week reporting delay.

To capture this mathematically, the pipeline engineered a **4-week shifted precipitation metric** (`rain_lag_4`). Exploratory data analysis verified that shifting precipitation metrics by 4 weeks yielded a substantially higher correlation coefficient with historical case rates than immediate, zero-lag recordings.

## 3. Statistical Methodology
Because infectious disease occurrence data consists of non-negative discrete integer counts ($0, 1, 2, 50, \dots$ cases per week), classical linear regression assumes inappropriate continuous normal distributions. To model this data properly, a Generalized Linear Model (GLM) utilizing a **Poisson error distribution** was deployed with a log-link function:

$$\log(E(Y)) = \beta_0 + \beta_1(\text{Average Temperature}) + \beta_2(\text{4-Week Lagged Precipitation})$$

## 4. Operational Results & Public Health Value
The `statsmodels` GLM summary provides key performance indicators for surveillance tracking:
* **P-Values ($P > |z|$):** Variables displaying values $< 0.05$ indicate factors that are statistically significant drivers of transmission dynamics.
* **Coefficients ($\beta$):** Positive parameters quantify exactly how much the expected weekly log-case count increases with every additional degree Celsius of temperature or millimeter of rainfall.

## 5. Core Competencies Demonstrated
This project demonstrates advanced analytical capability bridging macro-level environmental metrics with clinical disease surveillance data. Core technical skills include time-series data alignment, feature engineering of biological delay loops, data visualization, and generalized statistical modeling for public health early-warning intelligence.