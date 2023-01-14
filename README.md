# Summary
**Refer to Results on open-source datasets pdf file for more details** 

## Experiment 1: Comparing run time between Sklearn and Top N LOF
| Number of dimensions | Top N LOF (in seconds) with c = 2, d = 2/10/20, k = 2, n = 90000, r = 2 | Top N LOF (in seconds) with c = 1, d = 2/10/20, k = 20, n = 90000, r = 1 | Sklearn LOF (in seconds) |
| :---:   | :---: | :---: | :---: |
| 2 | 2   | 4   | 0.4 |
| 10 | 180   | 1914   | 36.9 |
| 20 | 492   | 2909   | 104.8 |

Training time in Top N LOF is longer, which is expected since the tree in BIRCH clustering is built for nothing.  

## Experiment 2: What if anomalies are introduced?
| Number of dimensions | Top N LOF (in seconds)  | Sklearn LOF (in seconds) |
| :---:   | :---: | :---: |
| 2 | 8   | 0.4  |
| 10 | 184   | 38.3 |
| 20 | 251   | 107.2 |

It seems that with anomalies, Top N LOF will take a shorter time. However, no clusters/points are pruned.

## Experiment 3: Increasing the dataset size to 500,000 rows with no anomalies
| Number of dimensions | Top N LOF (in seconds) with c = 2, d = 2/10/20, k = 2, n = 10, r = 2  | Sklearn LOF (in seconds) |
| :---:   | :---: | :---: |
| 2 | 8   | 2.8  |
| 10 | > 28800 (8 hours)   | 898.7 |
| 20 | > 28800 (8 hours)   | 3071.7 |

The results are similar to experiment 1, where top n lof still took longer than sklearn LOF.

## Experiment 4: Comparing F1 score for outlier class
| Number of dimensions | Top N LOF  | Sklearn |
| :---:   | :---: | :---: |
| 2 | 42.2%   | 33.3%  |
| 10 | 46.7%   | 35.6% |
| 20 | 47.8%   | 38.9% |

Sklearn has a lower f1 score, but this is only because k = 30 will give a better performance.

## Experiment 5: How does the parameter n affect Top N LOF’s performance?
| Value of N | F1 Score (Top N LOF)  | F1 Score (Sklearn) |
| :---:   | :---: | :---: |
| 9 | 88.9%   | 88.9%  |
| 90 | 47.8%   | 40% |
| 900 | 28.3%   | 24.8% |

As n increases, f1 score decreases. This is probably due to the fact that outliers are nearer to one another and less likely to be outliers since the data space remains largely unchanged.

## Experiment 6: Quick fix to be able to prune clusters
| Dimensions | Top N LOF (in seconds) with c = 1, d = 2/10/20, k = 2, n = 10, r = 1  | Sklearn (in seconds) |
| :---:   | :---: | :---: |
| 2 | 2   | 0.4  |
| 10 | 1427   | 38.9 |
| 20 | 2449   | 104.7 |

Runtime is still longer. This is probably due to the usage of for loops in the Java codes.

## Experiment 7: Calculating R and tuning C
| Dimensions | Top N LOF (in seconds)  | Sklearn LOF (in seconds) |
| :---:   | :---: | :---: |
| 2 | 5.8   | 0.4  |
| 10 | 514.1   | 39 |
| 20 | 1042.6   | 101.7 |

Runtime is longer, which is expected since there is excessive overhead computation (i.e. BIRCH clustering).

## Experiment 8: Comparing f1 score for outlier class
### Local Outliers
| Dimensions | Top N LOF  | Sklearn LOF |
| :---:   | :---: | :---: |
| 2 | 90%   | 90%  |
| 10 | 90%   | 100% |
| 20 | 80%   | 100% |

### Global Outliers
| Dimensions | Top N LOF  | Sklearn LOF |
| :---:   | :---: | :---: |
| 2 | 70%   | 70%  |
| 10 | 70%   | 100% |
| 20 | 90%   | 100% |

Tweaking c will affect the f1 score for both local and global outliers. Top N LOF does not perform better than Sklearn LOF for both global and local outliers.

## Experiment 9: ML Matt
### Vanilla Attempt
| Top N LOF with r = 11.5, c = 0.003125, n = 10167, k = 20, d = 44 | Sklearn LOF with contamination parameter set as the percentage of anomalous points |
| :---:   | :---:  |
| Runtime: 265 seconds | Runtime: 18.3 seconds |
| F1 Score:  27.6% | F1 Score: 28.1% |

### Tuning k
| Top N LOF with r =11.6, c = 0.003125, n =3050, k = 820, d = 44 | Sklearn LOF with contamination parameter set as the percentage of anomalous points and k set as 820|
| :---:   | :---:  |
| Runtime: 105 seconds | Runtime: 3 seconds |
| F1 Score: 20.7% | F1 Score: 20.6% |

