### Assignment5
### Visualizing Data Veracity Challenges in Multi-Label Classification  

This notebook explores **data veracity challenges** in **multi-label classification** using the **Yeast gene expression dataset**.  
The focus is on identifying **noisy labels**, **outliers**, and **hard-to-learn samples** through **non-linear dimensionality reduction techniques** — specifically **t-SNE** and **Isomap**.  

---

## Objective  
The goal of this assignment is to visualize and interpret challenges that classifiers face when dealing with complex, high-dimensional biological data.  
By projecting high-dimensional gene expression features into two dimensions, we aim to:  
- Reveal structural relationships between samples  
- Identify data quality issues affecting classifier performance  
- Compare **local** (t-SNE) vs. **global** (Isomap) manifold learning techniques  

---

## Dataset  
**Name:** Yeast Dataset (from [MULAN Repository](http://mulan.sourceforge.net/datasets.html))  
**Features (X):** 103 gene expression features  
**Labels (Y):** 14 binary functional categories  

Each data point corresponds to an experiment, and each gene may belong to multiple functional categories.  

---

## Part A: Preprocessing and Initial Setup (10 points)  

### Steps  
1. **Data Loading:**  
   - Loaded the feature matrix (`X`) and multi-label targets (`Y`) directly from the `.arff` file.  
   - Verified dataset dimensions and inspected sample data.  

2. **Label Simplification:**  
   - Identified:
     - Two most frequent **single-label** classes  
     - The most common **multi-label combination**  
   - Reassigned all remaining samples as **‘Other’** for more interpretable visualization.  

3. **Feature Scaling:**  
   - Standardized features using `StandardScaler`.  
   - Explained importance of scaling for distance-based methods.  
   - Verified scaling correctness through summary statistics.  

---

## Part B: t-SNE and Veracity Inspection (20 points)  

### Implementation  
- Applied **t-SNE** with multiple **perplexity** values to observe changes in local and global structure.  
- Created a grid of scatter plots, each colored using the simplified label categories.  

### Visualization  
- Presented 2D embeddings for each perplexity value.  
- Included a single shared legend and consistent color mapping.  

### Veracity Inspection  
Analyzed the t-SNE plots for:  
- **Noisy/Ambiguous Labels:** Points of overlapping colors or mixed functional identities.  
- **Outliers:** Isolated points or small distant clusters.  
- **Hard-to-Learn Samples:** Regions with heavily mixed label boundaries.  

### Justification  
- Recommended **optimal perplexity = 35** based on balance between local and global separation.  
- Summarized how t-SNE effectively preserves **local clusters** while losing **global geometry**.  

---

## Part C: Isomap and Manifold Learning (20 points)  

### Implementation  
- Introduced **Isomap** and explained its ability to preserve **global manifold structure**.  
- Applied Isomap on the scaled data with the same color coding as t-SNE for direct comparison.  

### Visualization  
- Generated the Isomap 2D embedding and highlighted:
  - Manifold curvature  
  - Inter-cluster distances  
  - Global structure relationships  

### Comparison & Analysis  
| Aspect | t-SNE | Isomap |
|--------|-------|--------|
| Structure Focus | Local | Global |
| Sensitivity to Scale | High | Moderate |
| Strength | Reveals clusters | Captures global manifold |
| Limitation | Distorts large-scale geometry | Misses fine local details |

### Interpretation  
- **t-SNE:** Highlights ambiguous and overlapping clusters → useful for identifying *noisy or hard-to-learn samples*.  
- **Isomap:** Unfolds the manifold → helps understand *global gene expression relationships* affecting classification complexity.  

---

## Key Learnings  

- **t-SNE** is powerful for uncovering *local patterns* and ambiguous clusters.  
- **Isomap** complements it by revealing *global manifold geometry*.  
- Visual inspection enables early detection of *data veracity issues* before model training — an essential step for biological datasets.  

---

## Tools & Libraries  
- `scikit-learn` (t-SNE, Isomap, StandardScaler)  
- `seaborn` & `matplotlib` (visualization)  
- `pandas`, `numpy` (data manipulation)  

---
