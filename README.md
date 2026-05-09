# Fuel Economy Trends: Predicting Real-World MPG

This repository contains the code, report, and generated figures for a machine learning project analyzing U.S. EPA Automotive Trends data. The project predicts real-world miles per gallon (MPG) from vehicle attributes using baseline, linear regression, and polynomial regression models. It also visualizes how MPG distributions have changed across decades.

## Project Overview

The goal of this project is to model real-world vehicle fuel economy using interpretable machine learning methods. The main task is supervised regression, where the target variable is real-world MPG and the predictors include model year, engine characteristics, vehicle class, transmission type, drive type, make, and fuel type.

The project compares:

- Mean baseline regression
- Linear regression
- Polynomial regression with degrees 2, 3, and 4

The final report is written in a NeurIPS-style LaTeX format and includes the required sections: Abstract, Introduction, Related Work, Methodology, Experiments & Results, Model Improvements, and Conclusion.

## Repository Contents

The repository should contain the following files:

```text
Final_Project.pdf
README.md
Final_Data_Science_Project.ipynb
model_comparison.png
mpg_spread_by_decade.png
residual_plot.png
actual_vs_predicted.png
```

Input files:

```text
neurips_2025.sty
epa_automotive_trends_1975_2024.csv
```

The EPA dataset file does not need to be committed if it is too large or if redistribution is not desired. Instead, users can download it directly from the EPA website.

## Data Source

The dataset comes from the U.S. Environmental Protection Agency Automotive Trends Data Explorer.

Download page:

https://www.epa.gov/automotive-trends/explore-automotive-trends-data

To reproduce the project:

1. Open the EPA Automotive Trends Data Explorer.
2. Export or download the detailed trends data as a CSV or Excel file.
3. Save the file locally.
4. Upload the file when prompted by the Colab notebook.

The notebook is designed to accept either `.csv`, `.xlsx`, or `.xls` files.

## Main Features Used

The pipeline automatically detects and standardizes common EPA column names. The expected feature columns include:

- Model Year
- Engine Cylinders
- Engine Displacement
- Transmission Type
- Vehicle Type
- Drive Type
- Regulatory Class
- Make
- Fuel Type

The target column is:

- Real-World MPG

If the exported dataset uses slightly different column names, the notebook attempts to rename them automatically.

## Preprocessing Steps

The preprocessing pipeline includes:

1. Target filtering  
   Rows with missing real-world MPG values are removed.

2. Numerical conversion  
   Model year, engine cylinders, engine displacement, and MPG are converted to numeric values.

3. Binary feature mapping  
   Two binary variables are created:
   - `Is_Truck_SUV`: equals 1 if the vehicle type or regulatory class indicates truck/SUV.
   - `Is_Manual`: equals 1 if the transmission type indicates manual transmission.

4. Missing value imputation  
   - Numerical columns use median imputation.
   - Categorical columns use constant imputation with the value `"missing"`.

5. Feature scaling  
   Numerical features are standardized using z-score scaling.

6. One-hot encoding  
   Categorical features are one-hot encoded with unknown categories ignored during validation/test evaluation.

7. Polynomial features  
   Polynomial expansion is applied to numerical features for degrees 2, 3, and 4.

## Model Training

The notebook trains and evaluates the following models:

| Model | Description |
|---|---|
| Mean baseline | Predicts the average training MPG |
| Linear regression | Uses preprocessed numerical and categorical features |
| Polynomial degree 2 | Adds quadratic numerical terms |
| Polynomial degree 3 | Adds cubic numerical terms |
| Polynomial degree 4 | Adds fourth-degree numerical terms |

The main model discussed in the report is degree-3 polynomial regression, unless a local run shows a different degree performs best.

## Evaluation Metrics

Models are evaluated using five-fold cross-validation with:

- Mean Squared Error (MSE)
- Mean Absolute Error (MAE)
- Coefficient of Determination (R²)

The final selected model is also evaluated on a held-out 20% test split for diagnostic plots.

## Generated Figures

Running the notebook produces the following figures:

```text
model_comparison.png
mpg_spread_by_decade.png
residual_plot.png
actual_vs_predicted.png
```

These figures are referenced in the LaTeX report and should be uploaded to the same Overleaf folder as the `.tex` file.

### Figure Descriptions

`model_comparison.png`  
Shows cross-validated R² and MAE for the baseline, linear, and polynomial models.

`mpg_spread_by_decade.png`  
Shows boxplots of real-world MPG by decade.

`residual_plot.png`  
Shows residuals versus predicted MPG for the final degree-3 polynomial model.

`actual_vs_predicted.png`  
Shows predicted MPG against actual MPG for the held-out test set.

## How to Run

The easiest way to reproduce the results is with Google Colab.

1. Open `Final_Data_Science_Project.ipynb` in Google Colab.
2. Run all cells.
3. When prompted, upload the EPA Automotive Trends CSV or Excel file.
4. Wait for the model comparison table and figures to generate.
5. Download the generated figures.
6. Upload the figures to Overleaf with the LaTeX report.

## Dependencies

The notebook uses the following Python packages:

```text
pandas
numpy
matplotlib
seaborn
scikit-learn
openpyxl
```

In Google Colab, most of these packages are already installed. If needed, install missing dependencies with:

```python
!pip install pandas numpy matplotlib seaborn scikit-learn openpyxl
```

## Reproducibility Notes

The notebook uses fixed random seeds where applicable:

```python
random_state = 42
```

Cross-validation uses five shuffled folds. Results may vary slightly depending on the exact EPA export, active filters used during export, package versions, and whether preliminary model-year data are included.

## Limitations

The current model is intentionally interpretable and does not include more complex methods such as random forests, gradient boosting, or neural networks. The model also depends on the columns available in the exported EPA file. Important predictors such as vehicle weight, horsepower, hybrid technology flags, or production volume may not be present in every export.

## Future Work

Possible improvements include:

- Ridge or Lasso regularization for polynomial regression
- Random forest or gradient boosting regression
- Segment-specific models for cars, SUVs, trucks, and hybrids
- Additional technology-specific features
- Prediction intervals using quantile regression or conformal prediction
- More detailed feature importance analysis

## Author

Brandon Bui  
Department of Computer Science  
Rutgers University