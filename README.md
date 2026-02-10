# REAL-TIME DATA FORECASTING WITH AI AND PYTHON

<img width="218" height="181" alt="edf" src="https://github.com/user-attachments/assets/775e8cc1-f6ec-4ead-8cbf-04cf781f1bc8" />


<img width="1536" height="1024" alt="efd" src="https://github.com/user-attachments/assets/b685e612-2bcb-4a4d-b2c7-773d62ed593d" />

# AI-Driven Multi-Day Energy Demand Forecasting for ISO Planning
Reliable energy demand forecasting is a foundational requirement for Independent System Operators (ISOs) and National Energy System Operators (NESOs). Accurate short- to medium-term forecasts support operational scheduling, network reliability, market efficiency, and long-term whole-system planning across electricity, gas, hydrogen, and emerging low‑carbon vectors.

This report documents an end-to-end case study involving the development of an AI‑driven, batch-trained energy demand forecasting system capable of producing 1‑day, 2‑day, and 3‑day ahead forecasts. The work demonstrates how advanced data engineering, feature stores, and machine‑learning models can be operationalised to support ISO decision‑making, regional energy strategy planning, and evidence‑based policy development.

# # Data Sources and Context  
# # Energy Demand Data


The primary dataset consists of time‑stamped energy demand measurements provided in CSV format. The data represents aggregated system‑level demand suitable for ISO‑level operational analysis.

Key characteristics:

High‑resolution time series data

Converted to daily aggregates to align with short‑term operational planning horizons

Indexed by timestamp (period) for temporal consistency

#  Operational Context

The modelling objective aligns with ISO use cases such as:

Day‑ahead and multi‑day scheduling

Reserve planning and system adequacy checks

Anticipating short‑term demand fluctuations for network coordination

# Data Preprocessing
# Temporal Resampling

Raw demand data is resampled to a daily frequency using summation, ensuring consistency with daily planning cycles:

Converts sub‑daily noise into stable daily signals

Improves model robustness

Aligns with ISO operational reporting intervals

# Handling Missing Values

Lagged and rolling features inherently introduce missing values at the start of the time series. These rows are systematically removed to ensure:

Clean model inputs

No data leakage from future values

# Feature Engineering

Feature engineering is central to capturing demand dynamics. The following categories were implemented.

# Lagged Demand Features

Lag features capture temporal dependencies and consumption inertia:

Short‑term memory: lag_1

Weekly structure: lag_4, lag_5, lag_6

Bi‑weekly structure: lag_11, lag_12, lag_13

These lags allow the model to learn recurring behavioural and operational patterns.

4.2 Rolling Statistics

Rolling statistics summarise recent demand trends:

7‑day rolling mean: captures baseline demand level

7‑day rolling standard deviation: captures volatility and uncertainty

These features are particularly valuable for anticipating unstable operating conditions.

# Calendar Effects – Day of Week

A day‑of‑week categorical feature was introduced to model systematic behavioural differences between weekdays and weekends.

Computed directly from the timestamp

Stored as an integer (0–6) or optionally one‑hot encoded

Enables the model to distinguish operational vs non‑operational days

# Feature Store Design

A lightweight feature store was implemented to ensure reproducibility, traceability, and scalability.

# Feature Store Components

Versioned YAML configuration (config_v1, config_v2)

CSV‑based storage for features and targets

Metadata tracking:

Latest feature date

Latest target date

Forecast offsets

# Benefits for ISO Workflows

Clear separation between data engineering and modelling

Enables batch retraining and incremental updates

Supports auditability and regulatory transparency

# Target Engineering

To support direct multi‑horizon forecasting, three target variables were defined:

target_1d: demand at t + 1 day

target_2d: demand at t + 2 days

target_3d: demand at t + 3 days

This structure avoids recursive forecasting error accumulation and aligns with ISO planning horizons.

# Model Development
7.1 Algorithm Selection

XGBoost regression was selected due to:

Strong performance on tabular time‑series features

