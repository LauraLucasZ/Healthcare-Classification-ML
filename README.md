# Medical Test Results Classification Project

This project focuses on predicting medical test results (`Normal`, `Inconclusive`, `Abnormal`) using a combination of preprocessing techniques, feature engineering, and multiple machine learning models.

---

## 🧹 Data Preprocessing

### 1. Handling Missing, Duplicate, and Garbage Values
- Missing values were imputed using strategies such as mean, mode, or placeholder values like `"Unknown"`.
- Duplicate rows were identified and removed to reduce bias.
- Garbage values (e.g., `null`, `??`, `N/A`) were cleaned or corrected.
- Gender inconsistencies were resolved using gender inference from names.

### 2. Feature Engineering

#### Encoding
- **One-Hot Encoding**: Applied to nominal categorical variables like `Gender`, `Blood Type`, `Medical Condition`, `Insurance Provider`, `Medication`.
- **Frequency Encoding**: Used for high-cardinality features such as `Doctor` and `Hospital`.
- **Label Encoding**: Applied to ordinal features such as `Admission Type` and `Test Results`.

#### Normalization
- Numerical features were scaled using **Min-Max Scaling** to the [0, 1] range.
- Temporal features (`Date of Admission`, `Discharge Date`) were converted to duration and scaled.
- Financial and count-based features (e.g., `Billing Amount`, `Stay Days`) were scaled.

---

## 📈 Exploratory Data Analysis

- **Correlation Heatmaps** were used to identify feature relationships.
- **Distribution Plots** assessed skewness and kurtosis for normalization verification.

---

## 🧪 Dimensionality Reduction: PCA

- **Purpose**: Reduce redundancy, improve training speed, and enhance generalization.
- **Component Selection**: Retained components explaining ~95% variance.
- PCA-transformed data was used across multiple models for fair comparison.

---

## 🤖 Modeling and Results

### 1. Logistic Regression

#### Without PCA
- **Accuracy (Test):** 0.7619  
- **F1 Score (Test):** 0.76  
- **Best Class Performance:** Abnormal (F1 = 0.80)

#### With PCA
- **Accuracy (Test):** 0.7575  
- **F1 Score (Test):** 0.76  
- Slight reduction in dimensionality with similar performance.

---

### 2. Multi-Layer Perceptron (MLP)

#### With PCA
- **Architecture**: Dense layers with LeakyReLU and Dropout.
- **Best Test Accuracy:** 0.8588

#### Without PCA
- **Architecture**: Simpler structure with ReLU activations.
- **Best Test Accuracy:** 0.8653

#### Deep MLP Without PCA
- **Architecture**: Increased depth for higher representational power.
- **Best Test Accuracy:** 0.8756  
- **Insight**: Depth improved model’s ability to learn complex patterns.

---

### 3. Naïve Bayes Classifier

#### Without PCA
- **Test Accuracy:** 0.7418  
- **F1 Score:** 0.79  

#### With PCA
- **Test Accuracy:** 0.7883  
- PCA reduced noise and improved class separability.

---

### 4. Ensemble Modeling (XGBoost)

- **Model Type**: Gradient Boosting with multi-class objective.
- **Test Accuracy:** 0.845  
- **Insight**: Outperformed Naïve Bayes models, confirming the power of ensemble methods.

---

### 5. Support Vector Machines (SVM)

#### Linear Kernel with PCA
- **Baseline Performance**

#### RBF Kernel with PCA and PSO Optimization
- **Test Accuracy:** 0.84  
- **F1 Score:** 0.844  
- **With Optimization (No PCA):**  
  - **Test Accuracy:** 0.85  
  - **F1 Score:** 0.845  
- **Insight**: RBF kernel with PSO tuning yielded the best SVM results.

---

## 📊 Comparative Summary

| Model                      | PCA Used | Test Accuracy |
|---------------------------|----------|----------------|
| Logistic Regression       | No       | 0.7619         |
| Logistic Regression       | Yes      | 0.7575         |
| MLP                       | Yes      | 0.8588         |
| MLP                       | No       | 0.8653         |
| Deep MLP                  | No       | 0.8756         |
| Naïve Bayes               | No       | 0.7418         |
| Naïve Bayes               | Yes      | 0.7883         |
| XGBoost                   | Yes      | 0.845          |
| SVM (RBF, with PCA)       | Yes      | 0.844          |
| SVM (RBF, PSO Optimized)  | No       | 0.85           |

---

## 📌 Insights

- **Normalization** and **encoding** were critical for consistent model input.
- **PCA** helped reduce complexity but wasn’t always beneficial for deep learning models.
- **MLP with increased depth** provided the best overall performance.
- **Ensemble methods (XGBoost)** and **optimized SVMs** performed competitively.
- Feature engineering had a significant impact across all models.

---
