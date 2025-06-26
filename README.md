# Instagram Fake Account Classification

This project aims to classify Instagram accounts as **fake** or **genuine** using machine learning techniques based on profile-level features. The models used include Random Forest and Decision Tree classifiers. The project provides a complete walkthrough including data analysis, training, and evaluation.

---

## Dataset Overview

The dataset contains the following profile-level features:

- `profile pic`: Indicates if the profile has a picture (0 or 1)
- `nums/length username`: Ratio of numbers to the total length of the username
- `fullname words`: Number of words in the full name
- `nums/length fullname`: Ratio of numbers to total length in full name
- `name==username`: Boolean feature indicating if the name matches the username
- `description length`: Length of the bio or description
- `external URL`: Indicates whether a URL is linked
- `private`: Account privacy status (0 = Public, 1 = Private)
- `#posts`: Number of posts made by the user
- `#followers`: Number of followers
- `#follows`: Number of accounts followed
- `fake`: Label (1 = Fake, 0 = Genuine)

Total rows: **576**, with no missing values.

---

## Exploratory Data Analysis (EDA)

### First 5 Rows of the Dataset

The first few records help us understand the structure and values present. For example, a typical row looks like:

```
profile pic: 1
nums/length username: 0.27
fullname words: 0
#followers: 1000
#follows: 955
fake: 0
```

### Dataset Info

All 576 rows are fully populated with integer and float values. There are no null entries, which means no imputation was necessary.

### Descriptive Statistics

We calculated the min, max, mean, and standard deviation for each feature. Notable observations:

- `#followers` ranged from 0 to 15 million, showing a wide variance.
- `#posts` ranged from 0 to 7389.
- `profile pic`, `private`, `external URL` are binary.
- Some accounts have 0 values for `description length`, `external URL`, and `fullname words`.

### Null Values Check

Output showed 0 missing values across all columns — no cleaning required.

### Class Balance

A bar chart was used to visualize the count of fake vs genuine accounts. The distribution appears reasonably balanced for binary classification.

### Correlation Matrix

A heatmap visualized correlations between all numeric features. This helps in understanding which features might be redundant or strongly related to the target `fake`.

---

## Model Training and Evaluation

### Random Forest Classifier

We trained a Random Forest model with 100 trees. 

#### Validation Performance:

- **Accuracy**: 91%
- **Classification Report**:
  - Precision for fake accounts: 0.94
  - Recall for fake accounts: 0.87
- **Confusion Matrix**:

```
[[60  3]   <- Genuine (Predicted vs Actual)
 [ 7 46]]  <- Fake
```

#### Test Performance:

- **Accuracy**: 92.5%
- **Classification Report**:
  - Fake precision and recall both ~0.93
- **Confusion Matrix**:

```
[[56  4]
 [ 5 55]]
```

This shows the model generalizes well to unseen data.

---

### Decision Tree Classifier

We trained a standard Decision Tree without hyperparameter tuning.

#### Validation Performance:

- **Accuracy**: 87%
- **Classification Report**:
  - Precision for fake accounts: 0.88
  - Recall for fake accounts: 0.83
- **Confusion Matrix**:

```
[[57  6]
 [ 9 44]]
```

Though performance is slightly lower than Random Forest, it's interpretable and easier to visualize.

---

## Feature Importance

We used both models to extract and visualize the importance of each feature.

Typical top features included:

- `#followers`
- `#follows`
- `profile pic`
- `description length`
- `external URL`

These features had the highest influence in classifying accounts as fake or genuine.

---

## Decision Tree Visualization

A visual tree (depth limited to 4) was generated showing decision paths. This allows us to interpret how the tree splits based on top features like `#followers` and `profile pic`.

---

## Conclusion

- **Random Forest** gives higher accuracy and better generalization.
- **Decision Tree** offers interpretability.
- Features like followers count, description, and presence of a profile pic are key indicators.
- The dataset is clean, binary-balanced, and suitable for traditional classifiers.

---

## Future Work

- Apply hyperparameter tuning (e.g., GridSearchCV)
- Experiment with ensemble models like XGBoost
- Add NLP-based features from bio text using embeddings
- Develop an API for real-time prediction

---



