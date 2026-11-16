# Walmart M5 — Retail Demand Planning

Can a four-week moving average or simple exponential smoothing beat a forecast based on the last observed week?

I used Python to compare three methods for forecasting weekly sales for 20 household products at one Walmart store (`CA_1`). The Power BI report shows how accuracy varied over time and across products.

- [View the Power BI report (PDF)](Walmart_M5_Demand_Planning.pdf)
- [Explore the Python notebook](01_data_exploration.ipynb)
- [Data source: M5 Forecasting – Accuracy on Kaggle](https://www.kaggle.com/competitions/m5-forecasting-accuracy/data)

## Forecasting methods

| Method | How it works |
|---|---|
| Naive | Uses sales from the last observed week. |
| MA4 | Averages sales over the last four observed weeks. |
| Simple exponential smoothing (SES) | Updates the estimate using 30% of the latest weekly sales and 70% of the previous estimate. |

Each method produced a forecast at the start of each four-week window and kept it fixed throughout that window. I used four validation windows to select the SES smoothing parameter (α = 0.30), then evaluated all three methods on a separate four-week test period (25 April–22 May 2016).

## Results

Mean absolute error (MAE), in units per product per week. Lower is better.

| Period | Naive | MA4 | SES |
|---|---:|---:|---:|
| Validation | 14.09 | 12.35 | **11.94** |
| Final test | **14.69** | 19.86 | 18.04 |

SES had the lowest validation error, but Naive performed best in the final test. On total sales over the four test weeks, Naive was closer than SES for 11 of the 20 products.

I would use Naive as the benchmark and repeat the comparison across more periods and stores before choosing a method for replenishment.
