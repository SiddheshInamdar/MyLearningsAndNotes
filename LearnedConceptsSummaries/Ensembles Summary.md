# Different ensembles techniques: 
### By: Siddhesh Inamdar
Ensamble methods involve multiple models (called weak learners), guessing that together they will approximate the model in a better way.
Most of the single learners have a high bias (e.g. low degrees of freedom) or high variance (e.g. high degrees of freedom) 
Homogeneous we learners form homogenous ensembles (opposite for heterogeneous) 
**the weak models should be aggregated in the correct manner**
e.g. If we choose base model with low bias high variance, we should aggregate in a way to reduce variance (same for bias). 
**Three kinds of sub-classes:** 
> 1. Boosting
> 2. Bagging
> 3. Stacking
## Parallel Methods:
> 1. Bootstrapping
> 2. Bagging
> 3. Random Forests
 - We fit different learners independantly with each other. One of the parallel methods, base learners learn indipendently, and its possible to train them together, most famous "**Bagging** - bootstrap aggregating".
### Bootstraping: 
Statistical method of drawing N samples from datasets with replacement B observations.
(Assumptions: Dataset N should comprise enough information for model(**Representivity**). Size N should be large enough compared to B of bootstrap samples so they are not correlated (**independence**).). Bootstrap is genera;;y used to determine variance of the random function.
### Bagging
Fit multiple independent models and **Average** their predictions in order to get a model with low variance. But w can't fit fully indepedent models cause that will require a lot of data, so we use bootstrapping methods to implement approximately independent models.
> 1. create multiple bootstrap samples
> 2. fit a weak learner on these samples and aggregate their outputs
> 3. So obtain a model with lesser variance than its components
 - **Averageing weak learners does not change the explected answer but reduce its variance.**, just like averaging random variables reduce variance but not mean.  
> - Averaging for regression, majority vote for classification (Big advantage- can be parallelized)
### Random Forests:
Learning trees are a popular base. Multiple trees make forests.  
> Shallow Trees have more bias, less variance. Deep trees have more variancea and less bias.  
 - **To make trees even less correlated, RF not bootstraps samples but also features (keep only a random subset of them to build a tree).**
Sampling has an effect that all trees do not look the same in structure in decision making. **Another advantage - System more robust to missing data.** 
Observations with missing data can be classified or regressed  
  
## Boosting Methods:
**Sequential methods**, weaker models fitted are not independent to each other. Iterative fitting - Training of a model given in a step depenas in a model in previous step.
Produces a method that is less biased than components. unlike bagging algorithms, the main aim is not only to reduce variance, but to get a model that would consider those samples in data that were handled badly in previous model. (adaptive technique)
> Each new model focuses its efforts on observations most difficult to identify, creates a strong learner with even lower bias.(plus: also reduces variance)
- main focus on reducing bias, so base models involved have high bias. (computations can't be parallel)
How to choose models and how to aggregate results, two ways to do that
> 1. AdaBoost
> 2. Gradient Boosting
# Adaptive Boosting (AdaBoost):
model - weighted sum of weak learners  
![image](https://user-images.githubusercontent.com/64798024/93098491-8c887f00-f6c4-11ea-96cf-86d71fbc803c.png)  
instead of doing it repeatedly, we try to do that in a single shot  
![image](https://user-images.githubusercontent.com/64798024/93098978-1c2e2d80-f6c5-11ea-926c-ebc1ef07f7ff.png)  
where weights and coefficients are chosen to possibly improve the accuracy metric. Thus we ar optimising locally, instead of globally to append weak learners, one by one.
> **For binary classification:**  
1. update the weights and train new classifier based on misclassified data.  
2. Add weak learner to the weighted sum according to an update coefficient that expresse the performances of this weak model: the better a weak learner performs, the more it contributes to the strong learner.
 - LogitBoost (for classification) or L2Boost (for regression) are two variants of AdaBoost, deferring by choice of loss function.
 # Gradient Boosting:
 Also a weigthed sum of learners. We cast the optimization problem into a gradient descent one. At each iteration we fit the current learner to the opposite of the gradient of the current fitting error with respect to the current ensemble model.
 Theoritical gradient descent  
 ![image](https://user-images.githubusercontent.com/64798024/93101538-053d0a80-f6c8-11ea-862e-27e85be63a19.png)  
 So, assume that we want to use gradient boosting technique with a given family of weak models. At the very beginning of the algorithm (first model of the sequence), the pseudo-residuals are set equal to the observation values. Then, we repeat L times (for the L models of the sequence) the following steps:
1. fit the best possible weak learner to pseudo-residuals (approximate the opposite of the gradient with respect to the current strong learner)
2. compute the value of the optimal step size that defines by how much we update the ensemble model in the direction of the new weak learner
3. update the ensemble model by adding the new weak learner multiplied by the step size (make a step of gradient descent)
4. compute new pseudo-residuals that indicate, for each observation, in which direction we would like to update next the ensemble model predictions

Gradient boosting can adapt to a larger number of loss functions. (generalization of adaboost to arbitrary loss function)
## Stacking Methods:
Differs from Bagging and Boosting on 2 points:
> 1. Heterogeneous weak learners
> 2. Combine base models using a meta model
Say we take KNN, SVM and LR as weak models and NN as a meta model taking inputs from weak models, for L weak learners, we take the foll steps:
>1. Convert data into 2 folds
2. Choose L weak learners and feed data of the first fold
3. for each weak learner, make predictions for observations of second fold
4. fit meta model on second fold and fit the model on predictions made by weak models on 2nd fold.
 - Drawback : Only half data available for training the meta model, use k-fold approach to overcome

 *Next one would be on advanced methods, like XGBoost and CatBoost!!!* 
 






