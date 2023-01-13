**Refer to Results on open-source datasets_caa130123 for more details**

The algorithms (Top N LOF and Sklearn LOF) are compared in 2 areas:
Runtime
Accuracy

These 2 areas are universal metrics used to evaluate any algorithm.

From the experiments conducted, accuracy between the 2 algorithms are comparable.

For runtime, however, Top N LOF has a larger advantage over Sklearn in terms of being able to process larger datasets without running into memory error.

| Size of dataset | Top N LOF | Sklearn LOF |
| :---:   | :---: | :---: |
| 1,000,000 rows | 119.5 seconds   | 7.1 seconds   |
| 2,000,000 rows | 230.1 seconds   | 16.4 seconds   |
| 3,000,000 rows | 409.9 seconds   | 28.3 seconds   |
| 23,000,000 rows | 1726.2 seconds   | 265.8 seconds   |
| 90,000,000 rows | 4213.6 seconds   | Memory Error   |
| 100,000,000 rows | 4396.4 seconds   | Memory Error   |

However, it is to note that Top N LOF takes longer than Sklearn for those datasets that are small enough for Sklearn to run.
