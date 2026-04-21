# 🔮 Unsupervised Learning - Complete Guide (Zero to Hero)

> Unsupervised learning finds **hidden patterns** in data **without labels** — the model discovers structure on its own.

---

## 🔹 What is Unsupervised Learning?

### 🧠 Real-World Analogy

> 👉 Like a **child sorting a box of mixed toys** without any instructions:
> - No one tells them "this is a car, this is a doll"
> - The child naturally groups similar items together
> - Cars with cars, dolls with dolls, blocks with blocks

### 🔸 Supervised vs Unsupervised

| | Supervised | Unsupervised |
|---|---|---|
| Labels? | ✅ Yes (input + answer) | ❌ No (input only) |
| Goal | Predict a known output | Discover hidden patterns |
| Example | "Is this email spam?" | "Group these customers" |
| Analogy | Learning with a teacher | Learning without a teacher |

---

## 🔹 Three Main Tasks

| Task | What It Does | Example |
|------|-------------|---------|
| **Clustering** | Groups similar items together | Customer segmentation |
| **Dimensionality Reduction** | Simplifies data (fewer features) | Compressing 100 features to 10 |
| **Association** | Finds relationships between items | "People who buy X also buy Y" |

---

# 🔵 CLUSTERING

---

## 🔹 What is Clustering?

> 👉 Dividing data into **groups (clusters)** where items in the same group are **similar** and items in different groups are **different**.

---

## 🔹 K-Means Clustering

### 🧠 Analogy

> 👉 Like a **pizza delivery company** deciding where to place **K warehouses** so that each warehouse is closest to its delivery area. The warehouses are the **centroids**, and each delivery zone is a **cluster**.

### 🔸 How It Works (Step by Step)

```
1. Choose K (number of clusters)
2. Randomly place K centroids
3. Assign each point to the nearest centroid
4. Move each centroid to the center of its assigned points
5. Repeat steps 3-4 until centroids stop moving
```

### 🔸 Example

```
Data: Customer spending patterns
K = 3

Result:
Cluster 1: High spenders (luxury shoppers)
Cluster 2: Medium spenders (regular shoppers)
Cluster 3: Low spenders (bargain hunters)
```

### 🔸 Choosing K — The Elbow Method

> 👉 Plot the "error" for different values of K. The point where the curve bends like an **elbow** is the best K.

```
K=1: High error
K=2: Lower error
K=3: Much lower error  ← elbow point
K=4: Slightly lower (not worth the extra cluster)
```

### 🔸 When to Use

- You know (or can estimate) the number of groups
- Data has roughly spherical clusters
- Customer segmentation, image compression

### 🔸 Pros & Cons

| Pros | Cons |
|------|------|
| Simple and fast | Must choose K in advance |
| Scales well to large data | Assumes spherical clusters |
| Easy to understand | Sensitive to initial centroid placement |
| | Sensitive to outliers |

---

## 🔹 Hierarchical Clustering

### 🧠 Analogy

> 👉 Like building a **family tree**. Start with individuals, then group siblings, then families, then extended families — creating a hierarchy from bottom to top.

### 🔸 Two Approaches

| Approach | Direction | How |
|----------|-----------|-----|
| **Agglomerative** (bottom-up) | Start with individual points → merge | Most common |
| **Divisive** (top-down) | Start with one big cluster → split | Less common |

### 🔸 How Agglomerative Works

```
1. Start: each point is its own cluster
2. Find the two closest clusters
3. Merge them into one
4. Repeat until all points are in one cluster
5. Cut the tree (dendrogram) at the desired level
```

### 🔸 Dendrogram

A tree diagram showing the merging process. You "cut" it at a height to get your desired number of clusters.

### 🔸 When to Use

- Don't know the number of clusters in advance
- Want to visualize the hierarchy
- Small to medium datasets

### 🔸 Pros & Cons

| Pros | Cons |
|------|------|
| No need to specify K | Slow on large datasets |
| Produces a dendrogram (visual) | Cannot undo a merge |
| Works with any cluster shape | Sensitive to noise and outliers |

---

## 🔹 DBSCAN (Density-Based Clustering)

### 🧠 Analogy

> 👉 Like finding **crowds in a park**. Dense groups of people = clusters. People standing alone far from any crowd = outliers (noise).

### 🔸 Concept

- Groups points that are **closely packed together**
- Points in low-density regions are marked as **outliers/noise**
- Does NOT require specifying the number of clusters

### 🔸 Key Parameters

| Parameter | Meaning |
|-----------|---------|
| `eps` (epsilon) | Maximum distance between two points to be considered neighbors |
| `min_samples` | Minimum points needed to form a dense region (cluster) |

### 🔸 When to Use

- Clusters have irregular shapes
- Data has outliers/noise
- Don't know the number of clusters

### 🔸 Pros & Cons

| Pros | Cons |
|------|------|
| Finds clusters of any shape | Sensitive to eps and min_samples |
| Detects outliers automatically | Struggles with varying density |
| No need to specify K | Doesn't work well in high dimensions |

---

## 🔹 Clustering Comparison

