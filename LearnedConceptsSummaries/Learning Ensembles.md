# Different ensembles techniques:
Ensamble methods involve multiple models (called weak learners), guessing that together they will approximate the model in a better way.
Most of the single learners have a high bias (e.g. low degrees of freedom) or high variance (e.g. high degrees of freedom) 
Homogeneous we learners form homogenous ensembles (opposite for heterogeneous) 
**the weak models should be aggregated in the correct manner**
e.g. If we choose base model with low bias high variance, we should aggregate in a way to reduce variance (same for bias). 
> **Three kinds of sub-classes:** 
> 1. Boosting
> 2. Bagging
> 3. Stacking
## Parallel Methods:
> Bootstrapping
> Bagging
> Random Forests
We fit different learners independantly with each other.
One of the parallel methods, base learners learn indipendently, and its possible to train them together, most famous "**Bagging** - bootstrap aggregating".
### Bootstraping: 
Statistical method of drawing N samples from datasets with replacement B observations.
(Assumptions: Dataset N should comprise enough information for model(**Representivity**). Size N should be large enough compared to B of bootstrap samples so they are not correlated (**independence**).). Bootstrap is genera;;y used to determine variance of the random function.
### Bagging
Fit multiple independent models and **Average** their predictions in order to get a model with low variance. But w can't fit fully indepedent models cause that will require a lot of data, so we use bootstrapping methods to implement approximately independent models.
> 1. create multiple bootstrap samples
> 2. fit a weak learner on these samples and aggregate their outputs
> 3. So obtain a model with lesser variance than its components
**Averageing weak learners does not change the explected answer but reduce its variance.**, just like averaging random variables reduce variance but not mean.  
> Averaging for regression, majority vote for classification (Big advantage- can be parallelized)
### Random Forests:
Learning trees are a popular base. Multiple trees make forests.  
> Shallow Trees have more bias, less variance. Deep trees have more variancea and less bias.  
**To make trees even less correlated, RF not bootstraps samples but also features (keep only a random subset of them to build a tree).**
Sampling has an effect that all trees do not look the same in structure in decision making. **Another advantage - System more robust to missing data.** 
Observations with missing data can be classified or regressed  
  
## Boosting Methods:





