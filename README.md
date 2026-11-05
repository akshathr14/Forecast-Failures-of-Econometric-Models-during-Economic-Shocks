# Forecast Failures of Econometric Models during Economic Shocks

### **Project Objective**
This research evaluates the forecasting limitations of statistically significant econometric models during extreme market volatility, specifically focusing on the **2007-08 Global Financial Crisis** and the **2020 COVID-19 Pandemic**.

### **Technical Stack**
* **Languages:** R (Original Research) & Python (Current Technical Port).
* **Model Architecture:** ARIMAX (ARIMA with Exogenous Regressors).
* **Libraries:** `yfinance`, `statsmodels`, `scipy`, `scikit-learn` (used for mean absolute error).
* **Data Source:** Daily historical values from Yahoo Finance (1998–2020).

### **Methodology & Rigor**
* **Variable Selection:** Modeled the **S&P 500** index using the DJIA, Nasdaq, Russell 2000, VIX, and 10-year Treasury yields.
* **Statistical Diagnostics:**
    * **Stationarity (ADF):** Verified using Augmented Dickey-Fuller (ADF) tests and ACF/PACF plots. Log prices are not stationary (p = 0.82) and daily changes are (p < 0.0001), which supports first differencing.
    * **Heteroskedasticity:** Identified via Breusch-Pagan tests(p<0.0001) but log transform reduces the scale but does not remove it.
    * **Autocorrelation:** Evaluated using the Durbin-Watson test on the residuals of the model fitted before the 2008 shock (2.0, so little autocorrelation).

### **Key Results**
The project utilized **ARIMA(1,1,1)** models to compare forecasting performance against real-world "Black Swan" events:

| Scenario | P-Value (Significance) | MAE (Error Magnitude) | Status |
| :--- | :--- | :--- | :--- |
| **2008 Financial Crisis** | **8.3e-07** | **30.09** | **Systemic Failure** |
| **2020 COVID-19 Pandemic** | **6.1e-08** | **24.47** | **Systemic Failure** |

* **2007-08 Financial Crisis:** Identified a statistically significant failure in mean predictions, confirming that models calibrated on "normal" periods cannot account for systemic feedback loops.
* **COVID-19 Pandemic:** Confirmed forecast failure during the February 2020 market crash, highlighting the "Accuracy Gap" created by extrinsic unpredictability.


### **Strategic Conclusion**
The study concludes that relying solely on econometric models for economic forecasting is risky during periods of shock. Resilient policy frameworks require **diversified forecasting tools**, **scenario analysis**, and **qualitative assessments** to manage the uncertainties associated with global financial systems.


### **Limitations**
* Each shock is tested over a short window (about 10 trading days), so the results describe two specific episodes.
* Forecasts use the realised values of the exogenous variables over the test window, so they are conditional forecasts, not live forecasts.
* The paired t-test treats daily index levels as independent although they are autocorrelated, so the p-values overstate significance. MAE is the more reliable measure of the miss.
* The Breusch-Pagan test still indicates heteroskedasticity after the log transformation.
* statsmodels reports a convergence warning for one of the model fits.
