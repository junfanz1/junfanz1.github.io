---
title: "Data Science Practical Guides"
categories:
  - Blog
  - Practical Guide
tags:
  - Data Science
  - Machine Learning


---

2019 - 11 - 2


<script async src="//busuanzi.ibruce.info/busuanzi/2.3/busuanzi.pure.mini.js"></script>

<span id="busuanzi_container_site_pv">
    Total <span id="busuanzi_value_site_pv"></span> views on my blog.
</span>

<span id="busuanzi_container_site_uv">
  You are number <span id="busuanzi_value_site_uv"></span> visitor to my blog.
</span>

<span id="busuanzi_container_page_pv">
  <span id="busuanzi_value_page_pv"></span> hits on this page.
</span>


<script type="text/javascript" async
  src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-MML-AM_CHTML">
</script>


# Kaggle Competition Pipeline

|  Feature Engineering |  Modeling | 
|---|---|
| Image Classification | Scaling, shifting, rotation, CNNs (ResNet, VGG, dense-net)|
|Sound Classification| Fourier, specgrams, scaling, CNNs (CRNN), LSTM|
| Text Classification | Tf-idf, SVD, stemming, spell checking, stop word's removval, x-grams, GBMs, Linear, DL, Naive Bayes, KNNs, LibFM, LibFFM|
| Time Series | Lags, weighted averaging, exponential smoothing, Autoregressive models, ARIMA, linear, GBMs, DL, LSTMs|
| Categorical features | Tagent enc, frequency, one-hot, ordinal, label encoding, GBMS, Linear, DL, LibFM, LibFFM|
| Numerical features | Scaling, binning, derivatives, outlier removals, dimension reduction, GBMs, Linear, DL, SVMs|
| Interactions | multiplications, divisions, group-by-features, concatenations, GBMs, Linear, DL|
| Recommenders | Features on transaction history, Item popularity, CF, DL, LibFM, LibFFM, GBMs, frequency of purchase, acquire valued shopers|
|||

# Ensembling

1. All this time, __predictions__ on internal validation & test are __saved__. If __collaborating__ with others, this is the point where everyone passes on their predictions.
2. Different ways to combine from __averaging__ to multilayer __stacking__.
3. Small data requires simpler ensemble techniques (averaging)
4. Helps to average a few __low-correlated predictions__ with good scores.
5. Bigger data can utilize stacking.
6. __Stacking process repeats__ the modeling process

# Matrix Factorization

1. Several MF methods can find in sklearn
2. SVD & PCA: Standard tools for matrix factorization
3. Truncated SVD: works with sparse matrices
4. Non-negative Matrix Factorization (NMF): ensures that all latent factors are non-negative; good for counts-like data

__Practical Notes__

- Matrix factorization is a very general approach for dimensionality reduction and feature extraction
- Can be applied for transforming categorical features into real-valued
- Many tricks suitable for linear models can be useful for MF.


# XgBoost & LightGBM

__Inputs__

|  XgBoost |  LightGBM | 
|---|---|
|  max-depth |  max-depth / num_leaves | 
|  subsample |  bagging_fraction | 
|  colsample_bytree, colsample_bylevel |  feature_feaction |  
| __min_child_weight, lambda, alpha__ | __min_date_in_leaf, lambda_l1, lambda_l2__ |
| eta, num_round | learning_rate, num_iterations|
|seed|*_seed|

# Sklearn

## Random Forest / Extra Trees

- N_estimators (the higher the better)
- max_depth
- max_features
- min_sample_leaf
- criterion
- random_state
- n_jobs

## Neural Nets

- Number of neutrons per layer
- Number of layers
- Optimizers (SGP + momentum / Adam, Adadelta, Adagrad, in practice to lead to more overfitting)
- Batch size 
- Learning rate
- Regularization (L1/L2 for weights, Dropout/Dropconnect, Static DropConnect)



# Mean Encoding

Very big dataset, separable.

__Comparison__

- Label encoding: random order, no correlation with target
- Mean encoding: separate 0 from 1, reach a better loss with shorter trees.

XgBoost & LightGBM can't handle large cardinality.

__The more complicated / nonlinear feature target dependency, the more effective is mean encoding.__

Notes:

- Validation should be impeccable.
- Basics for stacking
- Need regularization

# Regularization: battle with target variable leakage

1. Cross Validation loop inside training data (4 - 5 folds robust)
2. Smoothing
3. Adding random noise
4. Sorting & Calculating expanding mean

Notes:

- least amount of leakage
- no hyper parameters
- irregular encoding quality 
- built-in in CatBoost

# Generalization & Extensions

1. Using target variable in different tasks, regression multiclass
2. Domains with many-to-many relations
3. Time Series
4. Encoding interactions and numerical features

__Pros:__

- Compact transformation of categorical variables
- Powerful basis for feature engineering

__Cons:__

- Need careful validation, can overfit
- Significant improvement only on specific datasets

