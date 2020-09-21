# Activation Function:
Activation functions here are described with thier uses and misuses
## Desirable properties for activation functions:
### 1. NonLinearity:
If activation layer is non-linear, it can be proven that a 2 layer neural network is a universal approximator for any function.
### 2. Range: 
For a finite range, gradient based methods are more stable, as only limited weights are affected in each pattern. For a infinite range, training is more efficient as results affect all weights (for small learning rates).
### 3. Continuously Differentiable:
Desirable for gradient based, (ReLU is not but it is possible), as binary step activation is not differentiable, can work with gradient based methods.
### 4. Monotonic:
The error surface is guarenteed to be convex and hence, good for gradient based optimization.
### Approximates near the origin:
If this is true, then the NN will work better for randomly initialized wieghts with very small values.

## Linear function:
Quite a no go for neural networks as it makes the hidden layers linear combinations of input layers , hence, making them redundant.  
Explaining further, while using gradient descent for backpropogation, it jumps towards the minimising direction of derivative, for linear this derivative is the linear multiplier (constant), hence, the gradient descent is convinced that there is no minimum, so no improvement.
> Y = sum(a*X)
## Step functions: 
Binary in nature, can only allow values above a certain threshold. Hence, not used for multilevel classification (more than 2 outputs expected).  
![image](https://user-images.githubusercontent.com/64798024/93735841-f68cb100-fbfb-11ea-9f2f-d2e20d0d1b29.png)

## Non-Linear Activation functions:
Is it possible to preserve only partial information from the neuron (like, preserving 90% information from neuron with more significance and 20% with less significance). For this we need non linear activation functions.
### 1. Sigmoid Functions:
Elongated 'S', 0 < Y < 1, f(X) = 1/(1+e^(-x)).   
![image](https://user-images.githubusercontent.com/64798024/93735949-4f5c4980-fbfc-11ea-9d06-9e8e52d069ed.png)  
Although sigmoid function is simple, reduces training time,major drawback is information loss as derivative has short range.
Besides the logistic function, sigmoid functions include the **ordinary arctangent**, the **hyperbolic tangent**, the **Gudermannian function**, and the **error function**, but also the **generalised logistic function** and **algebraic functions**
### Softmax functions:
It is an improvement upon sigmoid function, as not only the outcome is a fraction but the sum of the values is equal to 1. Hence, it can be inferred as probability.  
![image](https://user-images.githubusercontent.com/64798024/93736043-bed23900-fbfc-11ea-9d56-4422a1ae2f35.png)  
This is quite useful in classification tasks as it gives probability for gtting classified into each category.
### 1. ReLU (Rectified Linear Unit):
As sigmoid and softmax are used for output layers, ReLU has been proven to give better results for hidden layers. 
Quite a mix of two simple activations (linear and step), abovethershold the output grows linearly.  
![image](https://user-images.githubusercontent.com/64798024/93736383-c514e500-fbfd-11ea-8848-56f6e9932cfa.png)   
Relu has fewer vanishing gradient problems due to antisymmetry, so better gradient propogation.
has a drawback that the neurons with below threshold value are directly discarded (Dead neurons problem, bad when happen to large number of neurons). If we want to pass on that information too, we have a varient called Leaky ReLU, which performs like this.  
![image](https://user-images.githubusercontent.com/64798024/93736483-22a93180-fbfe-11ea-8347-a70ef419f486.png)   
Some of the ReLU variants include : Softplus (SmoothReLU), Noisy ReLU, Leaky ReLU, Parametric ReLU and ExponentialReLU (ELU).
## How to Select an Activation Function:
Softmax is preferred over sigmoid, ReLU is preferred over both for hidden layers.

*Next one on Optimizers!*
