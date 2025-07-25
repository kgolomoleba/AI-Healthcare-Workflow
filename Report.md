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

