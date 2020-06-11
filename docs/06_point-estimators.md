---
output: html_document
editor_options: 
  chunk_output_type: console
---



# Properties of point estimators {#estimators}



Estimator ($\hat{\theta}$): a function that can be applied to data to produce estimates of a true quantity

Estimate ($\theta$): the value of a quantity returned by an estimator applied to data (e.g., a sample mean, a parameter of a probability distribution, a regression coefficient)

Estimand ($\theta$): the quantity we are trying to estimate

Before we see the data, they can be represented as a random variable, $D$. After we see the data, they are no longer random, and represented by $d$. 

If we apply an estimator to $D$, the result is $\hat{\theta}(D)$, which can vary from one dataset to the next. The distribution of an estimator is sometimes called the *sampling distribution*. The sample size of $D$ will affect the estimate, and we use $n$ to denote the sample size in the expression, $\hat{\theta}_n(D)$. 

In the first example, we apply the following estimator to $n$ i.i.d. random variables $X_i$, which are normally distributed with a mean $\theta$ and variance of 1 ($X_i \sim N(\theta, 1)$):

$$
\begin{aligned}
\hat{\theta}_n(D) = \frac{1}{n} \sum_{i = 1}^n X_i \\
\end{aligned}
$$

That is, we would like to estimate the mean of our random variables, $X_i$. We can do this in `R`, for 25 random variables that have a mean of 0 and a variance of 1:


```r
set.seed(12)
d <- rnorm(n = 25, mean = 0, sd = 1)
mean(d)
```

```
## [1] -0.1883626
```

## Bias

The *bias* of an estimator is the difference between the true value of the quantity we're interested in
(e.g., $\theta$), and the expectation of our estimator ($E[\hat{\theta}_n(D)]$). That is, our estimator is unbiased when it does not consistently over- or under- estimate the expectation; that is to say, it is *accurate*. Formally, the bias is:

$$
\begin{aligned}
\text{B}(\hat{\theta}_n) = E[\hat{\theta}_n(D)] - \theta \\
\end{aligned}
$$

We prefer estimators whose bias is 0 (i.e., unbiased).   

### Exercise set 6-1

1. The bias of the sample mean for $X_i \sim N(\theta, 1)$ is 0. See handwritten notes. 

2. Examining estimators for a normal distribution:


```r
library(stfspack)
s.mat <- mat.samps(n = 25, nsim = 10000)
str(s.mat)
```

```
##  num [1:10000, 1:25] 0.435 -1.023 -1.746 1.36 -0.642 ...
```

```r
## Sampling distribution of means
ests.mean <- apply(s.mat, 1, mean)
mean_of_means <- mean(ests.mean)

## Sampling distribution of medians
ests.median <- apply(s.mat, 1, median)
mean_of_medians <- mean(ests.median)

par(mfrow = c(1,2))
hist(ests.mean)
abline(v = mean_of_means, col = "red")
hist(ests.median)
abline(v = mean_of_medians, col = "red")
```

<img src="06_point-estimators_files/figure-html/unnamed-chunk-2-1.png" width="672" />

The mean and the median both appear unbiased - that is, their sampling distributions are centered on 0. 

## Variance

An estimator's variance measures the *precision* of the estimator. We define it in the same way that we defined the variance of a random variable:

