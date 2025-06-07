
# Wine Dataset Clustering Analysis

**Author:** Nischal Joshi
**Course:** MSCS 634 Advanced Data Mining and Big Data
**Assignment:** Clustering Analysis Using K-Means and K-Medoids Algorithms

## Purpose
The purpose of this lab is explore the clustering algorithms in the wine data set provided by the sckit-learn. The main objective is to 
* Implement K-Means and K-Mediods clustering algorithm.
* Compare and Contrast the two algorithms. 
* Assess the performanceusing Silhoutter score and Adjusted Rand Index. 
* Determine the right critea to apply various clustering techniques according to the characterstics of data and performance measure.

### Libraries Used
* `sklearn`: Dataset loading, preprocessing, K-Means, and metrics
* `numpy`: Numerical computations and array operations
* `pandas`: Data manipulation and exploration
* `matplotlib/seaborn`: Visualization and plotting
* `pyclustering`: K-Medoids implementation (with custom fallback)

## Details of dataset used 
The dataset includes: 
**178 samples** across: 3 different wine classes
* **13 chemical features**: alcohol, malic acid, ash, alcalinity of ash, magnesium, total phenols, flavanoids, nonflavanoid phenols, proanthocyanins, color intensity, hue, OD280/OD315 of diluted wines, proline
* **3 classes** representing different wine cultivars:
  * Class 0: 59 samples
  * Class 1: 71 samples
  * Class 2: 48 samples

### Data Preprocessing
**Standardization**: In this lab I applied  z-score normalization ensuring that all the features contribute equally to clustering
**Dimensionality Reduction**: Used PCA for 2D visualization while preserving cluster structure

### Evaluation Metrics

* **Silhouette Score**: The Silhouette score shows  how well-defined clusters are (range: -1 to 1, higher is better)
* **Adjusted Rand Index (ARI)**: ARI Compares clustering results with true wine classes (range: -1 to 1, higher is better)

### Performance Results
   **K-Means Silhouette Score**: 0.2849
   **K-Medoids Silhouette Score**: 0.2676

   **K-Means ARI**: 0.8975
   **K-Medoids ARI**: 0.7411


### Clustering and Analysis Comparison: 
  Depending upon the Silhouette Score and Adjusted Rand Index (ARI), K-Means provided slightly better and accurate clusters than K-Medoids:
  The higher Silhouette Score shows that K-means clusters are better separated. 
  The higher ARI shows that clusters in K-Means align more closely with the true wine class label.

### Differences in cluster shapes or positioning
 As expected, the K-Means algorithm creates tighter and more regularly shaped clusters since it is optimizing for variance minimization around centroids.
 K-Medoids, on the other hand, form slightly less regular clusters because it choose actual data points as medoids, which can lead to more natural but slightly less centered clustering.
 For PCA scatter plots, both algorithms identify similar clusters, but K-Means centroids are centrally located, while K-Medoids medoids are off-center in certain regions, affecting overall performance.

### K-Means is better when:
 The data is well-scaled, spherical, and contains few outliers.
 A faster computation and higher performance on large data is required.
 Cluster centers as averages (means) are meaningful.


# K-Medoids is better when:
 The dataset contains a lot of outliers or noise, since medoids are actual points and are less affected by them.
 An interpretable cluster centers that relate to real data points is required.
 The distance measure is non-Euclidean, or the mean is not meaningful e.g., for categorical data

### Challenges Faced and Solutions Implemented

### Technical Challenges

1. **K-Medoids Implementation**:
    * **Challenge**: The pyclustering library's default C++ core (ccore=True) caused installation or runtime issues on macOS with M1 chips due to architecture incompatibility and compiler dependencies.
    * **Solution**: Setting up the ccore=False in the kmedoids function to force use of the pure Python implementation helped in avoiding compilation issues and ensuring compatibility on macOS.

2. **Visualization Complexity**:
   * **Challenge**: Visualizing 13-dimensional data meaningfully was very challenging
   * **Solution**: Implemented PCA to reduce the dimensionalitywhile preserving cluster structure

