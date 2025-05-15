# ✈️ Fuel Consumption Optimization in Commercial Flights

This project analyzes flight data from January 2025 to identify patterns in fuel consumption and develop predictive models for operational efficiency.

## 📊 Dataset Overview

- Number of Flights: 56
- Time Period: January 2025
- Features: Departure & arrival airports, fuel levels, times, durations, and encoded route IDs

### ✍️ Feature Engineering

- `fuel_consumption`: Calculated as `Fuel at Departure - Fuel at Arrival`
- `flight_duration`: Time difference between arrival and departure in hours
- `destination_id`: Categorical encoding of unique airport pairs
- Additional time-based features: `weekday`, `monthday`, `departure_minutes`, `arrival_minutes`, `flight_duration_minutes`

## 🔍 Key Insights

- Average Fuel at Departure: 16,890 liters  
- Average Fuel at Arrival: 8,397 liters  
- Mean Fuel Consumption: 8,493 liters (Range: 2,570 – 13,280 liters)  
- Mean Flight Duration: 3.33 hours (Range: 1 – 4.17 hours)

## 📈 Observations from Exploratory Data Analysis

- ⛽️ Fuel consumption increases linearly with flight duration—except in outliers caused by excess fuel loads
- ❗ Fuel at Departure > 24,000 liters often results in inefficient usage (e.g., Destinations AYT-DUS, AYT-SAW, AYT-SOF, AYT-MUC)
- 📅 Most flights occurred between January 1st–5th and on Saturdays

## 🤖 Predictive Modeling

Four regression models were trained to predict fuel consumption:

| Model           | MAE     | RMSE    | R² Score | MAPE   |
|----------------|---------|---------|----------|--------|
| XGBoost        | 161.70  | 468.04  | 0.96     | 1.65%  |
| CatBoost       | 387.30  | 706.25  | 0.91     | 6.03%  |
| Random Forest  | 526.55  | 1221.97 | 0.74     | 8.41%  |
| SVM (optimized)| 425.95  | 873.87  | 0.87     | 4.77%  |

🏆 XGBoost was the best-performing model across all evaluation metrics.

## 💡 Business Recommendations

- ✅ Limit fuel at departure to below 24,000 liters to avoid inefficiencies.
- 🔍 Investigate high-traffic days (1st–5th of month, Saturdays) for links between passenger load and fuel usage.
- 📈 Use a larger dataset to improve model generalizability and capture diverse route/weather patterns.

## 🛠 Tools & Libraries Used

- pandas, NumPy
- matplotlib, seaborn
- scikit-learn
- XGBoost, CatBoost
- RandomForestRegressor
- Support Vector Regression (SVR)

---

📌 For questions or contributions, feel free to open an issue or submit a pull request.

