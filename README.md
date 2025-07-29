# Carbon Emissions Impact Analysis: A Time-Series and Predictive Study

## Project Overview

This project undertakes a comprehensive data analysis to explore the intricate relationship between global atmospheric carbon dioxide (CO₂) concentrations and global temperature changes over several decades. Utilizing time-series analysis, correlation, causality testing, advanced regression with lagged effects, and machine learning-based clustering, the study aims to quantify the impact of CO₂ on temperature and provide predictive insights into potential future climate scenarios.

## Problem Statement

Global warming and climate change represent one of humanity's most pressing challenges. The scientific consensus points to anthropogenic greenhouse gas emissions, particularly CO₂, as a primary driver. However, understanding the historical patterns, quantifying the statistical relationships, identifying distinct climate epochs, and building predictive models for "what-if" scenarios based on these emissions are crucial for informed decision-making, policy formulation, and climate mitigation strategies.

## Project Objectives

1.  **Exploratory Data Analysis (EDA):** Perform initial statistical analysis to understand the distributions and characteristics of temperature change and CO₂ concentration data.
2.  **Trend and Seasonal Analysis:** Identify long-term trends and examine seasonal variations in both temperature changes and CO₂ concentrations.
3.  **Relationship Quantification:** Quantify the correlation between CO₂ levels and temperature changes using various statistical measures.
4.  **Causality Investigation:** Employ Granger causality tests to explore potential lead-lag predictive relationships between CO₂ and temperature, considering the time-series nature of the data.
5.  **Lagged Effects Modeling:** Build a regression model to assess how current and past CO₂ concentrations collectively influence current temperature changes.
6.  **Climate Pattern Identification:** Utilize clustering techniques to group historical years into distinct climate patterns based on their combined temperature and CO₂ characteristics.
7.  **"What If" Scenario Prediction:** Develop a simple predictive model to simulate temperature changes under hypothetical future CO₂ emission scenarios.

## Column Dictionaries

### `temperature.csv`

This dataset contains global temperature change anomalies.

| Column Name  | Description                                                                                             |
| :----------- | :------------------------------------------------------------------------------------------------------ |
| `ObjectId`   | Unique identifier for each data entry.                                                                  |
| `Country`    | The geographical entity for which the data is recorded (e.g., 'World').                                 |
| `ISO2`       | Two-letter ISO country code.                                                                            |
| `ISO3`       | Three-letter ISO country code.                                                                          |
| `FYYYY`      | Global average temperature change anomaly for a specific year `YYYY` (e.g., `F1961`, `F2022`). Values are typically in degrees Celsius (°C) relative to a baseline period. |

### `carbon_emmission.csv`

This dataset contains global atmospheric carbon dioxide (CO₂) concentrations.

| Column Name  | Description                                                                                             |
| :----------- | :------------------------------------------------------------------------------------------------------ |
| `ObjectId`   | Unique identifier for each data entry.                                                                  |
| `Country`    | The geographical entity for which the data is recorded (e.g., 'World').                                 |
| `Date`       | The date of the measurement in `YYYYMM` format (e.g., `1958M03` for March 1958).                         |
| `Value`      | Atmospheric CO₂ concentration in parts per million (ppm). Note: For some dates, multiple entries exist; this analysis primarily used the aggregated (mean) values as CO₂ concentration. |

## Analysis Highlights & Key Findings

### 1\. Initial Data Overview & Statistics

  - **CO₂ Data:** Exhibited very high variance, indicating substantial changes over time, and showed a left-skewed distribution, reflecting the increasing trend with more recent higher values.
  - **Temperature Data:** Showed a more moderate variance but a clear upward trend in its mean and median, signaling warming.

### 2\. Time-Series Analysis: Trends Unveiled

  - Both **global temperature change and CO₂ concentrations display clear, strong, and remarkably parallel upward trends** over the decades. This visual correlation is the first compelling evidence of their linked progression.

### 3\. Correlation Quantification: A Strong Link

  - **Correlation Heatmap and Scatter Plot:** Quantified a **very strong positive linear correlation (Pearson: \~0.955; Spearman: \~0.938)** between CO₂ concentration and temperature change. This robust numerical finding unequivocally supports the visual evidence of a direct relationship, where rising CO₂ is associated with increasing temperatures.