$$
\begin{aligned}
\text{Var}(\hat{\theta}_n) =& ~ E[(\hat{\theta}_n(D) - E[\hat{\theta}_n(D)])^2] \\
=& ~ E[(\hat{\theta}_n(D)^2] - (E[\hat{\theta}_n(D)])^2 \\
\end{aligned}
$$

### Exercise set 6-2

1. The variance of the sample mean for $X_i \sim N(\theta, 1)$ is $\frac{1}{n}$. If we don't know the distribution from which $X_i$ are drawn, just that it has a finite variance, $\sigma^2$, the variance of the sample means is $\frac{\sigma^2}{n}$. See handwritten notes. 

2. Does the sample median have a larger or smaller variance than the mean, when data are drawn from a normal distribution?


```r
library(stfspack) 
library(tidyverse)
n_sims <- 10000
s.mat <- mat.samps(n = 25, nsim = n_sims)
str(s.mat)
```

```
##  num [1:10000, 1:25] 1.414 0.468 -0.785 -0.257 -0.205 ...
```

```r
## Sampling distribution of means
ests.mean <- apply(s.mat, 1, mean)
var_of_means <- var(ests.mean)

## Sampling distribution of medians
ests.median <- apply(s.mat, 1, median)
var_of_medians <- var(ests.median)

var_of_means; var_of_medians
```

```
## [1] 0.04031047
```

```
## [1] 0.06237011
```

```r
df <- data.frame(estimator = c(rep("mean", n_sims), rep("median", n_sims)), 
                 value = c(ests.mean, ests.median))

df %>% 
  ggplot(aes(value, fill = estimator)) + 
  geom_density(alpha = 0.3)
```

<img src="06_point-estimators_files/figure-html/unnamed-chunk-3-1.png" width="672" />

The sample median has a larger variance than the sample mean. 

## Mean squared error

The *mean squared error* is a metric that combines bias (accuracy) and variance (precision) in one metric. It is the expected squared difference between the value of an estimator and the true quantity:

$$
\begin{aligned}
\text{MSE}(\hat{\theta}_n) =& ~ E[(\hat{\theta}_n(D) - \theta)^2] \\
=& ~ \text{B}(\hat{\theta}_n)^2 + \text{Var}(\hat{\theta}_n)
\end{aligned}
$$

### Exercise set 6-3

1. See handwritten notes or Edge solution. 

2. When estimating the first parameter of a normal distribution, the sample mean will have a lower mean squared error. This is because although both are unbiased estimators, the sample median has a higher variance. If bias for both is equal to zero, then the mean square error is simply the variance of the estimator. 

## Consistency

As we collect more data, it would be preferable for the estimator to get closer and closer to the estimand; that is, we wish the estimator to be *consistent*. A consistent estimator is one that converges in probability to the true value, and is defined formally as:

$$
\begin{aligned}
lim_{n \rightarrow \infty} \text{P}(|\hat{\theta}_n - \theta| > \delta) = 0
\end{aligned}
$$

where $\delta$ is any positive number. 

It turns out (if we complete a proof) that an estimator $\hat{\theta}_n$ is consistent if: 

$$
\begin{aligned}
lim_{n \rightarrow \infty} \text{MSE}(\hat{\theta}_n) = 0
\end{aligned}
$$

that is, an estimator is consistent if the mean squared error goes to zero as the sample size increases to infinity. Both biased and unbiased estimators can be consistent, Edge's figure 6.2 demonstrates this nicely. 

### Exercise set 6-4

1. Yes, the sample mean is consistent as an estimator of the first parameter (the population mean) of a normal distribution. We know this because the MSE is the sum of the bias squared and the variance. As $n$ increases, variance goes to zero (because $\frac{\sigma^2}{n}$). And we already showed (in ex. 6-1-2) that at large *n*, the bias of the sample mean is zero (this is also true at small *n*). 

- The first parameter of a normal distribution is also its expectation - so can we extend the sample mean as a consistent estimator of any distribution, as long as it has a finite variance? Yes, because the law of large numbers applies to any distribution. See Edge explanation. 

2. Use simulations to show that the sample median is a consistent estimator of the first parameter of a normal distribution. We already know that the sample median is unbiased, so the following simulations focus on the variance. 


```r
library(stfspack)
library(tidyverse)
n_sims <- 1000
n_samps <- 25

get_var_of_median <- function(n_sims, n_samps){
  s.mat <- mat.samps(n = n_samps, nsim = n_sims)
  ests.median <- apply(s.mat, 1, median)
  var_of_medians <- var(ests.median)
  return(var_of_medians)
}

n_samps_vector <- c(5, 10, 25, 50, 100, 200, 500) 
vector_length <- length(n_samps_vector)
var_vector <- rep(NA, vector_length)

for(i in 1:vector_length){
  var_vector[i] <- get_var_of_median(n_sims, n_samps = n_samps_vector[i])
}

plot(n_samps_vector, var_vector, col = "red", pch = 20, 
     xlab = "Number of samples", ylab = "Variance of medians", type = "b") 
abline(h = 0, lty = 2, col = "gray")
```

<img src="06_point-estimators_files/figure-html/unnamed-chunk-4-1.png" width="672" />

3. Considering $n$ i.i.d. random variables $X_i$, which are normally distributed with a mean $\theta$ and variance of 1 ($X_i \sim N(\theta, 1)$), are the following estimators (i) unbiased; and (ii) consistent?

  a. The sample mean is unbiased and consistent, we have shown these already. 

b. A shifted sample mean will be biased (e.g., because we are adding a constant to each value prior to taking the average), and will not be consistent because the mean squared error will never approach 0 (because it is biased). Also see Edge's explanation. 

c. The first observation, $X_1$ will be an unbiased estimator because it has an expectation of $\theta$. It has a variance of 1, and thus it is not consistent (because the variance does not approach zero as the number of samples increases). 

d. A 'shrunk' sample mean is biased and consistent; see handwritten notes for solution. 

4. Prove that if Eq. 6.7 holds, then Eq. 6.6 also holds. SKIPPED; see Edge for solution. 
