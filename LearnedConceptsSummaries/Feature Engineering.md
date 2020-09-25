##### **1. Binarization of dataset:**
- Sometimes some values in data are anonlymously large (in orders of magnitudes), the model would be pulled by these large values while training. So to make the model robust, we binarize the count and clip all value greater than the threshold to the threshold.  
e.g.: In song predictor model, some people might listen to songs on infinite loop hence, unnecesarily increasing the number of counts. SO we clip them to make model robust.  
> - large counts are bad in unsupervised learning like k-means clustering (uses Euclidean distance as a similarity function to measure the similarity between data points. A large count in one element of the data vector would outweigh the similarity in all other elements, which could throw off the entire similarity measurement.)  

- Other method is *Quantization of count* into bins (convert continuous value to discrete one)   
- **Fixed width binning**: linear or custom - Algebraic or geometric depending on the span - then take log of the count for bringing them closer
```python  
>>> np.floor_divide(small_counts, 10)  
>>> np.floor(np.log10(large_counts))
```
- **Quantile binning**: fixed width binnings are easy but if there are large gaps betweeen the data then it is a problem and quantiles can divide data into blocks with equal distributions (median divides into halves, quartiles divide into 4ths, deciles into 10ths)
```python
>>> deciles = biz_df['review_count'].quantile([.1, .2, .3, .4, .5, .6, .7, .8, .9])
# Map the counts to quartiles
>>> pd.qcut(large_counts, 4, labels=False)
array([1, 2, 3, 0, 0, 1, 1, 2, 2, 3, 3, 0, 0, 2, 1, 0, 3], dtype=int64)
# Compute the quantiles themselves
>>> large_counts_series = pd.Series(large_counts)
>>> large_counts_series.quantile([0.25, 0.5, 0.75])
```

##### 2. Log Transformation:
Since a0 = 1, we have loga(1) = 0. This means that the log function maps the small range of numbers between (0, 1) to the entire range of negative numbers (–∞, 0). The function log10(x) maps the range of [1, 10] to [0, 1], [10, 100] to [1, 2], and so on. In other words, the log function compresses the range of large numbers and expands the range of small numbers. The larger x is, the slower log(x) increments. Log transform is good for dealing with high tailed distributions, where more probability is placed on rhs tail, log streches the tail on LHS and compresses tail on RHS.
```python
# Note that we add 1 to the raw count to prevent the logarithm from
# exploding into negative infinity in case the count is zero.
>>> biz_df['log_review_count'] = np.log10(biz_df['review_count'] + 1)
```
- **Power Transforms: Generalizations of Log Transforms** (these are variance stabilizing transforms)  
![image](https://user-images.githubusercontent.com/64798024/94251767-a3d73000-ff40-11ea-987f-073867b19100.png)  
Box-Cox transform for λ = 0 (the log transform), λ = 0.25, λ = 0.5 (a scaled and shifted version of the square root transform), λ = 0.75, and λ = 1.5. Setting λ to be less than 1 compresses the higher values, and setting λ higher than 1 has the opposite effect.
![image](https://user-images.githubusercontent.com/64798024/94251997-f31d6080-ff40-11ea-98ad-c7c7fadcc4fc.png)  
Box Cox works only for positive data, for negetive, shift by constant, then apply. 
```python
>>> from scipy import stats
>>> rc_log = stats.boxcox(biz_df['review_count'], lmbda=0)
By default, the scipy implementation of Box-Cox transform finds the lambda
# parameter that will make the output the closest to a normal distribution
>>> rc_bc, bc_params = stats.boxcox(biz_df['review_count'])
```
A probability plot, or probplot, is an easy way to visually compare an empirical distribution of data against a theoretical distribution. This is essentially a scatter plot of observed versus theoretical quantiles.
##### Feature Scaling and Normalization:
Models that are smooth functions of input get affected by order of magnitude of data. Unlike tree based models who don't.
- **Min Max Scaling:**
![image](https://user-images.githubusercontent.com/64798024/94257488-003e4d80-ff49-11ea-8589-1010097394ce.png)  
- **Standardization (Variance Scaling):** 
It subtracts off the mean of the feature (over all data points) and divides by the variance.
Hence, it can also be called variance scaling. The resulting scaled feature has a mean of 0 and a variance of 1.  
>Use caution when performing min-max scaling and standardization on sparse features. Both subtract a quantity from the original
feature value. For min-max scaling, the shift is the minimum over all values of the current feature; for standardization, it is the mean.
If the shift is not zero, then these two transforms can turn a sparse feature vector where most values are zero into a dense one. This in
turn could create a huge computational burden for the classifier, depending on how it is implemented.
- **l_square Normalization:**
![image](https://user-images.githubusercontent.com/64798024/94258063-e9e4c180-ff49-11ea-8d4a-7aa397acdb70.png)  
The ℓ2 norm sums the squares of the values of the features across data points, then takes the square root. After ℓ2 normalization, the feature column has norm 1.
```python
>>> import sklearn.preprocessing as preproc
# Standardization - note that by definition, some outputs will be negative
>>> df['standardized'] = preproc.StandardScaler().fit_transform(df[['n_tokens_content']])
# L2-normalization
>>> df['l2_normalized'] = preproc.normalize(df[['n_tokens_content']], axis=0)
```
for all scalings and normalizations, the distribution shape will remain the same only the x -axis will change.
