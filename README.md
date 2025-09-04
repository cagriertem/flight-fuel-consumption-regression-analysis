# ✈️ Flight Fuel Consumption, Regression Analysis

This project analyzes flight data from January 2025 to identify patterns in fuel consumption and develop predictive models for operational efficiency.

## 📊 Dataset Overview
- Number of Flights: 56
- Time Period: January 2025
- Features: Departure & arrival airports, fuel levels, times, durations, and encoded route IDs


## 1. Preprocessing

- **Aircraft Type**: Dropped (only one type available).  
- **Missing Values**: Removed rows with missing Departure/Arrival Airports.  
- **Time Formatting**: Standardized "Departure Time" and "Arrival Time" to `HH:MM`.  

### Feature Engineering
Added several derived columns for analysis:
- `fuel_consumption` = Fuel at Departure – Fuel at Arrival  
- `distance_km` = Distance for each destination using Airport Codes 
- `fuel_per_km` = fuel_consumption ÷ distance_km  
- `speed_km/h` = distance_km ÷ flight_duration  

**Dropped Columns**: Removed identifiers and redundant columns (e.g., `No`, `Fl. Nb`, `airport_pair`).

---

## 2. Exploratory Data Analysis (EDA)
- **Fuel Usage**:  
  - Avg. departure fuel = ~16,890 L  
  - Avg. arrival fuel = ~8,397 L  
  - Avg. consumption = ~8,493 L (range: 2,570 – 13,280 L)  
- **Flight Durations**: Mostly ~3 hours (range: 1 – 4.17 hrs).  
- **Excessive Departure Fuel (>24,000 L) Leads to Inefficiencies:** High fuel levels show decreased fuel efficiency due to increased flight weight. 

- **Speed and Distance Effects**: The least efficient flights often occur when speed is low or distance is short

- **Duration-Driven Fuel Usage:** Longer flight durations generally lead to higher total fuel consumption.

- **Destination-Specific Patterns:** Certain destinations consistently have higher fuel usage, mainly driven by flight duration and route characteristics.

- **Temporal Patterns:** More flights occur in early January and on weekends, which may influence aggregate fuel consumption patterns.

---

## 3. Investigating Special Cases

- Excessive departure fuel (>24,000 L) reduces efficiency.  
- Mid-distance flights (Dest 1, 2, 7) show unusual fuel use.  
- High-speed flights with elevated fuel per km indicate anomalies.  
- Specific dates/durations (e.g., 2025-01-17) reveal operational inefficiencies.  

## 4. Predictive Modeling

Four regression models were trained to predict fuel consumption:

| Model         | MAE        | MSE           | RMSE       | R² Score | MAPE    |
|---------------|-----------|---------------|------------|----------|---------|
| XGBoost       | 334.41    | 396,057       | 629.33     | 0.897    | 3.59%   |
| Random Forest | 683.18    | 1,675,634     | 1,294.46   | 0.565    | 7.92%   |
| CatBoost      | 469.96    | 547,025       | 739.61     | 0.858    | 5.17%   |
| SVM           | 589.43    | 992,816       | 996.40     | 0.742    | 6.77%   |

🏆 XGBoost was the best-performing model across all evaluation metrics.

---

## 5. Optimum Fuel Value at Departure
- **Finding and Optimum Value**: Using the best performed model in order to find the optimum "Fuel at Departure" value per destination.
- **Evaluating Efficiency of the Optimum Value**: Compare the results with "Fuel Consumption" and actual "Fuel at Departure" values to show the efficiency of the optimum fuel values.  

---

## 6. Business Recommendations
- **Keep fuel at departure under 24,000 liters** to improve fuel efficiency.  
- **Maintain optimal cruising speeds** to reduce fuel consumption per km.  
- **Short flights consume more fuel per km** due to longer takeoff and climb phases.  
- **Low speed combined with short distance** results in the least efficient flights.  
- **Use optimum fuel levels** to reduce costs and unnecessary fuel burn.  
- **Check high-traffic days** (first 5 days of the month, Saturdays) to assess passenger impact.  
- **Use a larger dataset** for more reliable insights across destinations, weather, and passenger volumes.
- 
## 🛠 Tools & Libraries Used

- pandas, NumPy
- matplotlib, seaborn
- scikit-learn
- XGBoost, CatBoost
- RandomForestRegressor
- Support Vector Regression (SVR)
