# Housing Prices Data Science Portfolio Piece

# California Housing Price Prediction with Confidence Intervals

This project builds several machine learning models to predict **median house values** in California using neighborhood features from the California Housing dataset.  
It also trains **quantile regression models** to produce **prediction intervals**, allowing the uncertainty and risk of predictions to be evaluated.

The project demonstrates data handling, model training, model comparison, uncertainty quantification, and clear visualization of results.

---

## Project Goals

- Predict median house values using neighborhood-level features  
- Compare three regression models: Linear Regression, Random Forest, and LightGBM  
- Quantify model accuracy with RMSE and R²  
- Build **80% confidence intervals** using quantile regression  
- Measure **calibration** (how often intervals contain the true value)  
- Visualize model predictions and uncertainty distributions  

---

## Models Used

| Model | Purpose | Notes |
|-------|---------|-------|
| **Linear Regression** | Baseline model | Limited by linear assumptions |
| **Random Forest Regressor** | Nonlinear ensemble | Strong improvement |
| **LightGBM Quantile Regression** | Median + interval prediction | Best overall performance |

Three LightGBM models were trained for quantiles:

- 10th percentile (lower bound)  
- 50th percentile (median prediction)  
- 90th percentile (upper bound)  

Together, these form an **80% prediction interval** for each data entry.

---

## Dataset

The project uses the **California Housing Dataset** from the 1990 California census, containing:

- Median income  
- House age  
- Average rooms and bedrooms  
- Population
- Average number of occupants
- Latitude
- Longitude 
- Median house value (target)

The target variable is scaled in units of **$100,000**.

---

## Train/Test Split

The dataset is divided into:

- **80% training data**  
- **20% testing data**

A fixed random seed ensures reproducibility.  
This prevents the model from simply memorizing the dataset.

---

## Model Performance

| Model | RMSE (≈ USD error) | R² |
|--------|---------------------|-----|
| Linear Regression | ~$75,000 | 0.58 |
| Random Forest | ~$51,000 | 0.81 |
| **LightGBM (median)** | **~$47,000** | **0.83** |

The LightGBM model performs best in both RMSE and R².

---

## Uncertainty & Calibration

Using quantile regression, the model produces **80% prediction intervals**.

**Calibration Result:**  
The true median house value fell inside the interval **69%** of the time  
(vs. 80% expected).

Interpretation:

- The model is **slightly overconfident**  
- Intervals are somewhat too narrow  
- Increasing interval width or adjusting quantile spread could improve calibration

**Mean interval radius:** ~$39,587

**Example predictions:**

- Predicted median house value: $335,228 ± $90,757
- Predicted median house value: $243,915 ± $32,654
- Predicted median house value: $134,088 ± $19,922
- Predicted median house value: $349,831 ± $95,364
- Predicted median house value: $257,324 ± $28,484

---

## Visualizations

The notebook includes the following plots:

### Predicted vs. Actual Scatter Plots
- Linear Regression  
- Random Forest  
- LightGBM Median Prediction  

### Quantile Scatter Plot (10%, 50%, 90%)
Shows lower, median, and upper predictions for each sample.

### Interval Scatter Plot (with Error Bars)
Visualizes uncertainty size for each individual prediction.

### Histogram of Confidence Interval Radii
Shows that:
- Most intervals are small (tight uncertainty)
- A long tail exists for harder-to-predict homes

---

## Interpretation of Results

### Linear Regression
- RMSE ≈ $75k, R² = 0.58  
- Overpredicts low-value homes, underpredicts high-value homes  
- Strong vertical line at $500k reflects dataset cap  
- Least accurate of the three models  

### Random Forest
- RMSE ≈ $51k, R² = 0.81  
- Much closer fit to the true values  
- Handles nonlinearities well  
- More reliable across the price range  

### LightGBM Quantile Regression
- RMSE ≈ $47k, R² = 0.83  
- Best model for this task  
- Provides usable uncertainty intervals  

### Confidence Intervals
- Most intervals are narrow  
- A small number of very wide intervals  
- Histogram shows a peak near ~$30k with a long right tail past ~$150k  
- Calibration rate (69%) < expected (80%), indicating intervals are too tight  

---

## What I Learned

- Comparing linear and nonlinear regression models  
- How to use **LightGBM** for quantile regression  
- How to compute **prediction intervals** using quantile loss 
- How to evaluate interval calibration  
- How to visualize uncertainty and interpret model risk  

---

## Running the Code

Dependencies:

- Python 3  
- NumPy  
- Pandas  
- scikit-learn  
- LightGBM  
- Matplotlib  

Run locally:

- python housing_prices.py

Or open the notebook in Google Colab.

---

## Files

- `housing_prices.py` – Full analysis, models, and visualizations  
- Optional: Jupyter notebook version  

---

## Conclusion

This project demonstrates a full machine learning workflow with:

- Data preprocessing  
- Multiple regression models  
- Quantile-based uncertainty estimation  
- Calibration testing  
- Clear visualizations  
- Practical interpretation  

It serves as a strong portfolio piece for data science and machine learning internships.
