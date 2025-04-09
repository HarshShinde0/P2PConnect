# **Comprehensive Report on Air Quality Prediction and Modeling**

## **Objective**
The goal of this project was to analyze, model, and predict air quality pollutants such as Methane, Acetone, Benzene, and Toluene using real-world data from Ameya Paper Mills. Specifically, the focus was on understanding correlations, building predictive models, and forecasting pollutant levels for the next 24 hours.

---

## **Steps and Methodologies**

### **1. Data Loading and Preprocessing**
- **Data Source:** The dataset was loaded from an Excel file.
- **Initial Cleaning:**
  - Removed unnecessary headers and skipped rows.
  - Converted the `Timestamp` column to datetime format.
  - Removed duplicate entries based on timestamps.
  - Sorted the data by time and set the `Timestamp` as the index.
- **Target Variables for Modeling:**
  - Methane (ppm)
  - Acetone (ug/m3)
  - Benzene (ug/m3)
  - Toluene (ug/m3)

### **2. Feature Engineering**
- **Lag Features:** Added lagged versions of the target variables and `VOC (Grades - 0 to 3)` to capture temporal dependencies.
- **Handling Missing Data:** Dropped rows with NaN values caused by lagging.

---

### **3. Predictive Modeling**
#### **Model 1: XGBoost Regression**
- A multi-output regression model was built using XGBoost (`xgboost.XGBRegressor`) to predict the target pollutants.
- **Data Splitting:**
  - Data was split into training and testing sets (80% training, 20% testing) without shuffling to retain temporal consistency.
- **Model Training:**
  - Trained the XGBoost model using `MultiOutputRegressor`.
- **Evaluation Metrics:**
  - RMSE (Root Mean Squared Error)
  - MAE (Mean Absolute Error)
  - R² Score
- **Visualization:**
  - Plotted actual vs. predicted values for each pollutant.

#### **Model 2: LSTM Neural Network**
- Built a Long Short-Term Memory (LSTM) neural network for time-series prediction of pollutants.
- **Data Preparation:**
  - Standardized the data using `StandardScaler`.
  - Created sequences with a lookback window of 24 hours.
  - Split the data into training and testing sets (80% training, 20% testing).
- **Model Architecture:**
  - LSTM layer with 64 units.
  - Dense layers for multi-output regression.
  - Optimized using the Adam optimizer and MSE loss function.
  - Early stopping used to avoid overfitting.
- **Evaluation:**
  - RMSE, MAE, and R² metrics were calculated for each pollutant.
  - Visualized actual vs. predicted values for pollutants.

---

### **4. Comparative Analysis**
- Combined the results of XGBoost and LSTM models into a single dataframe for comparison.
- Plotted RMSE values for both models to identify the better-performing model for each pollutant.

---

### **5. Correlation Analysis**
- Analyzed correlations between `VOC (Grades - 0 to 3)` and individual pollutants.
- Plotted a heatmap for the correlation matrix.
- Observed significant relationships between `VOC` and pollutants like Methane, Acetone, Benzene, and Toluene.

---

### **6. Linear Regression for VOC vs Pollutants**
- Investigated linear relationships between `VOC (Grades - 0 to 3)` and each pollutant using `LinearRegression`.
- Visualized scatter plots with regression lines and reported R² scores for each relationship.

---

### **7. Time-Series Forecasting**
#### **LSTM-Based 24-Hour Forecast**
- Extended the LSTM model to forecast pollutant levels for the next 24 hours.
- **Forecasting Methodology:**
  - Prepared input sequences using the last 24 hours of data.
  - Predicted pollutant levels for the next 24 hours.
- **Inverse Transformation:**
  - Used the scaler to reverse-transform the standardized predictions into their original scale.
- **Visualization:**
  - Plotted 24-hour forecasts for each pollutant.
  - Created a forecast table with time indices and pollutant levels.

---

### **8. Model Deployment**
- Saved the trained models:
  - XGBoost model saved as `xgb_model.pkl`.
  - LSTM forecasting model saved as `lstm_forecast_model.keras`.
- Exported the results:
  - Model comparison results saved as `model_comparison_results.csv`.
  - 24-hour forecasts saved as `24hr_forecast_pollutants.csv`.

---

## **Key Results**
1. **XGBoost vs LSTM Performance:**
   - RMSE and R² scores varied for different pollutants, but the LSTM model generally outperformed XGBoost in capturing temporal dependencies.
2. **Correlation Insights:**
   - Strong correlations were observed between `VOC` and pollutants like Methane and Benzene.
3. **24-Hour Forecast:**
   - Successfully forecasted pollutant levels for the next 24 hours with reasonable accuracy.
4. **Linear Relationships:**
   - Regression analysis confirmed linear trends between `VOC` and individual pollutants.

---

## **Visual Outputs**
1. **Actual vs Predicted Values:**
   - Line plots comparing actual and predicted pollutant levels for both XGBoost and LSTM models.
2. **Correlation Heatmap:**
   - Visualized the relationships between `VOC` and pollutants.
3. **Regression Plots:**
   - Scatter plots with regression lines for `VOC` vs pollutants.
4. **24-Hour Forecasts:**
   - Line charts showing predicted pollutant levels for the next 24 hours.

---

## **Conclusion**
This project successfully demonstrated the use of machine learning and deep learning models for air quality prediction. The insights gained from correlation analysis, linear regression, and time-series forecasting can be valuable for environmental monitoring and decision-making.

**Artifacts:**
- Trained models: `xgb_model.pkl`, `lstm_forecast_model.keras`
- Forecast CSV: `24hr_forecast_pollutants.csv`
- Model comparison CSV: `model_comparison_results.csv`
