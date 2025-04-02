# Walmart-Sales-Forecasting
	Retail forecasting is a complex challenge, especially for a company like Walmart, where sales fluctuate due to seasonality, promotions, and economic factors. This project aimed to predict weekly sales across Walmart stores while accounting for holiday effects, markdowns, and external influences. To achieve this, we tested machine learning models (Linear Regression, Decision Tree, Random Forest, and XGBoost) and time-series forecasting methods like SARIMA to find the best predictive approach.
.
 Linear Regression and Time Series Forecasting
•	Initiated the analysis by engineering lag-based features (Lag_1, Lag_4, Lag_52) to test the hypothesis that historical sales patterns could predict future sales. Lag_52 (sales from the same week in the previous year) showed a strong correlation with current weekly sales (R ≈ 0.93), indicating robust yearly seasonality.
•	Trained a Linear Regression model using only Lag_52, which performed surprisingly well:
o	R² = 0.9753, RMSE = $83,013.91, MAE = $52,103.33
o	RMSE was only 8.06% of average weekly sales
o	Residual analysis revealed signs of heteroscedasticity, suggesting the model wasn’t fully capturing underlying variance
•	To benchmark this result with a traditional time series approach, implemented a SARIMA(1,1,1)(1,1,1,52) model:
o	Parameters selected using ADF stationarity tests, ACF, and PACF plots
o	R² = 0.6426, RMSE = $890,763.33, MAE = $760,840.46
o	RMSE = 19.15% of average weekly sales
o	SARIMA captured trend and yearly seasonality but lacked the flexibility to incorporate external drivers or respond to high-variance weeks
•	The clear performance gap between SARIMA and the simple Lag_52 regression confirmed the value of lag-based modelling, while residual patterns pointed toward the need for richer feature sets and non-linear modelling.
•	Expanded the feature set to include Total_MarkDown, Store_Type, and Store_Size. Used correlation matrices and VIF tests to check for multicollinearity, ultimately removing Store_Size. However, the updated regression model delivered identical results to the Lag_52-only version — validating the dominance of seasonal patterns in sales prediction.

Non – Linear Modelling
•	Implemented a Decision Tree Regressor to model potential non-linear relationships:
o	R² = 0.9752, RMSE = $83,013.91, MAE = $52,103.33
o	Residual plots revealed overfitting around peak sales values
•	Applied a Random Forest Regressor to ensemble predictions across multiple trees:
o	R² = 0.9699, RMSE = $91,685.47, MAE = $53,759.07
o	RMSE = 8.75% of average weekly sales
o	Reduced overfitting and improved stability over single-tree models
•	Tuned and deployed an XGBoost Regressor, which provided the most balanced results:
o	R² = 0.9733, RMSE = $86,382.29, MAE = $53,924.57
o	RMSE = 8.24% of average weekly sales
o	Residuals were tightly centered, randomly distributed, and showed minimal bias

Delivered a comprehensive model comparison framework. Concluded that:
•	Lag-based linear regression performed exceptionally well due to strong annual seasonality
•	SARIMA served as a useful statistical baseline, but lacked the adaptability of modern ML approaches
•	Tree-based models, particularly XGBoost, provided the best mix of accuracy and generalization
![image](https://github.com/user-attachments/assets/ec73dc9b-c344-4989-a9ae-a4cb5fa9f362)
