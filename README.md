# Smart-Air-Quality-Forecasting-in-Jaipur-MLR-and-SARIMA-techniques-for-NO2-prediction
Forecasting NO₂ pollution levels in Jaipur using Multiple Linear Regression with polynomial features and SARIMA time-series models. Includes full preprocessing, correlation analysis, model tuning, and visualization.

## 📋 Project Overview

This project presents a comprehensive study on air quality forecasting in Jaipur, India, focusing on NO₂ (Nitrogen Dioxide) prediction using Multiple Linear Regression (MLR) and Seasonal AutoRegressive Integrated Moving Average (SARIMA) models. The research addresses the critical need for accurate air quality prediction in emerging urban centers, where air pollution poses significant health risks.

**Supervisors:**
- Dr. Ruchi Sharma - Department of Civil Engineering
- Prof. Sudhir Kumar - Department of Civil Engineering

## 🎯 Why This Project?

### Problem Statement
- **Health Crisis**: India has 6 of the world's top 10 most polluted cities, with air pollution being the second most significant disease risk factor
- **Jaipur's Challenge**: March 2024 AQI of 190 reflects "Moderate-Poor" air quality, with Adarsh Nagar exceeding WHO daily NO₂ limits for 277 days (75.89% of 2023)
- **Research Gap**: Limited forecasting models for NO₂ in emerging urban centers like Jaipur, with most studies focusing only on metro cities

### Research Objective
**"Smart Air Quality Forecasting using MLR and SARIMA Techniques in Jaipur City"**

#### Sub-objectives:
1. Collect and preprocess air quality (NO₂) and meteorological data from CPCB monitoring stations
2. Analyze correlations between pollutants and weather parameters using Pearson's Correlation
3. Develop MLR and SARIMA models for NO₂ prediction with temporal and seasonal patterns
4. Evaluate model performance and determine optimal approach for urban NO₂ forecasting


## 🔬 How We Did It

### 1. Data Collection & Preprocessing
- **Dataset**: 61,368 data points from 6 monitoring stations (2018-2024)
- **Sources**: CPCB (primary), RSPCB (supplementary)
- **Preprocessing**: 
  - Linear interpolation for missing values
  - Outlier removal using STL decomposition, IQR, and Z-score methods
  - Seasonal trend analysis for robust data handling

### 2. Feature Selection
- **Pearson Correlation Analysis** to identify key predictors
- **Cyclic Encoding** to provide strong features in sarima model
- **Selected Features for MLR**: PM₂.₅, SO₂, NH₃, CO, AT, RH, WS, SR
- **Selected Features for SARIMA**: PM₂.₅, CO, NH₃, SO₂, AT, RH, WS, month_cos

### 3. Model Development

#### Multiple Linear Regression Approaches:
- **Baseline Linear Regression**
- **Ridge Regression** (L2 penalty)
- **Lasso Regression** (L1 penalty) 
- **ElasticNet** (L1 + L2 penalty)
- **Polynomial Features + Ridge** (Best performing)

#### SARIMA Model:
- **Best Configuration**: SARIMA(1,1,1)×(1,0,0,24)
- **Seasonal Component**: 24-hour cycle for daily patterns
- **Model Selection**: Based on AIC/BIC values

## 📊 Results

### Model Performance Comparison

#### Multiple Linear Regression
| Model | Test R² | Test RMSE |
|-------|---------|-----------|
| Baseline Linear | 0.6005 | 0.2707 |
| Ridge | 0.6005 | 0.2707 |
| Lasso | 0.6005 | 0.2707 |
| ElasticNet | 0.6005 | 0.2707 |
| **Polynomial + Ridge** | **0.6454** | **0.2551** |

#### SARIMA Models
| Model | Test R² | Test RMSE |
|-------|---------|-----------|
| SARIMA(1,1,1)×(0,0,0,24) | 0.3510 | 8.3035 |
| **SARIMA(1,1,1)×(1,0,0,24)** | **0.5233** | **8.2271** |

### Key Findings
- **MLR Performance**: Polynomial Ridge achieved R² = 0.6454, effectively capturing non-linear relationships
- **SARIMA Performance**: Best model achieved R² = 0.5233 with 5.5% mean absolute error for 24-hour forecasts
- **Meteorological Impact**: NO₂ negatively correlates with temperature (-0.45), humidity, and wind speed; positively with atmospheric pressure and PM₂.₅ (+0.65)

## 🛠️ Installation & Usage

```bash
# Clone repository
git clone https://github.com/yourusername/air-quality-forecasting.git
cd air-quality-forecasting

# Install dependencies
pip install pandas numpy scikit-learn statsmodels matplotlib seaborn scipy

# Run notebooks in order:
# 1. data_preprocessing.ipynb
# 2. correlation_analysis.ipynb  
# 3. mlr_modeling.ipynb
# 4. sarima_modeling.ipynb
```

## 📁 Project Structure

```
air-quality-forecasting/
├── data/
│   ├── raw/                    # Original CPCB/RSPCB data
│   └── processed/              # Cleaned datasets
├── notebooks/
│   ├── data_preprocessing.ipynb
│   ├── correlation_analysis.ipynb
│   ├── mlr_modeling.ipynb
│   └── sarima_modeling.ipynb
├── src/
│   ├── preprocessing.py        # Data cleaning functions
│   ├── mlr_models.py          # MLR implementations
│   ├── sarima_models.py       # SARIMA implementations
│   └── evaluation.py          # Model evaluation metrics
├── results/
│   ├── figures/               # Plots and visualizations
│   └── predictions/           # Model forecasts
└── README.md
```

## 🔍 Monitoring Stations

1. **Adarsh Nagar** (N 26° 54' 9" E 75° 50' 12") - 2018-2024
2. **Police Commissionerate** (N 26° 54' 45" E 75° 47' 12") - 2018-2024  
3. **Shastri Nagar** (N 26° 56' 29" E 75° 47' 50") - 2018-2024
4. **Sitapura** (26.7751° N, 75.8514° E) - 2023-2024
5. **Murlipura** (26.9776° N, 75.7639° E) - 2023-2024
6. **Mansarovar** (26.8505° N, 75.7628° E) - 2023-2024

### Data Sources
- Primary: Central Pollution Control Board (CPCB)
- Secondary: Rajasthan State Pollution Control Board (RSPCB)

## 📈 Quick Example

```python
# Load and preprocess data
from src.preprocessing import preprocess_data
data = preprocess_data('data/raw/jaipur_air_quality.csv')

# Train MLR model
from src.mlr_models import PolynomialRidgeRegression
mlr_model = PolynomialRidgeRegression()
mlr_model.fit(X_train, y_train)

# Train SARIMA model  
from src.sarima_models import SARIMAModel
sarima_model = SARIMAModel(order=(1,1,1), seasonal_order=(1,0,0,24))
sarima_model.fit(time_series_data)

# Generate forecasts
mlr_forecast = mlr_model.predict(X_test)
sarima_forecast = sarima_model.forecast(steps=24)
```

## 🎯 Project Significance

This major project addresses a critical environmental and public health challenge by:
- Providing the first comprehensive NO₂ forecasting study for Jaipur
- Developing reliable prediction models for urban air quality management
- Enabling proactive measures to protect public health from air pollution
- Contributing to sustainable urban development planning

## 📚 Key References

1. Central Pollution Control Board (CPCB) - Air Quality Data
2. Rajasthan State Pollution Control Board (RSPCB) - Supplementary Data
3. WHO Air Quality Guidelines
4. Relevant research papers on SARIMA and MLR for air quality prediction


**⭐ If you find this project helpful, please consider giving it a star!**
