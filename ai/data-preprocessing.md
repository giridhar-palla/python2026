# 🧹 Data Preprocessing - Complete Guide (Zero to Hero)

> Data preprocessing is **cleaning and preparing raw data** so that ML models can learn from it effectively. Garbage in = garbage out.

---

## 🔹 Why Preprocessing?

### 🧠 Analogy

> 👉 Like **preparing ingredients before cooking**:
> - Wash vegetables (clean data)
> - Chop them to the right size (scale/normalize)
> - Remove rotten parts (handle missing values)
> - Measure ingredients (feature engineering)
>
> You can't cook a great meal with dirty, uncut, unmeasured ingredients.

### 🔸 Real-World Data is Messy

| Problem | Example |
|---------|---------|
| Missing values | Age: 25, ?, 30, ?, 28 |
| Different scales | Age: 25, Salary: 500000 |
| Text categories | Color: "Red", "Blue", "Green" |
| Outliers | Ages: 25, 30, 28, 200 |
| Duplicates | Same row appears twice |
| Inconsistent format | "Male", "male", "M", "m" |

---

## 🔹 The Preprocessing Pipeline

```
Raw Data
  ↓
1. Handle Missing Values
  ↓
2. Handle Duplicates
  ↓
3. Handle Outliers
  ↓
4. Encode Categorical Data
  ↓
5. Feature Scaling
  ↓
6. Feature Selection
  ↓
7. Train-Test Split
  ↓
Clean Data → Ready for ML Model
```

---

## 🔹 1. Handling Missing Values (VERY IMPORTANT 🔥)

### 🔸 Why Do Missing Values Exist?

- Data entry errors
- Sensor failures
- Survey respondents skipping questions
- Data merging issues

### 🔸 Strategies

| Strategy | When to Use | Example |
|----------|------------|---------|
| **Remove rows** | Few missing values, large dataset | Drop rows with any NaN |
| **Remove columns** | Column has >50% missing | Drop the entire column |
| **Fill with mean** | Numerical data, normal distribution | Age: fill with average age |
| **Fill with median** | Numerical data, has outliers | Salary: fill with median |
| **Fill with mode** | Categorical data | City: fill with most common city |
| **Fill with constant** | Domain knowledge | Status: fill with "Unknown" |
| **Forward/Backward fill** | Time series data | Use previous/next value |

### 🔸 Example

```
Original:
Name    Age    Salary
Alice   25     50000
Bob     ?      60000
Charlie 30     ?
Diana   28     55000

Strategy 1 — Remove rows with missing values:
Alice   25     50000
Diana   28     55000

Strategy 2 — Fill with mean:
Bob     27.67  60000    (mean age = (25+30+28)/3)
Charlie 30     55000    (mean salary = (50000+60000+55000)/3)
```

### 🔸 Important Rule

> ⚠️ **Never fill missing values using information from the test set.** Calculate mean/median only from the training set, then apply to both train and test.

---

## 🔹 2. Handling Duplicates

```
Before:
Alice   25   50000
Bob     30   60000
Alice   25   50000   ← duplicate!

After removing duplicates:
Alice   25   50000
Bob     30   60000
```

✔ Always check for and remove duplicates before training.

---

## 🔹 3. Handling Outliers

### 🧠 Analogy

> 👉 Like a class where everyone scored 70-90 on an exam, but one student scored 5. That 5 is an **outlier** that can skew the average.

### 🔸 Detection Methods

| Method | How |
|--------|-----|
| **Visual** | Box plots, scatter plots |
| **IQR Method** | Values below Q1-1.5×IQR or above Q3+1.5×IQR |
| **Z-Score** | Values more than 3 standard deviations from mean |

### 🔸 Handling Strategies

| Strategy | When |
|----------|------|
| Remove | Clearly erroneous data |
| Cap/Floor | Replace with upper/lower bounds |
| Transform | Log transformation to reduce impact |
| Keep | If outliers are genuine and important |

---

## 🔹 4. Encoding Categorical Data (VERY IMPORTANT 🔥)

ML models work with **numbers**, not text. You must convert categories to numbers.

### 🔸 Label Encoding — Assign a Number to Each Category

```
Color: Red, Blue, Green

Label Encoded:
Red   → 0
Blue  → 1
Green → 2
```

⚠️ **Problem:** The model might think Green (2) > Blue (1) > Red (0), which is meaningless for colors.

✔ **Use for ordinal data** (categories with natural order): Low=0, Medium=1, High=2

### 🔸 One-Hot Encoding — Create Binary Columns

```
Color: Red, Blue, Green

One-Hot Encoded:
       Red  Blue  Green
Row 1:  1    0     0
Row 2:  0    1     0
Row 3:  0    0     1
```

✔ **Use for nominal data** (categories with no order): colors, cities, brands

### 🔸 Label vs One-Hot Encoding

| | Label Encoding | One-Hot Encoding |
|---|---|---|
| Output | Single column with numbers | Multiple binary columns |
| Implies order? | ✅ Yes (can be misleading) | ❌ No |
| Use for | Ordinal data (Low/Med/High) | Nominal data (Red/Blue/Green) |
| Columns added | 0 | N-1 (where N = categories) |

### 🔸 The Dummy Variable Trap

When one-hot encoding, you can **drop one column** because it's redundant:

```
If Red=0 and Blue=0, it MUST be Green.

So you only need 2 columns for 3 categories:
       Red  Blue
Row 1:  1    0     (Red)
Row 2:  0    1     (Blue)
Row 3:  0    0     (Green — implied)
```

---

## 🔹 5. Feature Scaling (VERY IMPORTANT 🔥)

### 🧠 Analogy

