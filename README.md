# StudentLife Productivity Analysis

A time-series analysis investigating the relationship between smartphone usage patterns and student well-being using the StudentLife dataset from Dartmouth College.

## Overview

This project examines whether smartphone behaviors (unlock patterns, screen time, nighttime usage) can predict student productivity and mood. Using time-series models including ARIMA, SARIMA, VAR, and linear regression with bootstrap confidence intervals, we analyze temporal relationships between digital behavior and psychological outcomes.

**Key Finding:** Simple phone usage metrics (frequency, duration, timing) show minimal predictive power for student productivity and well-being. Psychological state drives phone behavior rather than the reverse.

## Research Questions

1. **RQ1:** How do smartphone behaviors (unlock patterns, screen time, activity) relate to daily productivity?
2. **RQ2:** How does well-being (stress, sleep, mood, activity, sociability) correlate with productivity and predict changes over time? Does smartphone usage play a mediating role?

## Dataset

**StudentLife Dataset** (Dartmouth College, 2013)
- 48 students tracked over 10 weeks
- Passive smartphone sensing: activity, phone lock/unlock events, location
- Ecological Momentary Assessments (EMA): mood (PAM), stress, productivity
- Publicly available, anonymized dataset

**Dataset Access:** [StudentLife Dataset](https://studentlife.cs.dartmouth.edu/)

## Methods

### Statistical Approaches
- **Linear Regression** with bootstrap confidence intervals (2,000 iterations)
- **ARX(1)** - Autoregressive models with exogenous variables
- **VAR(1)** - Vector autoregressive models for bidirectional relationships
- **ARIMA** - AutoRegressive Integrated Moving Average models
- **SARIMA** - Seasonal ARIMA with weekly periodicity (s=7)

### Key Variables
- `unlock_rate`: Phone unlocks per hour
- `avg_session_sec`: Mean duration of phone usage sessions
- `nighttime_ratio`: Proportion of usage during dark periods
- `pam_mean`: Daily average mood score
- `productivity`: Self-reported productivity ratings
- `stress`: Self-reported stress levels

## Key Results

### Phone Usage vs Productivity
- **Total usage time:** No relationship (β = 0.0003, 95% CI: [-0.0012, 0.0018])
- **Checking frequency:** Positive association (β = 0.042, 95% CI: [0.015, 0.068]), likely due to reverse causality
- **Forecasting:** ARIMA and SARIMA models showed poor predictive accuracy (40-50% MAE)

### Mood and Behavior
- Strong mood persistence across days (VAR coefficient = 6.90, p = 0.001)
- Mood predicts next-day phone checking (coefficient = 0.0088, p = 0.008)
- Phone usage does not predict next-day mood

### Time-Series Forecasting
- **ARIMA(1,1,0):** Best model by AIC (43.67), but 35-45% forecast error
- **SARIMA(1,1,0)(1,0,0,7):** Better in-sample fit (AIC = 23.15) but no improvement in predictions
- Seasonal component non-significant (p = 0.684)
- Wide confidence intervals (20-30 points) indicate high uncertainty


## Installation

### Prerequisites
- Python 3.8+
- Jupyter Notebook/Lab

### Setup

1. **Clone the repository:**
```bash
git clone https://github.com/ChowdhuryFarzana/studentlife-productivity-analysis.git
cd studentlife-productivity-analysis
```

2. **Create virtual environment (recommended):**
```bash
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
```


### Required Packages
```
numpy>=1.21.0
pandas>=1.3.0
matplotlib>=3.4.0
seaborn>=0.11.0
scipy>=1.7.0
statsmodels>=0.13.0
scikit-learn>=0.24.0
jupyter>=1.0.0
```


## Main Findings

1. **No Predictive Power:** Phone usage metrics fail to predict future productivity (40-50% forecast errors)

2. **Reverse Causality:** The positive relationship between checking frequency and productivity likely reflects that productive students feel comfortable taking breaks

3. **Mood Drives Behavior:** Students in better moods check phones more frequently the next day, not vice versa

4. **Context Matters:** Productivity depends on unmeasured factors (deadlines, sleep, social events) that passive sensing cannot capture

5. **Content Over Quantity:** What students do on phones likely matters more than frequency or duration

## Limitations

- High missingness in productivity (90.6%) and stress (57.5%) variables
- Short observation period (10 weeks, 14-20 observations per user)
- Sample limited to Dartmouth students in 2013
- Passive sensing cannot distinguish app content
- No subjective measures of problematic usage

## Future Directions

- Incorporate richer contextual features (sleep, activity, location, academic calendar)
- Classify phone usage by content type (educational vs social vs entertainment)
- Explore different temporal lags (hourly, multi-day, weekly)
- Build personalized models for individual users
- Use non-linear methods (random forests, neural networks)
- Add subjective measures of digital well-being

## Related Publications

**Original StudentLife Dataset:**
- Wang, R., et al. (2014). "StudentLife: Assessing mental health, academic performance and behavioral trends of college students using smartphones." *UbiComp 2014*.

**Related Work:**
- Wang, R., et al. (2015). "SmartGPA: How smartphones can assess and predict academic performance of college students." *UbiComp 2015*.
- Huckins, J. F., et al. (2020). "Mental health and behavior of college students during the early phases of the COVID-19 pandemic." *JMIR*.


## Acknowledgments

- StudentLife dataset provided by Dartmouth College, and kaggle community
- Mount Holyoke College for Data Science class 
- Project Advisor Arie Shaus for mentorship
