# 📊 Time-Series Demand Forecasting for Store Items 🌟

Hello! 👋 In this project, we aimed to forecast the demand for various products across different stores for the next 3 months. 

This project is based on a Kaggle competition:  
[Demand Forecasting - Kernels Only](https://www.kaggle.com/c/demand-forecasting-kernels-only/data)

---

## 📝 Business Problem

The goal is to predict product demand at the store-item level for the next 3 months. This helps optimize inventory management and minimize stock-outs or overstock situations.

---

## 📂 Dataset Features

The dataset includes transaction data for multiple stores and items over several years.

### 📋 Variables:
- `date`: Date of the transaction.
- `store`: ID of the store.
- `item`: ID of the item.
- `sales`: Number of items sold on the given date.

---

## 🔧 Data Preprocessing Steps

### 📅 Date-Based Features:
Processed the `date` variable and created additional features:
- **Month**, **Day of the Month**, **Day of the Year**  
- **Week Number**, **Day of the Week**  
- **Quarter**, **Is Month Start/End**, **Is Year Start/End**

### 🎯 Feature Engineering:
- **Lag Features**: Incorporated past sales values using lagged variables to identify trends.
- **Rolling Mean Features**: Added rolling averages to smooth data and capture seasonal trends.
- **Exponentially Weighted Features**: Used exponentially weighted averages to emphasize recent data.
- **One-Hot Encoding**: Applied for categorical variables such as store and item.
- **Performed a log transformation** on the target variable, `sales`, to stabilize variance.

### 📉 Data Splitting:
- **Time-Based Validation Sets**: Initially, the training set was defined as data up to the end of 2016, and the validation set was the first 3 months of 2017. This approach ensured that the validation period closely resembled the forecasted period.

---

## ⚙️ Modeling

### 🚀 LightGBM Model:
- Optimized using early stopping and evaluation logging.
- Incorporated a custom cost function for better SMAPE metric performance.
- Tuned hyperparameters to achieve better accuracy.

### ✨ SMAPE Score:
- Validation SMAPE: **13.85**

---

## 🔍 Final Steps and Submissions

- **Final Model**:  
  In the final model, the following process was applied:  
  - The combined dataset of train and test sets had a key difference:  
    The `train` set included `sales` values, while the `test` set had `sales` values as NaN.  
    To address this:  
    ```python
    train = df.loc[~df.sales.isna()]
    x_train = train[cols]
    Y_train = train["sales"]
    
    test = df.loc[df.sales.isna()]
    x_test = test[cols]
    ```

- **Submission File Creation**:  
  After predicting the `sales` values for the test set, these values and their corresponding `id` values were added to the `submissions_df` DataFrame. This DataFrame was then saved as a `.csv` file for submission.

---

## 🔍 Visualizations

### 📈 Plotted annual sales trends and transaction counts for stores and items.
### 🏆 Feature Importance Plot: Highlighted the most impactful features influencing the model.

---

## ✨ Achievements
✅ Successful demand forecasting for store items.  
✅ Implementation of advanced feature engineering techniques.  
✅ Accurate model evaluation using SMAPE as the metric.  
✅ Effective creation and submission of test predictions.
