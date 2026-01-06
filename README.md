# NBA-Win-Predictions-ML-Code
Predicting NBA team season outcomes using advanced stats, with a comparison of Ridge regression, XGBoost, and TPOT across different prediction targets.


[README_Final.txt](https://github.com/user-attachments/files/24460544/README_Final.txt)
NBA Wins & Win Percentage Prediction

This project looks at two related regression problems using NBA team data:

	1.	Predicting total season wins
	2.	Predicting season win percentage

Even though these targets are mathematically related, they behave differently when modeled. Because of that, the best-performing models (and the impact of hyperparameter tuning) ended up being different for each notebook.
⸻

Modeling Overview

Both notebooks follow the same workflow:

	⁃	Data cleaning and feature selection
	⁃	Train / test split by season
	⁃	Baseline regression models
	⁃	Model evaluation using MAE, RMSE, and R²
	⁃	Domain-specific accuracy metrics

Where they differ and which models actually perform best for each.
⸻

Total Wins Prediction
Notebook: NBA_Wins_Prediction.ipynb

Models Used
	⁃	Dummy Regressor (baseline)
	⁃	Ridge Regression
	⁃	XGBoost Regressor
	⁃	XGBoost + RandomizedSearchCV
	⁃	TPOT Regressor

Results & Observations
	⁃	In this case, XGBoost outperformed Ridge.
	⁃	RandomizedSearchCV actually made XGBoost worse, not better.
	⁃	After extensive setup and tuning, TPOT produced the best overall model.

Evaluation Metrics
	⁃	Percentage of predictions within ±3 wins
This threshold was chosen to account for roster turnover between seasons and real-world factors like injuries or mid-season trades, while still being tight enough to reflect meaningful predictive accuracy.

Final Model Ranking (Wins)
	1.	TPOT Regressor
	2.	XGBoost (no RSCV)
	3.	Ridge Regression
⸻


Win Percentage Prediction
Notebook: NBA_WinPct_Prediction.ipynb

Models Used
	⁃	Dummy Regressor (baseline)
	⁃	Ridge Regression
	⁃	XGBoost Regressor
	⁃	XGBoost + RandomizedSearchCV (RSCV)

Results & Observations
	⁃	Ridge Regression outperformed XGBoost, even after hyperparameter tuning.
	⁃	RandomizedSearchCV did improve XGBoost, but not enough to beat Ridge.
	⁃	Because of this, TPOT was intentionally not used in this notebook.

Evaluation Metrics
	⁃	Percentage of predictions within ±0.03 win rate
This threshold represents a small but meaningful difference in season-long performance, roughly equivalent to a 2–3 win swing over an 82-game season.

Final Model Ranking (Win %)
	1.	Ridge Regression
	2.	XGBoost (with RSCV)
	3.	XGBoost (no RSCV)
⸻

TPOT was intentionally only used in the Wins Prediction notebook. In the Win% model, the linear Ridge regressor consistently outperformed XGBoost, even after hyperparameter tuning, which indicated that the relationships were largely linear. So, adding TPOT would have likely increased complexity without improving results.

For the Wins model, however, nonlinear effects mattered more, and TPOT was able to find a pipeline that clearly outperformed both Ridge and XGBoost. Because TPOT is expensive to run and configure, it was only applied where it actually improved performance.

Saved Models

Only the best-performing model from each notebook is saved. So the TPOT model from the Win Prediction book, and the Ridge model from the Win Percentage book. Other models are evaluated inline and kept for comparison rather than persistence.
⸻

Key Takeaways

	⁃	Closely related targets can favor very different models.
	⁃	Hyperparameter tuning does not guarantee better performance.
	⁃	Linear models should not be underestimated.
	⁃	AutoML tools like TPOT are useful when the target contains nonlinear structure that simpler models fail to map to. However, when the signal is largely linear, traditional models can be equally effective or better.
⸻

Tools & Libraries

	⁃	Python
	⁃	pandas, numpy
	⁃	scikit-learn
	⁃	XGBoost
	⁃	TPOT
	⁃	matplotlib
⸻

Possible Next Steps

	⁃	Feature engineering specific to pace or era
	⁃	Create a rolling validation window so training data is limited to the season prior
	⁃	Comparing predictions to betting lines or preseason projections
