# Subscription_and_call_fraud
A functional fraud detection system integrated with a visualization tool for actionable insights.

### Objective

Build a system that detects and prevents telecom fraud, such as subscription fraud, and call forwarding fraud, using Python, SQL, and visualization tools.

Steps

**1. Data Collection**

Simulate or source anonymized telecom Call Detail Records (CDR).

Fields: call_duration, call_location, call_type, call_cost, caller_id, receiver_id, timestamp.

Sample Data Sources:

Kaggle Telecom Datasets

Public datasets from Google Dataset Search

Generate synthetic data using Python’s Faker library.

**2. Data Preprocessing**

SQL Queries:

Remove null or duplicate records.

Aggregate data to identify unusual patterns, e.g., frequent short-duration calls.

Example Query:

SELECT caller_id, COUNT(*) AS call_count, AVG(call_duration) AS avg_duration
FROM cdr
WHERE call_type = 'international'
GROUP BY caller_id
HAVING avg_duration < 10;

**3. Fraud Detection Model**

Use Python and scikit-learn to build a classification model.

Steps:

Feature Engineering: Extract features like call_frequency, avg_call_cost.

Train a Random Forest model for fraud classification.

Example Code:

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
print("Accuracy:", accuracy_score(y_test, predictions))

**4. BI Dashboard**

Use Tableau or Power BI to visualize trends:

KPIs: "Number of Fraudulent Calls Detected", "Fraud Types by Region".

Create charts showing fraud hotspots and trends over time.

**5. Outcome**

A functional fraud detection system integrated with a visualization tool for actionable insights.
