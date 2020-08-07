---
output: html_document
editor_options: 
  chunk_output_type: console
---



# Semiparametric estimation and inference {#semiparametric}



> Parametric: governed by parameters; e.g., normal distributions

> Nonparametric: not governed by parameters; used when we cannot assume that the distribution of a random variable follows a particular probability distribution

> Semiparametric: a model whose behavior is partially governed by parameters

> Empirical distribution function: summarizes all the information that the data provide about a random variable's distribution

The empirical distribution function $\hat{F}_n(z)$ gives the proportion of *observations in a sample* that are less than or equal to a constant $z$: 

$$
\begin{aligned}
\hat{F}_n(z) =& \frac{1}{n} \sum_{i = 1}^n I_{X_i \leq z}
\end{aligned}
$$

where $I$ is an indicator variable that states whether observation $X_i$ is less than or equal to $z$. 

### Exercise set 8-1

1. Comparing an ECDF with a CDF for the normal distribution

  a. As the sample size increases, the ECDF approximates the CDF of the normal distribution. 


```r
n <- 500
x.vals <- seq(-3, 3, length.out = 10000)
Fx <- pnorm(x.vals, 0, 1)
plot(x.vals, Fx, xlab = "z", ylab = "F(z)", type = "l")
x <- rnorm(n, 0, 1)
lines(ecdf(x), verticals = TRUE, do.points = FALSE, lty = 2)
```

<img src="08_semiparametric-estimation_files/figure-html/unnamed-chunk-1-1.png" width="672" />

  b. Comparing an ECDF with a CDF for the Poisson distribution


```r
set.seed(22)
n <- 30
lambda <- 10
x.vals <- seq(0, 30, by = 1)
Fx <- ppois(x.vals, lambda = lambda)
plot(x.vals, Fx, xlab = "z", ylab = "F(z)", type = "p")
x <- rpois(n, lambda = lambda)
lines(ecdf(x), verticals = TRUE, do.points = FALSE, lty = 2)
```

<img src="08_semiparametric-estimation_files/figure-html/unnamed-chunk-2-1.png" width="672" />

2. See handwritten notes. 

## Semiparametric point estimation using the method of moments

> Methods of moments: a semiparametric approach to estimation  
> Method of maximum likelihood: a parametric approach to estimation

Suppose $X$ is a random variable. The $j$th **moment** of the distribution is: 

$$
\begin{aligned}
\mu_j =& E(X^j)
\end{aligned}
$$

where $\mu$ is used as the symbol for a moment. For example $\mu_1 = E(X)$. It is easy to express the first moment of $X$ as an expression using $X$ - but what about $\mu_2$?

$$
\begin{aligned}
\mu_2 =& E(X^2)
\end{aligned}
$$

Now we have expressed the second moment, $\mu_2$, as the expectation of a new random variable, $X^2$. At least this is how I interpret it. From my reading, I gather this is not so satisfying, because the second moment is then usually rearranged in the following way. 

First, we need to recall the definition of Var($X$):

$$ 
\begin{aligned}
\text{Var}(X) = \text{E}(X^2) - [\text{E}(X)]^2 \\
\end{aligned}
$$

So, if we rearrange we get:

$$ 
\begin{aligned}
\text{E}(X^2) = \text{Var}(X) + [\text{E}(X)]^2 \\
\end{aligned}
$$

We can continue on with 3rd, 4th, 5th, etc, moments. But expressing these in terms of $X$ is, I am guessing, a harder challenge. These additional moments describe further the probability distribution, but typically knowing the first and second moments is enough for practical purposes (our purposes). As an aside, the third moment gives us the *skewness*, and the fourth moment gives us the *kurtosis*, of the distribution. Finally, it is worth noting the notation for *a moment* - here I have used $\mu$, becuase it is often used in statistics notes (that I found online). This can be confusing, because we often use $\mu$ for the population mean. But we won't do that here, for clarity. 

So, let us say that $X$ follows a Normal($\theta$, $\sigma^2$) distribution. In this case, we know that E($X$) = $\theta$, and that Var($X$) = $\sigma^2$. So we can express the first and second moments as:

$$ 
\begin{aligned}
\mu_1 =& ~ \text{E}(X) \\
=& ~ \theta \\
\mu_2 =& ~ \text{E}(X^2) \\
=& \text{Var}(X) + [\text{E}(X)]^2 \\
=& ~ \sigma^2 + \theta^2 \\
\end{aligned}
$$

So we have expressed the moments in terms of the parameters of the distribution we are trying estimate. We can rearrange these, to express the *parameters* in terms of $X$ - which is exactly what we want to do, since we are trying to estimate $\theta$ and $\sigma^2$!

$$ 
\begin{aligned}
\theta =& ~ \text{E}(X) \\
\sigma^2 =& ~ \text{E}(X^2) - [\text{E}(X)]^2 \\
\end{aligned}
$$

To paraphrase Edge, we can estimate the moments of arbitrary distributions (i.e., distributions that are not described by parameters) by following these steps:

  1. Write the equations that give the moments of a random variable in terms of the parameters being estimated
  
  2. Solve the equations from (1) for the desired parameters, giving expressions for the parameters in terms of the moments
  
  3. Estimate the moments and plug the estimates into the expressions for the parameters from (2)
  
