### Steps to run

1. Install pacakges
```{sh}
pip install -r requirements.txt
```

2. Run preprocessing

The constants at the beginning of each of the notebooks (all three steps) contain relative path values (`BASE_DIR`, `DATA_DIR`, `MODEL_DIR` etc) and the hierarchy we want to run for (`HIERARCHY_COL` indicates the column name, `STORES` indicate the unique values in that column). These values __must be changed__ to the current paths and the hierarchy one is running for.

Run the cells in `step1_m5_preprocess.ipynb`. The processed data will be stored in the data dir, which is referenced in the next stage i.e. training. Seperate sets of features such as `BASE`, `PRICE`, `CALENDAR` etc are stored as seprate pickle files in the `DATA_DIR`. These files are read and the features are combined using the `id` and `d` column (which can identify a unique row).

3. Run training
    1. To run without tuning (harcoded hyperparameters) --> Run `step2a_basic_training.ipynb`
    2. To run with tuning: 
        1. __`modeling.py`__ also needs to be downloaded and kept in the same directory (as we import the class from there.) 
        2. For Bayesian hyperparamter tuning, we need to install the package: `hyperopt`. 
        3. Then we can run `step2b_tune.ipynb`.
        4. One can any Scikit Learn model here, just the hyperparamter search space, `fit_params` and model class should be changed.

The test data and trained models are saved in the `MODEL_DIR` (used in predictions).

4. Generating Predictions
Run `step3_predict_m5.ipynb`. Predictions (fully formatted) are stored under `BASE_DIR + /submissions/` directory. Last cell is for ensembling, use the previous submissions (palced in the `data` folder on Google Drive to combine them).