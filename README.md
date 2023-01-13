**For more details, please refer to Lit Review_caa130123.pdf**

# Introduction

5 broad categories for outlier detection:
1. Distribution-based
2. Depth-based
3. Distance-based
4. Clustering-based
5. **Density-based** (Top N LocalOutlierFactor (LOF) is in this category)

# Motivation

Existing solution: Sklearn LOF \
Drawback: Have to compute the LOF score for every point. The larger the LOF score, the more likely the point is an anomaly \
TopN LOF prunes points and does not compute the LOF score for all points

# Use Cases
1. Prune anomalous points in preprocessing
2. Anomaly detection
3. Detecting attrition

# Algorithm

## Step 1: Preprocessing
Use BIRCH clustering to get all micro clusters

## Step 2: Compute LOF bound for each micro cluster
Those micro clusters with a very small upper LOF bound will be pruned since the points inside are unlikely to be outliers.

## Step 3: Rank Top-n Local Outliers
For the remaining micro clusters, calculate the LOF scores for all points inside them and sort the points by their LOF scores in descending order.

# Evaluation Metrics

## Number of unpruned candidates vs Max Radius
![Alt text](/lit_review_screenshots/eval_metric1.png) \
Increasing max radius will not significantly increase the number of unpruned candidates. Hence, this will not significantly increase runtime.

## Running time vs max radius
![Alt text](/lit_review_screenshots/eval_metric2.png) \
Increasing max radius will not significantly increase runtime.

## Runtime vs size of data
![Alt text](/lit_review_screenshots/eval_metric3.png) \
Increasing the size of data will not significantly increase runtime.

# Source Codes
Language: Java 

Other parameters: 
1. k for KNN (k)
2. N to indicate how many outliers to return (n)
3. Dimensionality of dataset (d)
4. Domain Range (for BIRCH clustering) (r) \
Defined as the distance between the centre of the data space to the furthest data point
5. Cluster radius (for BIRCH clustering) (c) \
Between 0 and 1 \
Metrics used to calculate distance: L1/L2 norm 

# LOF Score
Defined as the average of the ratios of the density of the neighbours as compared to the density of the focal point. \
The higher the score, the denser the neighbours are as compared to the focal point. Hence, it is more likely for the focal point to be an anomaly.

# Challenges

## High dimensions
Top N LOF cannot handle high dimensions well due to the curse of dimensionality.

### First naive approach
Top N LOF drawback: If you have multiple anomalies close to one another, these anomalies cannot be flagged out well by KNN 

Solution:
1. Calculate the k-nearest neighbor distances
2. Calculate the successive differences between distances
3. Select the knn distance with the maximum difference

### Better approach
Uses an encoder-decoder architecture to reduce the dimensionality space so that anomalies can be more effectively detected in lower dimensions.

### Alternative approach
Uses an encoder-decoder architecture as well as clustering to flag out anomalies instead.

# Global Outlier Factor (GOF) Score
An alternative to using LOF is GOF. 

Approaches:
1. Statistical boxplot
2. Sklearn Isolation Forest \
Uses decision trees to flag anomalies. \
The shorter the path from the root to the leaf containing the anomalies, the more likely those anomalies are indeed anomalies
