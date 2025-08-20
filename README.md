# **Customer Acceptance Prediction for Marketing Campaign**

**Author:** Sthefanie Ferreira de S. D. Otaviano  
**Date:** August 20, 2025  
**Project Version:** 1.0  

---

## **1. 📝 Project Overview**

This project utilizes a dataset of customer information to build and evaluate several machine learning models. The primary goal is to predict whether a customer will accept a marketing campaign offer. By identifying the key drivers behind customer acceptance, this analysis aims to provide actionable insights for the marketing team to improve campaign targeting, increase conversion rates, and optimize return on investment (ROI).

---

## **2. 📊 Data Source**

The dataset used in this project is the *Customer Personality Analysis* dataset, publicly available on Kaggle.

- **Link to dataset:** [https://www.kaggle.com/datasets/imakash3011/customer-personality-analysis/data](https://www.kaggle.com/datasets/imakash3011/customer-personality-analysis/data)

The features include:

- **Customer Profile:** Demographics such as age, education, marital status, and income.  
- **Household Information:** Number of children and teenagers.  
- **Customer Relationship:** Date of enrollment and recency of the last purchase.  
- **Spending Habits:** Amount spent on various product categories (e.g., wine, fruit, meat).  
- **Promotional Behavior:** Number of purchases with discounts and acceptance of past campaigns.  
- **Target Variable:** `Response` (1 if the customer accepted the offer in the last campaign, 0 otherwise).  

---

## **3. ⚙️ Project Workflow & Methodology**

The project followed a structured data science workflow:

### **3.1. Data Cleaning & Preprocessing**
- **Initial Inspection:** The dataset was analyzed for data types, statistical properties, and missing values. 24 missing values were identified in the `Income` column.  
- **Handling Irrelevant Columns:** The `ID` column was dropped as it is a non-predictive identifier. The `Z_CostContact` and `Z_Revenue` columns were constant for all rows and were also removed.  

### **3.2. Exploratory Data Analysis (EDA)**
- **Target Variable:** The distribution of the `Response` variable was visualized, revealing a significant class imbalance. This was addressed by using stratified splitting and setting `class_weight='balanced'` in the models.  
- **Feature Distributions:** The distributions of key numerical and categorical features were plotted. A strong right-skew was identified in the `Total_spent` feature.  

### **3.3. Feature Engineering**
Several new features were engineered to capture more meaningful information:  
- `Age`: Calculated from `Year_Birth`.  
- `Customer_Tenure`: Number of years a person has been a customer.  
- `Total_children`: Sum of `Kidhome` and `Teenhome`.  
- `Total_spent`: Total amount spent across all product categories.  
- `Total_purchases`: Total number of purchases made through all channels.  
- `Total_campaigns_accepted`: Sum of acceptances from the 5 previous campaigns.  

A **logarithmic transformation** (`np.log1p`) was applied to the `Total_spent` feature to correct its skewness.  

### **3.4. Modeling & Evaluation**
1. **Preprocessing Pipeline:**  
   - **Numeric Features:** Missing values in `Income` were imputed using the median, and the data was scaled using `StandardScaler`.  
   - **Categorical Features:** One-hot encoding was applied to convert categorical variables into a numerical format.  

2. **Model Comparison:**  
   Three baseline classification models were trained and evaluated using a stratified 80/20 train-test split:  
   - Logistic Regression  
   - Random Forest  
   - XGBoost  

3. **Hyperparameter Tuning:**  
   `GridSearchCV` with 5-fold cross-validation was employed to find the optimal parameters for each model, ensuring robust evaluation.  

---

## **4. 📈 Results & Findings**

### **4.1. Model Performance**
After hyperparameter tuning and cross-validation, the **Random Forest** model emerged as the top performer with the highest and most stable ROC AUC score of **0.878**. XGBoost followed closely, while Logistic Regression also provided strong results.  

| Model               | Best CV ROC AUC |
| :------------------ | :-------------- |
| **Random Forest**   | **0.8779**      |
| XGBoost             | 0.8725          |
| Logistic Regression | 0.8638          |

_**[INSERT YOUR COMPARATIVE ROC CURVE IMAGE HERE]**_

### **4.2. Key Predictive Features & Business Insights**
1. **Past Engagement is the #1 Predictor:**  
   The most important feature was `Total_campaigns_accepted`.  
   - *Actionable Insight:* Prioritize targeting this "golden audience" with exclusive or high-value offers.  

2. **Customer Loyalty and Recency are Crucial:**  
   `Customer_Tenure` and `Recency` were highly influential.  
   - *Actionable Insight:* Focus on customers with recent purchases and develop retention strategies for long-term customers.  

3. **Life Stage and Family Profile Matter:**  
   Features like `Marital_Status` (especially `Single`) and `Total_children` had predictive power.  
   - *Actionable Insight:* Segment campaigns based on household and relationship status.  

---

## **5. 🚀 Setup & Execution**

### **5.1. Repository Structure**

📦 Customer-Personality-Classification
┣ 📜 classification_customer_acceptance.ipynb # Main notebook with all analysis and modeling
┣ 📜 README.md # Project documentation (this file)
┗ 📜 requirements.txt # Project dependencies


### **5.2. Dependencies**
This project requires Python 3 and the libraries listed in `requirements.txt`. You can install them using pip:  
```bash
pip install -r requirements.txt
```

Alternatively, install them manually:
```bash
pip install pandas numpy seaborn matplotlib scikit-learn xgboost
```

### 5.3. Instructions

Clone this repository to your local machine:

```bash
git clone https://github.com/your-username/Customer-Personality-Classification.git
cd Customer-Personality-Classification
```
- Install the required dependencies as mentioned above.
- Ensure the dataset marketing_campaign.csv is in the root directory.
- Open and run the Jupyter Notebook classification_customer_acceptance.ipynb. Run the cells sequentially to replicate the analysis.

### 6. 📬 Contact

Sthefanie Ferreira de S. D. Otaviano [LinkedIn](linkedin.com/in/sthefanie-ferreira-de-s-d-otaviano-976a59206)
