# Daily Rainfall Estimation and Agricultural Weather Analysis for Anuradhapura, Sri Lanka

**Student:** Sithum Wickramanayaka  
**Student ID:** 269214N

## Problem

This project analyses historical weather conditions in Anuradhapura and develops a Python regression model that estimates daily rainfall. The main, guideline compliant solution uses Gradient Boosting with current weather, calendar patterns, and leakage safe features calculated only from previous days. An optional two-stage extension first classifies whether meaningful rain will occur and then estimates the amount on rainy days. The work is relevant to agricultural planning and water management in Sri Lanka, where rainfall varies by season and location.

The model is an educational historical data estimation solution, not an operational weather forecast, because it uses measurements from the day being estimated. On the chronological 2023–2024 test set, the primary model achieved MAE 2.756 mm, RMSE 6.602 mm, and R-squared 0.524. The optional extension achieved classification accuracy 0.862, precision 0.845, recall 0.863, F1-score 0.854, MAE 2.754 mm, and R-squared 0.530.

## Dataset

- **Source:** NASA POWER Project
- **Location:** Anuradhapura, Sri Lanka
- **Coordinates:** 8.3114° N, 80.4037° E
- **Period:** 1 January 2015 to 31 December 2024
- **Records:** 3,653 daily observations
- **Source variables:** 15
- **Format:** CSV
- **Target variable:** `PRECTOTCORR` - corrected precipitation in mm/day
- **Daily API documentation:** https://power.larc.nasa.gov/docs/services/api/temporal/daily/
- **Parameter dictionary:** https://power.larc.nasa.gov/parameters/
- **Dataset request:** https://power.larc.nasa.gov/api/temporal/daily/point?parameters=T2M,T2M_MAX,T2M_MIN,T2MDEW,T2MWET,RH2M,QV2M,WS2M,WD2M,PS,PRECTOTCORR,ALLSKY_SFC_SW_DWN,CLOUD_AMT&community=AG&longitude=80.4037&latitude=8.3114&start=20150101&end=20241231&format=CSV

The source variables include temperature, dew point, wet-bulb temperature, relative and specific humidity, wind speed and direction, atmospheric pressure, solar irradiance, cloud amount, and corrected precipitation. The dataset contains no personal or confidential information. NASA documents `-999` as its missing data marker; no such missing observations were found in the downloaded daily records. NASA POWER is gridded satellite/reanalysis-derived data rather than a local rain gauge record.

## Models and evaluation

- Linear Regression, Random Forest, and Gradient Boosting are compared using the same chronological test period.
- Gradient Boosting remains the main regression model and has the best MAE among those three models.
- The optional two-stage extension defines meaningful rain as at least 1.0 mm/day, uses a Random Forest classifier, and applies conditional Gradient Boosting regression when rain is detected.
- The notebook includes accuracy, precision, recall, F1-score, a confusion matrix, a residual-error graph, a model-comparison chart, and separate errors for dry/trace, normal rainy, and heavy-rainfall days.
- The confusion matrix contains 335 correctly identified dry/trace days, 54 false rain alerts, 47 missed rainy days, and 295 correctly identified rainy days.

No frontend or separate user input interface is included. All implementation and results are contained in the notebook.

## Required Python libraries

- Pandas
- NumPy
- Matplotlib
- Scikit-learn
- Jupyter Notebook

## How to run

1. Extract the ZIP file.
2. Keep `rainfall_analysis.ipynb` and `anuradhapura_daily_weather_2015_2024.csv` in the same folder.
3. Open a terminal in the extracted folder.
4. Install the required libraries:

   `pip install pandas numpy matplotlib scikit-learn notebook`

5. Start Jupyter Notebook:

   `jupyter notebook`

6. Open `rainfall_analysis.ipynb`.
7. Select **Kernel > Restart & Run All**.
8. Confirm that all cells run without errors and display the analysis, charts, model comparisons, confusion matrix, and rainfall estimates.

## Main project files

- `rainfall_analysis.ipynb` - complete executable Python solution and results
- `anuradhapura_daily_weather_2015_2024.csv` - expanded NASA POWER dataset
- `269214N_Daily_Rainfall_Estimation_Anuradhapura.pptx` - presentation-powerpoint version
- `269214N_Daily_Rainfall_Estimation_Anuradhapura.pdf` - presentation-pdf version
- `Recorded_Presentation.mp4` - presentation video
- `Figures Directory` - contains charts and figures of the model.
- `Readme.md` - readme file

## Acknowledgements

Rainfall-season context was checked using the Department of Census and Statistics, Sri Lanka: https://www.statistics.gov.lk/abstract2024/chapter1

Scikit-learn Gradient Boosting documentation: https://scikit-learn.org/stable/modules/generated/sklearn.ensemble.GradientBoostingRegressor.html

Scikit-learn Random Forest documentation for the comparison model: https://scikit-learn.org/stable/modules/generated/sklearn.ensemble.RandomForestRegressor.html

Scikit-learn Random Forest classifier documentation for the optional rain/no-rain stage: https://scikit-learn.org/stable/modules/generated/sklearn.ensemble.RandomForestClassifier.html
