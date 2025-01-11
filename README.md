# Subscription and Call Fraud Detection System

A functional **fraud detection system** integrated with a **visualization tool** for actionable insights.

## 1. **Data Collection**

**Objective**: Gather relevant data to detect telecom fraud.

### Why This Step Is Critical:
The foundation of the fraud detection system relies on **telecom data**—specifically **Call Detail Records (CDR)**. These records capture the detailed metadata of each call made in a telecom network. By collecting this data, I ensure that the system has access to real-world behavior patterns that can be analyzed for anomalies indicative of fraud.

### Steps:
- **Simulate or Source Anonymized CDRs**: I either source real telecom data from public datasets or simulate synthetic data that mimics telecom behavior using Python’s Faker library. The goal is to test the model with data that mirrors the characteristics of actual telecom activity.

- **Key Fields Collected**:
- `call_duration`: Tracks the length of each call. Short or unusually long calls may indicate fraudulent activity.
- `call_location`, `call_type`, and `call_cost`: These attributes help in identifying fraud patterns, such as frequent international calls that could indicate call forwarding fraud.
- `caller_id`, `receiver_id`, `timestamp`: These identifiers allow for the tracking of suspicious activities over time.

### Data Sources:
- **Kaggle Telecom Datasets**: Real-world datasets from platforms like Kaggle, which contain telecom records that can be used to train the fraud detection model.
- **Synthetic Data**: Where necessary, I generated synthetic data using Python’s Faker library, which simulates fraudulent and non-fraudulent call behavior.

---

## 2. **Data Preprocessing**

**Objective**: Clean and prepare the data for analysis and model building.

### Why This Step Is Critical:
Data preprocessing ensures the integrity of the dataset. Raw telecom data often contains **null values**, **duplicate records**, or **inconsistencies** that would skew model predictions. By cleaning and organizing the data, I improve the reliability and accuracy of the model.

### Steps:
- **Removed Null and Duplicate Records**: Ensuring the data is complete and free of redundancy helps avoid errors during model training and analysis.
- **Aggregated Data to Identify Patterns**: Aggregating by `caller_id` and other relevant attributes enables me to spot irregularities, such as a high frequency of short-duration calls, which is indicative of fraud.

### SQL Query Example:
  - I used the following query to detect suspicious behavior:
    ```sql
          SELECT caller_id, COUNT(*) AS call_count, AVG(call_duration) AS avg_duration
          FROM cdr
          WHERE call_type = 'international'
          GROUP BY caller_id
          HAVING avg_duration < 10;

## 3. **Fraud Detection Model**

**Objective**: Build a machine learning model to classify telecom calls as fraudulent or legitimate.

### Why This Step Is Critical:
With clean and preprocessed data, I built a **fraud detection model** using **Random Forest**. This machine learning algorithm is effective for classification tasks because it handles complex, non-linear relationships well and is resilient to overfitting.

### Steps:
- **Feature Engineering**: I engineered features such as:
  - **call_frequency**: Frequent calls at odd hours can signal fraud.
  - **avg_call_cost**: Unusually high call costs often correlate with fraudulent activity.
  - **call_duration**: Short or very long call durations may indicate fraudulent practices like call forwarding.

- **Model Training**: I trained the **Random Forest** model using labeled data, where the fraud label (fraudulent or not) was known. This helps the model learn from past data to predict new instances of fraud.
  
  ### Python Code Example:
     ```python
          from sklearn.ensemble import RandomForestClassifier
          from sklearn.model_selection import train_test_split
          from sklearn.metrics import accuracy_score
          
          # Prepare data
          X = cdr_data[['call_frequency', 'avg_call_cost', 'call_duration']]
          y = cdr_data['fraudulent']
          
          X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.3)
          
          # Train model
          model = RandomForestClassifier()
          model.fit(X_train, y_train)
          
          # Evaluate
          predictions = model.predict(X_test)
          print("Accuracy:", accuracy_score(y_test, predictions));


## 4. **BI Dashboard**

**Objective**: Visualize trends and key performance indicators (KPIs) for actionable insights.

### Why This Step Is Critical:
Having a model that detects fraud is not enough; it must also be coupled with a **Business Intelligence (BI) Dashboard** that visualizes key metrics. This allows decision-makers to easily monitor trends, detect fraud hotspots, and take prompt action.

### Steps:
- **KPIs to Track**:
  - **Number of Fraudulent Calls Detected**: This helps measure the effectiveness of the fraud detection system.
  - **Fraud Types by Region**: Identifying which regions experience more fraud can help in resource allocation and targeted actions.
  
- **Charts and Visualizations**:
  I used **Tableau** or **Power BI** to build dynamic charts. These dashboards allow stakeholders to view:
  - **Fraud hotspots**: Visualizing geographic areas with a high incidence of fraud.
  - **Trends over time**: Understanding whether fraud activity is increasing or decreasing can inform business decisions.

---

## 5. **Outcome**

**Objective**: Deliver a fully functional fraud detection system that provides actionable insights.

### Why This Step Is Critical:
The ultimate goal was to deliver a **comprehensive fraud detection system** that not only identifies fraud but also helps telecom companies take action based on real-time insights. This system integrates **data science** with **business intelligence** for proactive fraud management.

### Steps:
- **System Integration**: I integrated data collection, preprocessing, fraud detection, and visualization into a cohesive system.
- **Actionable Insights**: The BI dashboard provides stakeholders with the ability to act on fraud trends, making the entire process proactive rather than reactive.

### Final Outcome:
The result is a **fully integrated fraud detection system** that:
- Detects fraudulent telecom calls.
- Provides visual insights into fraud patterns and hotspots.
- Enables telecom companies to make data-driven decisions to reduce fraud and protect revenue.

---

Through this systematic approach, I leveraged my expertise in **Network Assurance** and **Revenue Assurance** to create a powerful tool for detecting fraud and providing actionable insights for telecom operators. The data collected and processed was specifically tailored to telecom operations, ensuring that the system is both relevant and effective in real-world scenarios.

