# Summary
**Refer to Results on open-source datasets_caa130123 for more details** 

The algorithms (Top N LOF and Sklearn LOF) are compared in 2 areas:
1. Runtime
2. Accuracy

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

# Source Data and Codes

Link to download data & results folder: https://app.box.com/s/yjk0ighknlk2q59ictw75khnp3s22e5d 

The code is split into multiple sections by experiment.

For Experiment 1, Comparing run time between Sklearn and Top N LOF \
Data used: data\synthetic_1 \
Results stored in: results\synthetic_1

For Experiment 2, Comparing run time between Sklearn and Top N LOF \
Data used: data\synthetic_2 \
Results stored in: results\synthetic_2

For Experiment 3, Comparing run time between Sklearn and Top N LOF \
Data used: data\synthetic_3 \
Results stored in: results\synthetic_3

For Experiment 4, Comparing run time between Sklearn and Top N LOF \
Data used: data\synthetic_4 \
Results stored in: results\synthetic_4

For Experiment 5, Comparing run time between Sklearn and Top N LOF \
Data used: data\synthetic_5 \
Results stored in: results\synthetic_5

For Experiment 6, Comparing run time between Sklearn and Top N LOF \
Data used: data\synthetic_6 \
Results stored in: results\synthetic_6

For Experiment 7, Comparing run time between Sklearn and Top N LOF \
Data used: data\synthetic_7 \
Results stored in: results\synthetic_7

For Experiment 8, Comparing run time between Sklearn and Top N LOF \
Data used: data\synthetic_8 \
Results stored in: results\synthetic_8

For Experiment 9, Comparing run time between Sklearn and Top N LOF \
Data used: data\real_world_9 \
Results stored in: results\real_world_9

For Experiment 10, Comparing run time between Sklearn and Top N LOF \
Data used: data\real_world_10 \
Results stored in: results\real_world_10

For Experiment 11, Comparing run time between Sklearn and Top N LOF \
Data used: data\real_world_11 \
Results stored in: results\real_world_11

The data and results for Experiment 12 have been omitted due to the large size of the files.
