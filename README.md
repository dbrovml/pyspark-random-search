# Distributed random hyperparameter search with PySpark
This repo contains a technical demo of distributing random hyperparameter search using pyspark. The main issue in running distributed hyperparameter tuning jobs using sequential model-based techniques is balancing parallelism and information efficiency. Random search does not assume the use of parallel trial results in making decision on the next step of optimization. This allows for easy parallelization.<br><br> *Note*: this is a simplified and slightly convoluted example that reduces the functionality of spark to simply submiting small-sized jobs to provisioned workers, i.e. it does not utilise the distributed filesystem capabilities. A better alternative would be to use something like `hyperopt.SparkTrials` that are well-supported by Databricks.

**Facts**:
- [Adult income dataset](https://archive.ics.uci.edu/ml/datasets/adult) is used as a toy example.
- Azure edition of Databricks is used for provisioning pyspark infrastrucutre.
- Basic sklearn classifiers are used as model examples.
- MLFlow is used for trial tracking (it is also well-integrated with Databricks).
- Hyperopt hyperparameter spaces are used for random sampling.

**Workflow**:
1. `job-preprocess.ipynb` - preprocess the data, encode features and prepare train-validation splits.
2. `job-search.ipynb` - uses `.map()` method on a serialized dummy list to run parallel evaluations.