### 4\. Trends & Seasonal Patterns: Deeper Dive

  - **Quantified Linear Trends:** The analysis determined an average global temperature increase of approximately **0.02°C per year** and an average CO₂ concentration increase of about **1.63 ppm per year**.
  - **CO₂ Seasonal Variation:** A distinct annual cycle in CO₂ concentrations was observed, with peaks in late spring/early summer and troughs in autumn. This pattern is consistent with the seasonal biological activity (photosynthesis and respiration) primarily in the Northern Hemisphere's vast landmasses.

### 5\. Causality Investigation: Predictive Relationship

  - **Granger Causality Test:** While Pearson and Spearman correlations showed strong association, the Granger causality test (at 1-3 year lags) provided **weak statistical evidence (p-value for Lag 1 was 0.0617, others higher)** for CO₂ concentration "Granger-causing" temperature change within this specific econometric framework. This highlights the complexity of climate systems, where responses might involve longer lags, non-linearities, or other confounding factors not fully captured by this test alone.

### 6\. Lagged Effects Analysis: Unpacking the Influence

  - **OLS Regression Model:** A robust model was built, explaining approximately **95% of the variance** in temperature change using current and lagged CO₂ concentrations.
  - **Key Predictors:**
      - **Current CO₂ Concentration** showed a highly statistically significant positive impact.
      - **1-year Lagged CO₂ Concentration** also exhibited a statistically significant effect, though with a negative coefficient (likely influenced by multicollinearity with current CO₂).
      - CO₂ concentrations from **2 and 3 years prior did not show statistically significant additional impacts** in this model, suggesting the most dominant effects are relatively immediate or captured within the preceding year.
  - **Multicollinearity:** A high condition number in the OLS results indicated strong multicollinearity among the lagged CO₂ variables, which can make individual coefficient interpretations challenging but does not invalidate the overall model's predictive power.

### 7\. Climate Pattern Clustering: Identifying Epochs

  - **K-Means Clustering:** Years were successfully clustered into three distinct "climate patterns":
      - **'Low Temp & CO₂':** Representing earlier periods with minimal warming.
      - **'Moderate Temp & CO₂':** A transitional phase.
      - **'High Temp & CO₂':** Encompassing recent decades with significant warming and elevated CO₂ levels.
  - This clustering visually confirms a **clear historical progression** through these climate states, driven by increasing CO₂ and leading to higher global temperatures.

### 8\. "What If" Analysis: Future Scenario Predictions

  - A simple linear regression model was used to predict temperature changes under hypothetical CO₂ scenarios:
      - **+10% CO₂:** Predicted temperature change of \~1.087°C.
      - **-10% CO₂:** Predicted temperature change of \~-0.060°C.
      - **+20% CO₂:** Predicted temperature change of \~1.660°C.
      - **-20% CO₂:** Predicted temperature change of \~-0.633°C.
  - These predictions dramatically illustrate the **sensitivity of global temperatures to CO₂ concentrations**, providing tangible insights into the potential warming from increased emissions and the mitigation potential of reduction efforts.

## Technologies Used

  * **Python:** Programming Language
  * **Pandas:** Data Manipulation and Analysis
  * **NumPy:** Numerical Operations
  * **Plotly:** Interactive Data Visualization
  * **Scikit-learn (sklearn):** Machine Learning (Linear Regression, KMeans, StandardScaler)
  * **SciPy:** Scientific Computing (e.g., `linregress`, `pearsonr`, `spearmanr`)
  * **Statsmodels:** Statistical Modeling (e.g., OLS Regression, Granger Causality)

## How to Run the Code

1.  **Clone the repository:**
    ```bash
    git clone <repository-url>
    cd <repository-name>
    ```
2.  **Install dependencies:**
    ```bash
    pip install pandas numpy plotly scikit-learn scipy statsmodels
    ```
3.  **Place Data:** Ensure `carbon_emmission.csv` and `temperature.csv` are in the root directory of the repository.
4.  **Execute:** Run the Python script containing the analysis steps in your preferred environment (e.g., Jupyter Notebook, IDE).

-----