## Experiment 10: Access behavior anomaly dataset
### Vanilla Attempt
| Top N LOF with r = 4.4, c = 0.003125, n = 589, k = 20, d = 9 | Sklearn LOF with contamination parameter set as the percentage of anomalous points|
| :---:   | :---:  |
| Runtime: 1 second | Runtime: < 0.1 second |
| F1 Score: 40.1% | F1 Score: 45.5% |

### Tuning k
| Top N LOF with r =4, c = 0.003125, n =177, k = 490, d = 9 | Sklearn LOF with contamination parameter set as the percentage of anomalous points and k set as 660|
| :---:   | :---:  |
| Runtime: < 1 second | Runtime: < 1 second |
| F1 Score: 52.5% | F1 Score: 57.6% |

## Experiment 11: Energy
### Vanilla Attempt
| Top N LOF with r = 5.8, c = 0.00125, n = 4517, k = 20, d = 18 | Sklearn LOF with contamination parameter set as the percentage of anomalous points|
| :---:   | :---:  |
| Runtime: 29 seconds | Runtime: 3.4 seconds |
| F1 Score: 32.5% | F1 Score: 34.2% |

### Tuning k
| Top N LOF with r =5.4, c = 0.00125, n =1355, k = 110, d = 18 | Sklearn LOF with contamination parameter set as the percentage of anomalous points and k set as 70|
| :---:   | :---:  |
| Runtime: 12 seconds | Runtime: 0.7 second |
| F1 Score: 27.3% | F1 Score: 31.1% |

Across Experiments 9, 10, 11, for both the vanilla attempt and after tuning k, sklearn has consistently performed better and faster than top n lof.

### Alternative Approach to hyperparameter tuning
| Top N LOF with r =5.4, c = 0.158, n =1355, k = 51, d = 18 | Sklearn LOF with contamination parameter set as the percentage of anomalous points, k set as 26|
| :---:   | :---:  |
| Runtime: 1 second | Runtime: 0.6 second |
| F1 Score: 32% | F1 Score: 33.2% |

Disadvantage to tuning Top N LOF: No clusters or points are pruned. The hyperparameters k and c have to be tuned while ensuring that there are clusters pruned.

## Experiment 12: Comparing runtime for very large datasets
The algorithms (Top N LOF and Sklearn LOF) are compared in 2 areas:
1. Runtime
2. Accuracy

These 2 areas are universal metrics used to evaluate any algorithm.

From the experiments conducted, accuracy between the 2 algorithms are comparable. The table below shows the comparison in runtime between the 2 algorithms.

| Size of dataset | Top N LOF | Sklearn LOF |
| :---:   | :---: | :---: |
| 1,000,000 rows | 119.5 seconds   | 7.1 seconds   |
| 2,000,000 rows | 230.1 seconds   | 16.4 seconds   |
| 3,000,000 rows | 409.9 seconds   | 28.3 seconds   |
| 14,000,000 rows | 1241 seconds   | 161.1 seconds   |
| 23,000,000 rows | 1726.2 seconds   | 265.8 seconds   |
| 60,000,000 rows | Memory Error   | 888.8 seconds   |
| 70,000,000 rows | Memory Error   | 1053.7 seconds (but vs code will crash)   |
| 80,000,000 rows | Memory Error   | 1301.7 seconds (but vs code will crash)   |
| 90,000,000 rows | Memory Error   | Memory Error   |
| 100,000,000 rows | Memory Error   | Memory Error   |

It is to note that Top N LOF takes longer than Sklearn for those datasets that are small enough for both algorithms to run.

# Source Data and Codes

Link to download data & results folder: https://app.box.com/s/yjk0ighknlk2q59ictw75khnp3s22e5d 

The code is split into multiple sections by experiment.

For Experiment 1, Comparing run time between Sklearn and Top N LOF \
Data used: data\synthetic_1 \
Results stored in: results\synthetic_1

For Experiment 2, What if anomalies are introduced? \
Data used: data\synthetic_2 \
Results stored in: results\synthetic_2

For Experiment 3, Increasing the dataset size to 500,000 rows with no anomalies \
Data used: data\synthetic_3 \
Results stored in: results\synthetic_3

For Experiment 4, Comparing F1 score for outlier class \
Data used: data\synthetic_4 \
Results stored in: results\synthetic_4

For Experiment 5, How does the parameter n affect Top N LOF’s performance? \
Data used: data\synthetic_5 \
Results stored in: results\synthetic_5

For Experiment 6, Quick fix to be able to prune clusters \
Data used: data\synthetic_6 \
Results stored in: results\synthetic_6

For Experiment 7, Calculating R and tuning C \
Data used: data\synthetic_7 \
Results stored in: results\synthetic_7

For Experiment 8, Comparing f1 score for outlier class \
Data used: data\synthetic_8 \
Results stored in: results\synthetic_8

For Experiment 9, ML Matt \
Data used: data\real_world_9 \
Results stored in: results\real_world_9

For Experiment 10, Access behavior anomaly dataset \
Data used: data\real_world_10 \
Results stored in: results\real_world_10

For Experiment 11, Energy \
Data used: data\real_world_11 \
Results stored in: results\real_world_11

The data and results for Experiment 12 have been omitted due to the large size of the files.