> 👉 Like converting **different currencies to one currency** before comparing prices. You can't compare $100 with ¥10000 directly — you need to normalize them.

### 🔸 Why Scale?

```
Feature 1: Age → values: 20-60
Feature 2: Salary → values: 30000-200000

Without scaling: Salary dominates because its numbers are much larger.
The model thinks Salary is more important just because of the scale.
```

### 🔸 Normalization (Min-Max Scaling)

Scales values to a range of **0 to 1**.

```
Formula: X_new = (X - X_min) / (X_max - X_min)

Age: [20, 30, 40, 50, 60]
Normalized: [0.0, 0.25, 0.5, 0.75, 1.0]
```

✔ Use when: data doesn't follow a normal distribution, neural networks

### 🔸 Standardization (Z-Score Scaling)

Scales values to have **mean = 0** and **standard deviation = 1**.

```
Formula: X_new = (X - mean) / std_deviation

Age: [20, 30, 40, 50, 60]  (mean=40, std=15.81)
Standardized: [-1.26, -0.63, 0.0, 0.63, 1.26]
```

✔ Use when: data follows a normal distribution, SVM, logistic regression

### 🔸 Normalization vs Standardization

| | Normalization | Standardization |
|---|---|---|
| Range | 0 to 1 | No fixed range (centered at 0) |
| Sensitive to outliers | ✅ Yes | ❌ Less sensitive |
| Use when | Neural networks, KNN | SVM, Logistic Regression |
| Distribution | Any | Normal distribution preferred |

### 🔸 Which Algorithms Need Scaling?

| Needs Scaling ✅ | Doesn't Need Scaling ❌ |
|-----------------|----------------------|
| KNN | Decision Tree |
| SVM | Random Forest |
| Logistic Regression | Naive Bayes |
| Neural Networks | XGBoost |
| Linear Regression | |
| K-Means | |

🧠 **Rule of thumb:** Distance-based and gradient-based algorithms need scaling. Tree-based algorithms don't.

---

## 🔹 6. Feature Selection

### 🧠 Analogy

> 👉 Like choosing the **most relevant subjects** to study for an exam. Studying everything wastes time — focus on what matters.

### 🔸 Why Select Features?

- Remove irrelevant/redundant features
- Reduce overfitting
- Speed up training
- Improve model performance

### 🔸 Methods

| Method | How |
|--------|-----|
| **Correlation analysis** | Remove features highly correlated with each other |
| **Feature importance** | Use Random Forest to rank features |
| **Variance threshold** | Remove features with very low variance (almost constant) |
| **Domain knowledge** | Use your understanding of the problem |

---

## 🔹 7. Train-Test Split

```
Total Data: 1000 samples

Option 1 — Simple split:
├── Training: 800 (80%)
└── Testing: 200 (20%)

Option 2 — With validation:
├── Training: 700 (70%)
├── Validation: 150 (15%)
└── Testing: 150 (15%)
```

### 🔸 Important Rules

- **Shuffle** data before splitting (avoid ordering bias)
- **Stratify** for classification (maintain class proportions in each split)
- **Never** use test data during training or preprocessing
- Split **before** scaling (fit scaler on train, transform both)

---

## 🔹 Common Preprocessing Mistakes ⚠️

### 🔸 Mistake 1: Scaling Before Splitting

```
❌ Wrong: Scale ALL data → then split
   (test data information leaks into training)

✅ Right: Split → Scale training data → Apply same scaler to test data
```

### 🔸 Mistake 2: Filling Missing Values with Test Data Info

```
❌ Wrong: Calculate mean from ALL data → fill missing
✅ Right: Calculate mean from TRAINING data only → fill both
```

### 🔸 Mistake 3: Ignoring Categorical Encoding

```
❌ Wrong: Feed "Red", "Blue", "Green" directly to model
✅ Right: One-hot encode or label encode first
```

### 🔸 Mistake 4: Not Handling Imbalanced Data

```
Dataset: 950 "Not Fraud" + 50 "Fraud"

Techniques:
- Oversampling minority class (SMOTE)
- Undersampling majority class
- Use class weights in the model
- Use F1/Recall instead of accuracy
```

---

## 🔹 Interview Questions 💡

### Q1: Why is data preprocessing important?
**Answer:** Real-world data is messy — missing values, different scales, text categories. Models can't learn effectively from raw data. Preprocessing cleans and transforms data so models can find patterns.

### Q2: What is the difference between normalization and standardization?
**Answer:** Normalization scales data to 0-1 range. Standardization scales to mean=0, std=1. Use normalization for neural networks/KNN, standardization for SVM/logistic regression.

### Q3: Why should you split data before scaling?
**Answer:** To prevent data leakage. If you scale before splitting, information from the test set (its mean, min, max) leaks into the training process, giving misleadingly good results.

### Q4: What is one-hot encoding?
**Answer:** Converting categorical variables into binary columns. Each category gets its own column with 1 or 0. Used for nominal data (no natural order) like colors or cities.

### Q5: How do you handle imbalanced datasets?
**Answer:** Oversampling (SMOTE), undersampling, class weights, or using metrics like F1/Recall instead of accuracy.

---

## 🔹 Complete Summary 📌

| Step | What | Why |
|------|------|-----|
| Missing values | Fill or remove | Models can't handle NaN |
| Duplicates | Remove | Bias toward repeated data |
| Outliers | Remove, cap, or transform | Skew model learning |
| Encoding | Label or One-Hot | Models need numbers |
| Scaling | Normalize or Standardize | Equal feature importance |
| Feature selection | Remove irrelevant features | Reduce noise, speed up |
| Train-test split | Separate data | Evaluate on unseen data |
| Data leakage | Scale AFTER split | Prevent cheating |

---

> 🚀 **Next:** NLP Basics →
