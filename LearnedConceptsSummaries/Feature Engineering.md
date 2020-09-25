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
