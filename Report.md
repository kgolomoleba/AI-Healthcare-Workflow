# Part 1: Short Answer Questions

## 1. Problem Definition

### Hypothetical AI Problem:  
**Predicting Student Dropout Rates in Universities**

### Objectives:  
1. Identify students at high risk of dropping out early in their academic journey.  
2. Provide actionable insights to academic advisors for timely intervention.  
3. Reduce overall dropout rates by 15% within two academic years.

### Stakeholders:  
- University administration (decision-makers for student support policies)  
- Academic advisors and counselors (who will act on model insights)

### Key Performance Indicator (KPI):  
- **Dropout Prediction Accuracy** — percentage of correctly identified at-risk students before dropout occurs.

---

## 2. Data Collection & Preprocessing

### Data Sources:  
1. Student academic records (grades, course completions, attendance)  
2. Student demographic data (age, gender, socioeconomic background)

### Potential Bias:  
- **Socioeconomic bias**: The dataset may underrepresent students from lower-income backgrounds, leading to unfair predictions that overlook specific challenges faced by these groups.

### Preprocessing Steps:  
1. **Handling Missing Data**: Impute missing grades or attendance records using median or mode based on similar students.  
2. **Normalization**: Scale continuous variables like grades to a 0-1 range to ensure uniformity across features.  
3. **Encoding Categorical Variables**: Convert categorical data like gender or major into numerical values using one-hot encoding.

---

## 3. Model Development

### Model Choice:  
**Random Forest Classifier** — chosen because it handles mixed data types well, is robust to overfitting, and provides feature importance for interpretability.

### Data Splitting:  
- **Training Set**: 70% of data to train the model  
- **Validation Set**: 15% for hyperparameter tuning  
- **Test Set**: 15% to evaluate final model performance on unseen data

### Hyperparameters to Tune:  
1. **Number of Trees (n_estimators)** — affects the model’s ability to generalize; too few leads to underfitting, too many increases computation.  
2. **Maximum Depth of Trees (max_depth)** — controls complexity; deeper trees may overfit, shallower trees might underfit.

---

## 4. Evaluation & Deployment

### Evaluation Metrics:  
- **Accuracy**: Measures overall correctness of predictions; useful but can be misleading if classes are imbalanced.  
- **F1-Score**: Harmonic mean of precision and recall, critical for imbalanced classes where false negatives (missing at-risk students) are costly.

### Concept Drift:  
Concept drift occurs when the statistical properties of input data change over time, causing model performance degradation. For example, changes in university policies or student behavior might affect dropout patterns.

**Monitoring:**  
- Periodic model re-evaluation with recent data  
- Automated alerts triggered when performance metrics drop below thresholds

### Technical Deployment Challenge:  
**Scalability** — Ensuring the model can process large volumes of student data in near real-time during enrollment periods without performance bottlenecks.

---
# Part 2: Case Study Application — Predicting Patient Readmission Risk

## Problem Scope (5 points)

### Problem Definition:  
Predict whether a patient discharged from the hospital will be readmitted within 30 days, enabling early intervention to reduce avoidable readmissions.

### Objectives:  
1. Accurately identify patients at high risk of readmission within 30 days.  
2. Support healthcare providers with actionable insights for personalized care plans.  
3. Reduce hospital readmission rates by at least 10% within one year.

### Stakeholders:  
- Patients (whose care outcomes depend on accurate risk prediction)  
- Healthcare providers and hospital administration (decision-makers in patient care and resource allocation)

---

## Data Strategy (10 points)

### Proposed Data Sources:  
1. **Electronic Health Records (EHRs):** Patient medical history, diagnosis codes, treatment details, previous admissions.  
2. **Demographic Data:** Age, gender, socioeconomic status, lifestyle factors (smoking, alcohol use).  

### Ethical Concerns:  
1. **Patient Privacy and Confidentiality:** Handling sensitive health data requires strict compliance with laws like HIPAA to protect patient identity and prevent unauthorized access.  
2. **Bias and Fairness:** Data may underrepresent certain demographic groups, risking unequal prediction accuracy and potential healthcare disparities.