Ability to model non‑linear relationships

Robustness with limited feature sets

# Multi‑Model Strategy

Rather than a single output model, three independent models were trained:

One model per forecast horizon (1‑day, 2‑day, 3‑day)

This allows each model to specialise in its specific temporal uncertainty structure.

# Model Training and Validation
# Cross‑Validation

K‑fold cross‑validation (4–5 folds)

Early stopping based on RMSE

Prevents overfitting and improves generalisation

# Evaluation Metrics

RMSE: absolute forecasting accuracy

R²: explanatory power of engineered features

Observed results showed reasonable short‑term accuracy, with increasing uncertainty at longer horizons, consistent with real‑world system behaviour.

# Inference and Evaluation
# Batch Inference

Latest features fetched from the feature store

Predictions generated for all three horizons

Timestamped outputs aligned with operational dates

# Actual vs Predicted Analysis

Predictions joined with realised demand

Visual comparison highlighted:

Strong alignment for 1‑day ahead forecasts

Gradual degradation for 2‑ and 3‑day horizons

This behaviour reflects increasing system uncertainty rather than model failure.
<img width="1187" height="547" alt="1, 2 ,3 dayy ahead" src="https://github.com/user-attachments/assets/40ce81cb-cd61-4e5e-bca8-3be1861711b7" />



# Key Findings and Insights

Lagged demand and rolling statistics are highly informative for short‑term ISO forecasting

Calendar effects significantly improve stability

Direct multi‑horizon modelling avoids error compounding

Feature stores enhance operational readiness and governance

# Benefits to ISO and Whole‑System Planning

This modelling framework supports:

Operational scheduling and reserve planning

Demand‑led network stress assessment

Evidence‑based regional energy strategy development

Scalable integration with future weather, EV, heat, and hydrogen demand drivers

The approach demonstrates how AI can be responsibly embedded into ISO planning workflows.

# Conclusion

This case study illustrates a complete AI lifecycle, from raw data ingestion to inference tailored for ISO‑level energy planning. By combining robust feature engineering, structured feature storage, and interpretable machine‑learning models, the solution delivers practical multi‑day demand forecasts that directly support system reliability and strategic decision‑making.

The work evidences the ability to translate advanced analytics into operational value, reinforcing the role of AI‑driven solutions in whole‑system energy planning.

# References

Chen, T. & Guestrin, C. (2016). XGBoost: A Scalable Tree Boosting System.

ISO New England / National Grid ESO – Demand Forecasting Practices

Hyndman, R. & Athanasopoulos, G. (2021). Forecasting: Principles and Practice

Open Energy Modelling Initiative (OpenEM)


## Branches
The branches are structured to correspond to the videos in the course. The naming convention is `CHAPTER#_MOVIE#`. As an example, the branch named `02_03` corresponds to the second chapter and the third video in that chapter. 
Some branches will have a beginning and an end state. These are marked with the letters `b` for "beginning" and `e` for "end". The `b` branch contains the code as it is at the beginning of the movie. The `e` branch contains the code as it is at the end of the movie. The `main` branch holds the final state of the code when in the course.

When switching from one exercise files branch to the next after making changes to the files, you may get a message like this:

    error: Your local changes to the following files would be overwritten by checkout:        [files]
    Please commit your changes or stash them before you switch branches.
    Aborting

To resolve this issue:
	
    Add changes to git using this command: git add .
	Commit changes using this command: git commit -m "some message"


# KAMIL RIDWAN KEHINDE

[0]: # (Replace these placeholder URLs with actual course URLs)

[lil-course-url]: https://www.linkedin.com/learning/ai-powered-time-series-forecasting-with-python
[lil-thumbnail-url]: https://media.licdn.com/dms/image/v2/D560DAQE7VhDbYtARPw/learning-public-crop_675_1200/learning-public-crop_675_1200/0/1723244697974?e=2147483647&v=beta&t=HCf5rgCpyIXardWyxrg5J5egVF8N1nArE8xu-BWgMkU