| Algorithm | Need K? | Cluster Shape | Handles Outliers? | Speed |
|-----------|:-------:|:---:|:---:|:---:|
| K-Means | ✅ Yes | Spherical | ❌ | ⚡ Fast |
| Hierarchical | ❌ No | Any | ❌ | 🐢 Slow |
| DBSCAN | ❌ No | Any | ✅ Yes | ⚡ Medium |

---

# 📉 DIMENSIONALITY REDUCTION

---

## 🔹 What is Dimensionality Reduction?

> 👉 Like **summarizing a 500-page book into a 10-page summary**. You keep the most important information and discard the rest.

### 🔸 Why Reduce Dimensions?

| Problem | Solution |
|---------|----------|
| Too many features (columns) | Reduce to fewer, meaningful ones |
| Visualization (can't plot 100 dimensions) | Reduce to 2D or 3D for plotting |
| Noise in data | Remove irrelevant features |
| Slow training | Fewer features = faster training |
| Curse of dimensionality | More features ≠ better model |

---

## 🔹 PCA (Principal Component Analysis)

### 🧠 Analogy

> 👉 Like taking a **photo of a 3D object from the best angle**. You lose one dimension (3D → 2D photo) but capture the most important information from the best viewpoint.

### 🔸 Concept

- Finds the **directions (components)** where data varies the most
- Projects data onto these directions
- First component captures the most variance, second captures the next most, etc.

### 🔸 Example

```
Original: 50 features (columns)
After PCA: 5 components that capture 95% of the information
Result: 10x fewer features, almost same accuracy
```

### 🔸 When to Use

- Too many features
- Need to visualize high-dimensional data
- Speed up training
- Remove correlated features

### 🔸 Pros & Cons

| Pros | Cons |
|------|------|
| Reduces features effectively | Components are hard to interpret |
| Removes noise | Assumes linear relationships |
| Speeds up training | Information loss |

---

## 🔹 t-SNE (t-Distributed Stochastic Neighbor Embedding)

### 🧠 Analogy

> 👉 Like arranging **people at a party** — people who know each other sit close together, strangers sit far apart. t-SNE does this with data points in 2D.

### 🔸 Concept

- Reduces high-dimensional data to **2D or 3D for visualization**
- Preserves **local structure** (nearby points stay nearby)
- NOT used for feature reduction in models — only for visualization

### 🔸 PCA vs t-SNE

| | PCA | t-SNE |
|---|---|---|
| Purpose | Feature reduction + visualization | Visualization only |
| Speed | Fast | Slow |
| Preserves | Global structure | Local structure |
| Use in models | ✅ Yes | ❌ No (visualization only) |

---

# 🛒 ASSOCIATION RULES

---

## 🔹 What are Association Rules?

> 👉 "People who bought **bread** also bought **butter**." Finding relationships between items in transactions.

### 🔸 Market Basket Analysis

```
Transaction 1: {Bread, Butter, Milk}
Transaction 2: {Bread, Butter}
Transaction 3: {Milk, Eggs}
Transaction 4: {Bread, Butter, Eggs, Milk}

Rule discovered: Bread → Butter (80% of people who buy bread also buy butter)
```

### 🔸 Key Metrics

| Metric | Meaning |
|--------|---------|
| **Support** | How often items appear together |
| **Confidence** | If A is bought, how likely is B? |
| **Lift** | How much more likely A and B together vs independently? |

### 🔸 Real-World Uses

- Product recommendations ("Customers also bought...")
- Store layout optimization
- Cross-selling strategies
- Netflix/YouTube recommendations

---

## 🔹 Interview Questions 💡

### Q1: What is the difference between clustering and classification?
**Answer:** Classification uses labeled data to predict categories (supervised). Clustering groups data without labels based on similarity (unsupervised).

### Q2: How do you choose K in K-Means?
**Answer:** Use the Elbow Method — plot error vs K and pick the "elbow" point where adding more clusters gives diminishing returns.

### Q3: When would you use DBSCAN over K-Means?
**Answer:** When clusters have irregular shapes, when there are outliers in the data, or when you don't know the number of clusters in advance.

### Q4: What is the curse of dimensionality?
**Answer:** As the number of features increases, the data becomes sparse and distances between points become meaningless. Models need exponentially more data to perform well. Dimensionality reduction helps combat this.

### Q5: What is the difference between PCA and t-SNE?
**Answer:** PCA is for feature reduction and visualization (fast, preserves global structure). t-SNE is for visualization only (slow, preserves local structure). Use PCA for model input, t-SNE for exploring data visually.

---

## 🔹 Complete Summary 📌

| Concept | Description |
|---------|-------------|
| Unsupervised Learning | No labels — finds hidden patterns |
| Clustering | Groups similar items |
| K-Means | Partition into K spherical clusters |
| Hierarchical | Bottom-up merging, produces dendrogram |
| DBSCAN | Density-based, finds outliers |
| Elbow Method | Choose K by finding the "bend" |
| Dimensionality Reduction | Fewer features, keep important info |
| PCA | Projects onto directions of max variance |
| t-SNE | 2D visualization preserving local structure |
| Association Rules | "If A then B" relationships |
| Support/Confidence/Lift | Metrics for association strength |

---

> 🚀 **Next:** Reinforcement Learning →
