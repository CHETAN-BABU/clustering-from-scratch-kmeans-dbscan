# Clustering from Scratch: Prototype (K-Means-style) vs DBSCAN

Implements two clustering algorithms **using only NumPy** (no scikit-learn) and compares them on synthetic datasets built to show where each one works and where it breaks.

**Tools:** Python · NumPy · matplotlib

## Implemented from scratch
- **Online prototype-adjustment clustering:** deterministic farthest-point initialisation, learning-rate (α) centroid updates, SSE tracking over epochs and centroid trajectory plots
- **DBSCAN:** region queries, cluster expansion, noise labelling, with ε chosen from the **4-NN distance curve**
- **Silhouette score:** hand-written, excluding noise points
- Learning-rate study with α ∈ {0.01, 0.05, 0.2}

## Datasets
- **A:** three well-separated Gaussian clusters (120 points)
- **B:** a noisy **ring** around a dense **blob**, plus uniform noise (120 points)

## Results
| Dataset | Algorithm | Clusters | Noise | Final SSE | Silhouette |
|---|---|---|---|---|---|
| A | Prototype | 3 | 0 | 213.35 | 0.808 |
| A | DBSCAN | 3 | 2 | – | **0.814** |
| B | Prototype | 2 | 0 | 1292.76 | **0.514** |
| B | DBSCAN | 1 | 15 | – | 0.000 |

On compact Gaussian clusters both methods do well. On ring + blob data a single global ε can't handle both densities, so DBSCAN merges everything. This is a useful lesson in how sensitive DBSCAN is to its parameters.

## Run it
```bash
pip install numpy matplotlib jupyter
jupyter notebook clustering_from_scratch.ipynb
```
The random seed is derived from a student ID, as the assignment specified, so results are reproducible.

---
*MSc Data Science & Analytics, Munster Technological University (Applied Machine Learning)*