> Plug-in estimation: perhaps I'm oversimplifying here, but this sounds like awesome jargon for 'calculate your estimator from data'. In other words, if you want the population mean -  collect some data and calculate the mean. Then 'plug that in' to your population mean. 

We can express a plug-in estimator of the $k$th moment of $X$, E($X^j$) as the $k$th *sample moment*:

$$ 
\begin{aligned}
\overline{X^k} = \frac{1}{n} \sum_{i = 1}^n X_i^k
\end{aligned}
$$

So to recap: a *moment* describes the random variable $X$. A *sample moment* is an estimate of the moment using independent samples ($X_1, X_2, X_3$) drawn from $X$. 

### Exercise set 8-2

1. Supose $X_1, X_2, ..., X_n$ are I.I.D observations. 
 
  a. What is the plug-in estimator of the variance of $X$?

$$ 
\begin{aligned}
\sigma^2 =& ~ \text{E}(X^2) - [\text{E}(X)]^2 \\
\hat\sigma^2 =& ~ \frac{1}{n} \sum_{i = 1}^n X_i^2 - [\frac{1}{n} \sum_{i = 1}^n X_i]^2 \\
\end{aligned}
$$
  b. What is the plug-in estimator for the standard deviation of $X$?
  
$$ 
\begin{aligned}
\hat\sigma =& ~ \sqrt{\frac{1}{n} \sum_{i = 1}^n X_i^2 - [\frac{1}{n} \sum_{i = 1}^n X_i]^2} \\
\end{aligned}
$$

  c. What is the plug-in estimator of the covariance of $X$ and $Y$?

Here is the formula for the covariance, as a reminder:

$$
\begin{aligned}
\text{Cov}(X,Y) =& ~ \text{E}([X - \text{E}(X)][Y - \text{E}(Y)]) \\
                =& ~ \text{E}(XY) - \text{E}(X)\text{E}(Y)
\end{aligned}
$$
Let's use the 2nd equation: 

$$
\begin{aligned}
\text{Cov}(X,Y) =& ~ \frac{1}{n} \sum_{i = 1}^n X_iY_i - [\frac{1}{n} \sum_{i = 1}^n X_i][\frac{1}{n} \sum_{i = 1}^n Y_i] \\
\end{aligned}
$$

  d. What is the plug-in estimator of the correlation of $X$ and $Y$?

Here is the formula for the correlation, as a reminder:

$$
\begin{aligned}
\text{Cor}(X,Y) =& ~ \rho_{X,Y} \\
                =& ~ \frac{\text{Cov}(X,Y)}{\sqrt{\text{Var}(X)\text{Var}(Y)}} \\
                =& ~ \frac{\text{Cov}(X,Y)}{\sigma_X \sigma_Y}\\
\end{aligned}
$$

Plugging in, we get:

$$
\begin{aligned}
\rho_{X,Y}      =& ~ \frac {\frac{1}{n} \sum_{i = 1}^n X_iY_i - 
                                  [\frac{1}{n} \sum_{i = 1}^n X_i][\frac{1}{n} \sum_{i = 1}^n Y_i]}  
                           {\sqrt{
                                  \frac{1}{n} \sum_{i = 1}^n X_i^2 - 
                                  [\frac{1}{n} \sum_{i = 1}^n X_i]^2}]
                                  [\frac{1}{n} \sum_{i = 1}^n Y_i^2]
                                  } \\
\end{aligned}
$$

2. Though the plug-in estimator of the variance is consistent, it is biased downward. 

  a. Demonstrate the downward bias in R with simulations. 
  
<!-- # ```{r} -->
<!-- # n_obs <- 5 -->
<!-- # n_sims <- 10000 -->
<!-- # x <- mat.samps(n = n_obs, nsim =  n_sims) -->
<!-- # x <- rnorm(n = n, mean = 0, sd = 1) -->
<!-- # x_mean <- rowMeans(x) -->
<!-- # x_sd <- apply(X = x, MARGIN = 1, FUN = sd) -->
<!-- # x_var <- x_sd^2 -->
<!-- #  -->
<!-- # mean(x_mean) -->
<!-- # mean(x_var) -->
<!-- # hist(x_mean) -->
<!-- # hist(x_var) -->
<!-- #  -->
<!-- # n <- 5 -->
<!-- # nsamps <- 100000 -->
<!-- # x <- rnorm(nsamps*n,0,1) -->
<!-- # head(x) -->
<!-- # samps <- matrix(x, nrow = nsamps, ncol = n) -->
<!-- # var.pi <- function(vec){ -->
<!-- #   return(sum((vec-mean(vec))^2)/length(vec)) -->
<!-- # } -->
<!-- # vars.pi <- apply(samps, 1, var.pi) -->
<!-- # mean(vars.pi) -->
<!-- #  -->
<!-- #  -->
<!-- # ``` -->


### Exercise set 8-3

## Semiparametric interval estimation using the bootstrap 

### Exercise set 8-4

## Semiparametric hypothesis testing using permutation tests

### Exercise set 8-5

## Chapter summary