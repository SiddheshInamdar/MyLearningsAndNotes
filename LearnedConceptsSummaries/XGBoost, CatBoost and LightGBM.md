# XGBoost, CatBoost and LightGBM
Various methods are developed on previous quite simpler ensemble methods like bagging and boosting. To summarize it, read my previous [blog on ensemble methods](https://github.com/SiddheshInamdar/MyLearningsAndNotes/blob/master/LearnedConceptsSummaries/Ensembles%20Summary.md).
Now we move on to some advanced methods that have shown impressive performance in building advanced machine learning models.
## XGBoost Summary: 
It was introduced in 2014 as a research and has delivered outstanding results in Machine Learning Hackathons. The algorithm works more efficiently than comparitively simpler ones by using a parallel and distributed computing resource. The principal use of bagging and boosting algorithms which use Classification and Regression Trees (CART) is to reduce variance and use gradient boosting framework just like Gradient Boosting Machines (GBMs).  
However, XGBoost improves upon GBM by two ways:
> System Optimization  
> Algorithmic Enhancements 
making algorithmic enhancements.
### 1. System Optimization:
 - **Parallelization:**  
 Two loops primarily compute the model in GBM, outer loop enumerates the nodes and inner loop calculates the features on each node. But switching the two actually improves the training time by implementing parallelization, a global scan on all instances and sorting parallely.  
 - **Tree Pruning:**  
 The algorithm works by setting a max depth parameter, node splitting criterion is greedy in nature and negetive loss criterion at the point of split. Improves computational performance significantly.
 - **Hardware Optimization:**  
 Use hardware efficiently, allocates multiple buffers and multi core, using full space available in the disk.
 ### Algorithmic Enhancements:
 - **Regularization:**  
 Complex models get penalized by using LASSO (L1) and Rigde (L2) regularization to prevent overfitting.
 - **Sparsity Awareness:**  
Uses sparsity awareness split finding algorithm to trace patterns in sparsity of data.

## CatBoost:


  


