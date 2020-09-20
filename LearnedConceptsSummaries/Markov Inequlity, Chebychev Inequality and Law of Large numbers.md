#https://github.com/SiddheshInamdar/MyLearningsAndNotes/new/master/LearnedConceptsSummaries
## Introductions:
For a random variable following normal distributions. 
> 68% of points will lie between 1 standard deviation.  
> 95% of points will lie between 2 standard deviations.  
> 99.7% of points will lie between 3 standard deviations.  
- multiples of standard deviations allow us to intuitively understand confidence levels in graphs etc.  
This generalization is okay for approximately normal distributions but not to some unknown highly non-normal distributions.
The confidence intervals can sometimes go lower than 75%. In these situations, it is useful to have a worst-case scenario of possible confidence interval values. Chebyshev's inequality helps with this as at most (1/k^2) of an arbitrary distribution falls under k*(standard dev) of the mean.

## Markov's Inequality:
For some non-negetive random variable X and a real number a > 0, the probability of X > a is less than or equal to the expected value of (X/a).
P(X >= a) <= E(X)/a. It can be shown in this image for Chi Squared function.  

![image](https://user-images.githubusercontent.com/64798024/93709743-7a905b80-fb5e-11ea-9221-f1135512015e.png)  

For large values of a curve will get closer to the bound at 0. 

## Chebechev's Inequality:
After understanding Markov Inequality, it is fairly easy to understand this one. Now we replace the X by |X - X'|, and a by sigma*.  
![image](https://user-images.githubusercontent.com/64798024/93710117-baa50d80-fb61-11ea-85ca-f6c80d2374ac.png)  

In short, we applied Markov's inequality to a random variable. The point at X = μ can be thought of as pulling the standard deviation downwards while the points at X = μ ± k pull it upwards. it makes sense that we would want the distribution inside of the bound to reduce the standard deviation as much as possible while the distribution outside of the bound should increase the standard deviation as little as possible.

## Law of Large Numbers:
Chebychev's inequality might be helpful in making a rough estimate of confidence intervals, but proves things in stats.
e.g. Law of Large numbers.  
![image](https://user-images.githubusercontent.com/64798024/93710747-91d34700-fb66-11ea-9357-26e626da435d.png)  
The graphical interpretation would be like  
![image](https://user-images.githubusercontent.com/64798024/93710794-d19a2e80-fb66-11ea-9d9b-eaa45a3a4c5f.png)  

Thats it for now!!



