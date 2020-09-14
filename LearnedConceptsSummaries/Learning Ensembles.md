# Different ensembles techniques
Ensamble methods involve multiple models (called weak learners), guessing that together they will approximate the model in a better way.
Most of the single learners have a high bias (e.g. low degrees of freedom) or high variance (e.g. high degrees of freedom) 
Homogeneous we learners form homogenous ensembles (opposite for heterogeneous) 
**the weak models should be aggregated well**
e.g. If we choose base model with low bias high variance, we should aggregate in a way to reduce variance (same for bias). 
> **Three kinds of sub-classes:** 
> 1. Boosting
> 2. Bagging
> 3. Stacking
## Bagging
One of the parallel methods, base learners learn indipendently, and its possible to train them together, most famous "**Bagging** - bootstrap aggregating".
