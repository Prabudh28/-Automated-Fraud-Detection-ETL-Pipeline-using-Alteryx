# Automated Fraud Detection ETL Pipeline in Alteryx

This project demonstrates the use of Alteryx Designer to build an automated ETL (Extract, Transform, Load) and data preparation pipeline for a machine learning task. The workflow ingests raw credit card transaction data, cleans it, performs feature engineering, and resolves severe class imbalance to create a model-ready dataset.

## Project Objective

The primary goal was to prepare the Kaggle Credit Card Fraud dataset for a predictive model. The raw dataset contains over 284,000 transactions but is highly imbalanced, with fraudulent transactions (Class '1') accounting for less than 0.2% of the data. This pipeline automates the entire pre-processing stage.

## Alteryx Workflow

Here is a snapshot of the final, automated workflow:

![Alteryx Workflow](https://github.com/Prabudh28/-Automated-Fraud-Detection-ETL-Pipeline-using-Alteryx/blob/4a2f4fd07fd1eb11e73c7d31358bc4f2a6b78fbb/The%20How.png)  <-- *REPLACE THIS WITH YOUR IMAGE FILE NAME*

### Key Workflow Steps:

1.  **Extract & Clean**: Ingests the `creditcard.csv` file and uses the **Data Cleansing** tool to remove whitespace, ensuring data quality.
2.  **Feature Selection**: The `Time` column is removed using a **Select** tool as it is not a useful predictor.
3.  **Feature Engineering (Normalization)**:
    * The `Amount` field has a wide distribution, which can skew ML models.
    * A **Summarize** tool finds the Min and Max transaction amounts.
    * An **Append Fields** tool joins these Min/Max values back to every row.
    * A **Formula** tool then creates a new `Normalized_Amount` column using the formula: `(Amount - Min) / (Max - Min)`.
4.  **Predictive Preparation (Oversampling)**:
    * The **Oversample Field** tool is used to correct the severe class imbalance.
    * It is configured to oversample the rare value **'1'** (fraud) until it constitutes **50%** of the final dataset.

## Final Result: A Balanced Dataset

The key outcome is a clean, feature-engineered dataset that is perfectly balanced, eliminating the primary challenge for any fraud detection model.

**Before Oversampling (Imbalanced):**
*Class '0': ~99.8%*
*Class '1': ~0.17%*

**After Oversampling (Balanced):**
![Balanced Class Result](balanced_class_screenshot.png)  <-- *REPLACE THIS WITH YOUR IMAGE FILE NAME*

## Skills Demonstrated

* **ETL Pipeline Development**: Building an end-to-end, repeatable workflow.
* **Data Cleansing & Transformation**: Using tools like Data Cleansing, Select, and Formula.
* **Feature Engineering**: Creating a new, normalized feature to improve model performance.
* **Predictive Data Preparation**: Using the **Oversample Field** tool to solve class imbalance, a critical step in fraud analytics.
* **Workflow Automation**: Creating a single-click process to replace complex manual data preparation.