### Preprocessing Pipeline:  
- **Data Cleaning:** Remove duplicates, handle missing values (imputation with median or domain-informed defaults).  
- **Feature Engineering:**  
  - Extract comorbidity scores from diagnosis codes (e.g., Charlson Comorbidity Index).  
  - Calculate time since last admission.  
  - Derive medication adherence indicators.  
- **Encoding:** Convert categorical variables (e.g., diagnosis types) using one-hot encoding.  
- **Normalization:** Scale numeric features like age and lab results.  
- **Train-Test Split:** Stratify by readmission outcome to maintain class balance.

---

## Model Development (10 points)

### Model Selection and Justification:  
**Gradient Boosting Machine (e.g., XGBoost)** is chosen for its strong predictive performance on tabular medical data, ability to handle missing values, and interpretability through feature importance.

### Confusion Matrix (Hypothetical):

|                   | Predicted Readmit | Predicted No Readmit |
|-------------------|-------------------|---------------------|
| **Actual Readmit** | 85 (True Positive) | 15 (False Negative)  |
| **Actual No Readmit** | 20 (False Positive) | 180 (True Negative) |

### Precision and Recall:  
- Precision = TP / (TP + FP) = 85 / (85 + 20) = 0.81  
- Recall = TP / (TP + FN) = 85 / (85 + 15) = 0.85  

These metrics balance identifying true readmissions while minimizing false alarms.

---

## Deployment (10 points)

### Integration Steps:  
1. **Model Packaging:** Convert the trained model into a deployable format (e.g., REST API using Flask or FastAPI).  
2. **System Integration:** Connect the API with hospital EHR systems for real-time risk scoring.  
3. **User Interface:** Develop dashboards for clinicians displaying patient risk scores and recommended actions.  
4. **Testing and Validation:** Perform integration and user acceptance testing with clinical staff.  
5. **Monitoring:** Implement logging and alerts to track model performance and data drift.

### Ensuring Healthcare Compliance (e.g., HIPAA):  
- Enforce data encryption both at rest and in transit.  
- Use role-based access control limiting data access to authorized personnel.  
- Maintain detailed audit logs of data usage and model predictions.  
- Conduct regular compliance audits and update privacy policies as required.

---

## Optimization (5 points)

### Method to Address Overfitting:  
**Early Stopping:** Monitor validation loss during training and halt training once the loss stops improving to prevent the model from overfitting on training data. Additionally, tune regularization parameters (e.g., L1/L2 penalties) and use cross-validation to ensure generalizability.

---
# Part 3: Critical Thinking

## Ethics & Bias (10 points)

### Impact of Biased Training Data on Patient Outcomes  
Biased training data can lead to unfair or inaccurate predictions for certain patient groups. For example, if minority populations or certain age groups are underrepresented, the model may perform poorly for these patients, leading to misclassification of their readmission risk. This can result in inadequate care plans or missed interventions, exacerbating healthcare disparities and negatively impacting patient outcomes.

### Strategy to Mitigate Bias  
One effective strategy is **data augmentation and re-sampling** to balance the dataset by oversampling underrepresented groups or applying synthetic data generation techniques (e.g., SMOTE). Additionally, incorporating fairness-aware algorithms and using fairness metrics during model evaluation can help detect and correct biases before deployment.

---

## Trade-offs (10 points)

### Model Interpretability vs Accuracy in Healthcare  
There is often a trade-off between choosing highly accurate but complex "black-box" models (like deep neural networks or ensemble methods) and simpler, more interpretable models (like logistic regression or decision trees). In healthcare, interpretability is critical for clinician trust and regulatory compliance, as practitioners need to understand model decisions to ensure patient safety. However, sacrificing some accuracy for explainability might reduce predictive performance. Striking a balance is essential, often favoring models that provide explanations alongside reasonable accuracy.

### Impact of Limited Computational Resources on Model Choice  
Hospitals with limited computational infrastructure may need to prioritize lightweight models that require less processing power and memory. This constraint could limit the use of computationally expensive models like deep learning. Instead, simpler algorithms such as logistic regression, decision trees, or small ensemble methods may be preferred for their efficiency and faster inference times, enabling real-time predictions without heavy hardware demands.

---
