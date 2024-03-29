---
output: html_document
editor_options: 
  chunk_output_type: console
---



# Properties of random variables {#randomvars}



## Expected values and the law of large numbers

When summarizing a probability distribution, it is useful to have a measure of:

  - Location (*Expectation*; E($X$))
  - Dispersal (*Variance*; Var($X$))

In this section, we're focusing on the expectation. 
  
The expectation of a discrete random variable is the average:

$$
\begin{aligned}
\text{E}(X) =& \sum_{i = 1}^{k}x_i P(X = x_i) \\
=& \sum_{i = 1}^{k}x_i f_X(x_i) \\
\end{aligned}
$$

If $Y$ represents a six-sided die, then:

$$
\begin{aligned}
\text{E}(Y) =& \sum_{i = 1}^{k}y_i f_Y(y_i) \\
=& 1(1/6) + 2(1/6) + 3(1/6) + 4(1/6) + 5(1/6) + 6(1/6) \\
=& 21/6 \\ 
=& 7/2 \\
\end{aligned}
$$

If $X$ is continuous:

$$
\begin{aligned}
\text{E}(X) =& \int_{- \infty}^{\infty} x f_X(x) dx \\
\end{aligned}
$$

Here we are integrating over the probability density function, rather than summing over the mass density function. 

### Weak law of large numbers

The expectation is more like a long-term average, rather than an actual instance (7/2 is not a possible instance of a dice roll). 

$X_i$ are i.i.d.

Assume E($X_1$) = E($X_2$) = ... = E($X_n$) = $\mu$

Define $\overline{X}_n$ as the mean of the observations:

$$
\begin{aligned}
\overline{X}_n = \frac{1}{n} (X_1 + X_2 + X_3 + ... + X_n)
\end{aligned}
$$

As $n \rightarrow \infty$, $\overline{X}_n$ "converges in probability" to $\mu$. This means for any positive constant $\delta$, 

$$
\begin{aligned}
lim_{n \rightarrow \infty} \text{P}(|\overline{X}_n - \mu| > \delta) = 0
\end{aligned}
$$

### Handy facts about expectations

The expectation of a constant times a random variable is the constant times the expectation of the random variable:

$$ 
\begin{aligned}
\text{E}(aX) = a \text{E}(X)
\end{aligned}
$$
The expectation of a constant is the constant:

$$ 
\begin{aligned}
\text{E}(c) = c
\end{aligned}
$$

The expectation of a sum of random variables is the sum of the expectations of those random variables: 

$$ 
\begin{aligned}
\text{E}(X + Y) = \text{E}(X) + \text{E}(Y)
\end{aligned}
$$

Putting all these facts together, we can calculate the expectation of two random variables $X$ and $Y$ as:

$$ 
\begin{aligned}
\text{E}(aX + bY + c) = a \text{E}(X) + b \text{E}(Y) + c
\end{aligned}
$$

This is called the **linearity of expectation**, which we will use frequently in the exercises. Linearity does not hold for other measures of location (e.g., median, mode). This fact accounts, in part, for the privileged status of the mean in statistics. 

To calculate the expectation of a function:

$$ 
\begin{aligned}
\text{E}[g(X)] = \sum_{i = 1}^{k} g(x_i)f_X(x_i)
\end{aligned}
$$

$$ 
\begin{aligned}
\text{E}[g(X)] = \int_{-\infty}^{\infty} g(x)f_X(x)dx
\end{aligned}
$$


### Exercise set 5-1

1a. Expected value of a Bernoulli random variable with parameter *p*?

$$ 
\begin{aligned}
f_X(x) = \text{P}(X = x) = p^x(1 - p)^{1-x} \text{ for } x \in \text{{0, 1}} \\
\end{aligned}
$$

Because there are only two outcomes (0 or 1), we can compute the expectation directly:

$$ 
\begin{aligned}
\text{E}(X) =& \sum_0^1 x f_X(x) \\
=& \sum_0^1 x p^x(1 - p)^{1-x} \\ 
=& 0 p^0(1 - p)^{1-0} + 1 p^1(1 - p)^{1-1} \\
=& 0 p^0(1 - p)^{1} + 1 p^1(1 - p)^{0} \\
=& 0 (1) (1-p) + p(1) \\ 
=& 0 + p \\
=& p
\end{aligned}
$$

1b. What is the expected value of a binomial random variable with parameters $n$ and $p$?

Here's the pmf for the binomial distribution:

$$ 
\begin{aligned}
f_X(x) = \text{P}(X = x) = \binom{n}{x} p^x(1 - p)^{n - x} \text{ for } x \in \text{{0, 1, 2, ..., n}} \\
\end{aligned}
$$

If we plug that into the equation for E($X$), we get:

$$ 
\begin{aligned}
\text{E}(X) =& \sum_0^n x f_X(x) \\
=& \sum_0^n x \binom{n}{x} p^x(1 - p)^{n - x} \\ 
\end{aligned}
$$
Well, I don't know how to evaluate this sum directly, considering the upper limit of $n$ is infinite. So we'll use the fact that the binomial is the sum of $n$ independent Bernoulli trials ($X_i$). 

$$ 
\begin{aligned}
\text{E}(X) =& \text{E}(\sum_{i=1}^nX_i)
\end{aligned}
$$

Because the expectation is linear, the expectation of the sum is the sum of the expectations; we can rearrange:

$$ 
\begin{aligned}
\text{E}(X) =& \sum_{i=1}^n \text{E}(X_i)
\end{aligned}
$$

From 1a, we can substitute $p$ for $\text{E}(X_i)$:

$$ 
\begin{aligned}
\text{E}(X) =& \sum_{i=1}^n p \\
=& np
\end{aligned}
$$

1c. What is the expected value of a discrete uniform random variable with parameters $a$ and $b$?

The probability mass function is:

$$ 
\begin{aligned}
\text{P}(X = k) =& \frac{1}{b - a + 1} \\
\end{aligned}
$$
The expectation is:

$$ 
\begin{aligned}
\text{E}(X) =& \sum_{x = a}^b x f_X(x) \\
=& \sum_{x = a}^b x \frac{1}{b - a + 1}  \\
=& \frac{1}{b - a + 1} \sum_{x = a}^b x \\
\end{aligned}
$$

We were given a hint that is useful now: for integers $a$ and $b$ with $b > a$, the sum of all the integers including $a$ and $b$, is:

$$ 
\begin{aligned}
\sum_{k = a}^b k  =& \frac{(a + b)(b - a + 1)}{2} \\
\end{aligned}
$$

So, plugging that hint in we get:

$$ 
\begin{aligned}
=& \frac{1}{b - a + 1} \times \frac{(a + b)(b - a + 1)}{2} \\
=& \frac{a + b}{2} \\
\end{aligned}
$$

1d. What is the expected value of a continuous uniform random variable with parameters $a$ and $b$?

The probability density function is:

$$ 
\begin{aligned}
\text{P}(X) =& \frac{1}{b - a} \\
\end{aligned}
$$

The expectation is:

$$ 
\begin{aligned}
\text{E}(X) =& \int_{a}^b x f_X(x) dx \\
=& \int_{a}^b x \frac{1}{b - a} dx  \\
=& \frac{1}{b - a} \int_{a}^b x  dx  \\
\end{aligned}
$$

Now we have to integrate the 2nd term:

$$ 
\begin{aligned}
=& \frac{1}{b - a} \times \frac{1}{2} x^2 \bigg\rvert_{a}^{b} \\
=& \frac{1}{b - a} \times (\frac{b^2}{2} - \frac{a^2}{2}) \\
=& \frac{1}{b - a} \times (\frac{b^2 - a^2}{2}) \\
\end{aligned}
$$

We use the hint from earlier, that $b^2 - a^2 = (b-a)(b+a)$:

$$ 
\begin{aligned}
=& \frac{1}{b - a} \times (\frac{(b-a)(b+a)}{2}) \\
=& \frac{a + b}{2} \\
\end{aligned}
$$


2. Exploring the law of large numbers by simulation. In Edge's code block below, `samp.size` represents $n$ in the weak law of large numbers (above); `n.samps` represents independent random variables $X_n$. The expectation for all $X_i$ is $\mu$. 

```r
samp.size <- 20
n.samps <- 1000
samps <- rnorm(samp.size * n.samps, mean = 0, sd = 1)
# Each column represents a random variable, X_i
# Each row represents a sample (instance) drawn from X_i
samp.mat <- matrix(samps, ncol = n.samps) 
str(samp.mat)
```

```
##  num [1:20, 1:1000] 0.875 0.274 -1.771 -1.672 -0.302 ...
```

```r
# Here we calculate the sample mean for each X_i (column)
samp.means <- colMeans(samp.mat)
str(samp.means)
```

```
##  num [1:1000] -0.04924 -0.00536 0.19048 -0.1071 -0.08355 ...
```

```r
hist(samp.means)
```

<img src="05_random-variables_files/figure-html/unnamed-chunk-1-1.png" width="672" />

2a. What happens if we change `samp.size` (i.e., $n$)? 


```r
n_vector <- c(1, 5, 20, 50, 100, 1000)
samp_means_mat <- matrix(data = NA, nrow = n.samps, ncol = length(n_vector))

calculate_sample_means <- function(samp.size = 20, n.samps = 1000){
  samps <- rnorm(samp.size * n.samps, mean = 0, sd = 1)
  samp.mat <- matrix(samps, ncol = n.samps) 
  samp.means <- colMeans(samp.mat)
  return(samp.means)
}

par(mfrow = c(2,3))
set.seed(21)
for(i in 1:length(n_vector)){
  samp_size_i <- n_vector[i]
  samp_means_i <- calculate_sample_means(samp.size = samp_size_i)
  hist(samp_means_i, xlim = c(-3, 3), ylim = c(0, 250), 
       xlab = "Sample mean", 
       main = paste("n = ", samp_size_i, sep = ""), col = "red")
}
```

<img src="05_random-variables_files/figure-html/unnamed-chunk-2-1.png" width="672" />

2b. Using the exponential distribution. 


```r
n_vector <- c(1, 5, 20, 50, 100, 1000)
samp_means_mat <- matrix(data = NA, nrow = n.samps, ncol = length(n_vector))

calculate_sample_means_exp <- function(samp.size = 20, n.samps = 1000){
  samps <- rexp(samp.size * n.samps, rate = 1)
  samp.mat <- matrix(samps, ncol = n.samps) 
  samp.means <- colMeans(samp.mat)
  return(samp.means)
}

par(mfrow = c(2,3))
set.seed(21)
for(i in 1:length(n_vector)){
  samp_size_i <- n_vector[i]
  samp_means_i <- calculate_sample_means_exp(samp.size = samp_size_i)
  hist(samp_means_i, 
       xlab = "Sample mean", 
       main = paste("n = ", samp_size_i, sep = ""), col = "red")
}
```

<img src="05_random-variables_files/figure-html/unnamed-chunk-3-1.png" width="672" />

## Variance and standard deviation

The variance is a measurement of dispersal - i.e., how spread out is the distribution? And spread out from what, exactly? It is useful to think about the distance $X_i$ takes from the expectation, E$(X)$: $X - \text{E}(X)$. What if we took the expectation of this - i.e., the average value of the distance from the mean?

$$ 
\begin{aligned}
\text{E}(X - \text{E}(X)) \\
\text{by linearity of expectation, we get:} \\
\text{E}(X) - \text{E}(\text{E}(X)) \\
\text{E}(X) - \text{E}(X) \\
0
\end{aligned}
$$

This won't work - we need to find a way to constrain the expression inside the parentheses to be non-negative. One way to do this is to use the mean absolute deviation, $|X - \text{E}(X)|$. Another way is to use the mean squared deviation, $[X - \text{E}(X)]^2$. The squared term constrains the variance to be $\ge 0$:  

$$ 
\begin{aligned}
\text{Var}(X) =& \text{E}([X - \text{E}(X)]^2) \\
\end{aligned}
$$

The mean squared deviation has two mathematical advantages:

1. It is easier to compute mathematically than an analogous quanitity using absolute deviations (but why?)

2. The variances of linear functions of random variables are 'beautifully behaved', whereas the analogous quantities for absolute deviations can be a hassle. 

I will just take Edge's word on these two points for now. 

### Beautiful properties of the variance

The variance can be rewritten as:

$$ 
\begin{aligned}
\text{Var}(X) = \text{E}(X^2) - [\text{E}(X)]^2 \\
\end{aligned}
$$

which is generally easier to compute. 

Adding a constant to a random variable does *not* affect the variance:

$$ 
\begin{aligned}
\text{Var}(a + cX) = c^2\text{Var}(X) \\
\end{aligned}
$$
where $a$ and $c$ are constants. 

If $X$ and $Y$ are independent random variables, then: 

$$ 
\begin{aligned}
\text{Var}(X + Y) = \text{Var}(X) + \text{Var}(Y) \\
\end{aligned}
$$

One big problem with the variance is that is in the wrong ($X^2$) units. To fix this, we calculate the *standard deviation*: 

$$ 
\begin{aligned}
\text{SD}(X) = \sqrt{\text{Var}(X)} \\
\end{aligned}
$$

SD is usually larger (never smaller) than MAD, and is more sensitive to large deviations. 

### Exercise set 5-2

I had to walk through Edge's solutions bit by bit; my handwritten version is [here](images/edge_4_1_3.pdf). 

## Joint distributions, covariance, and correlation

This section covers four key concepts:

1. Joint probability distribution: the probability distribution of the joint occurrence of $X$ and $Y$

2. Marginal distribution of X: the probability distribution of $X$, summing (integrating) over all values of $Y$

3. Covariance: a measurement of the extent to which $X$ and $Y$ depart from independence

4. Correlation: covariance rescaled to go from -1 to 1

### Joint probability distributions

Joint probability distribution: the probability distribution of the joint occurrence of $X$ and $Y$

The joint cumulative probability distribution of two random variables $X$ and $Y$ is given by:

$$
\begin{aligned}
F_{X,Y}(x, y) = \text{P} (X \leq x ~\cap ~ Y \leq y)
\end{aligned}
$$

Here is the corresponding joint probability mass function:

$$
\begin{aligned}
f_{X,Y}(x, y) = \text{P} (X = x ~\cap ~ Y = y)
\end{aligned}
$$

And for two continuous variables, we can recover the cumulative distribution function by integrating the probability density function with respect to $X$ and $Y$:

$$
\begin{aligned}
F_{X,Y}(x, y) =& ~ \text{P}(X \leq x ~\cap ~ Y \leq y) \\
=& \int_{- \infty}^{x} \int_{- \infty}^{y} f_{X,Y}(x, y) dx dy
\end{aligned}
$$

### Marginal distributions

Marginal distribution of X: the probability distribution of $X$, summing (integrating) over all values of $Y$

For discrete random variables, the marginal distribution of $X$ is:

$$
\begin{aligned}
f_{X}(x) =& ~ \text{P} (X = x) \\
         =& ~ \sum_{y} \text{P} (X = x ~\cap ~ Y = y) \\
         =& \sum_{y} f_{X,Y}(x,y)
\end{aligned}
$$

For continuous random variables, the marginal distribution of $X$ is:

$$
\begin{aligned}
f_{X}(x) =& \int_{- \infty}^{\infty} f_{X,Y}(x, y) dy
\end{aligned}
$$

### Covariance

Covariance is a measurement of the extent to which $X$ and $Y$ depart from independence

Such a measure should have two basic properties:

  - The number should be positive when $X$ and $Y$ increase or decrease together
  - The number should be negative when $X$ increases and $Y$ decreases (and vice versa).

Consider the random variable $[X - \text{E}(X)][Y - \text{E}(Y)]$. If we sample a joint probability distribution, resulting in a set ($\Omega$) of pairs of $(x, y)$, ask yourself:

  - Is the sign positive or negative when most of the pairs $(x, y)$ are such that $x > \text{E}(X)$ and $y > \text{E}(Y)$?
  - Is the sign positive or negative when most of the pairs $(x, y)$ are such that $x < \text{E}(X)$ and $y < \text{E}(Y)$?
  - Is the sign positive or negative when most of the pairs $(x, y)$ are such that $x > \text{E}(X)$ and $y < \text{E}(Y)$?
  - Is the sign positive or negative when most of the pairs $(x, y)$ are such that $x < \text{E}(X)$ and $y > \text{E}(Y)$?

Hopefully, you have convinced yourself that the random variable $[X - \text{E}(X)][Y - \text{E}(Y)]$ satisfies the two aforementioned properties. Now we take the expectation of this random variable to arrive at the covariance.

Conveniently (or purposefully?), the covariance is an extension of the variance:

$$
\begin{aligned}
\text{Cov}(X,Y) =& ~ \text{E}([X - \text{E}(X)][Y - \text{E}(Y)]) \\
                =& ~ \text{E}(XY) - \text{E}(X)\text{E}(Y)
\end{aligned}
$$

If you replace $\text{E}(Y)$ with $\text{E}(X)$ in the above equation, you should recover the definition of Var$(X)$, $\text{E}(X^2) - [\text{E}(X)]^2$.

If $X$ and $Y$ are independent, then $\text{Cov}(X,Y) = 0$ (we showed this in an earlier problem set).

However, if $\text{Cov}(X,Y) = 0$, that does not necessarily imply that $X$ and $Y$ are independent.

### Correlation

Correlation: covariance rescaled to go from -1 to 1

The covariance is not a pure measure of the linear dependence between two variables, because it is sensitive to the scaling of the variables. Therefore, we cannot use the covariance to compare the strengths of different bivariate relationships. In other words, we cannot use the covariance to answer the question: *Is the relationship between cereal yield and fertilizer consumption stronger than the relationship between career earnings and college GPA?*. Instead, we calculate the correlation:


$$
\begin{aligned}
\text{Cor}(X,Y) =& ~ \rho_{X,Y} \\
                =& ~ \frac{\text{Cov}(X,Y)}{\sqrt{\text{Var}(X)\text{Var}(Y)}} \\
                =& ~ \frac{\text{Cov}(X,Y)}{\sigma_X \sigma_Y}\\
\end{aligned}
$$

You can prove to yourself that the correlation is bounded from -1 to 1 using a simple heuristic. Which variable should be the most correlated with $X$? Well, that would be $X$. Plugging in $X$ for $Y$, we get:

$$
\begin{aligned}
\text{Cor}(X,X) =& ~ \frac{\text{Cov}(X,X)}{\sigma_X \sigma_X} \\
                 =& ~ \frac{\text{Var}(X)}{\text{Var}(X)} \\
                 =& ~ 1
\end{aligned}
$$

Using the same logic, $-X$, is the least correlated with $X$. Try working through the algebra, you should get -1:

$$
\begin{aligned}
\text{Cor}(X,-X) =& ~ \frac{\text{Cov}(X,-X)}{\sqrt{\text{Var}(X)\text{Var}(-X)}} \\
                =& ~ \frac{\text{E}(X \times -X) - \text{E}(X)\text{E}(-X)}{\sqrt{\text{Var}(X)\text{Var}(-X)}} \\
\end{aligned}
$$

### Additional exercise

I will add one problem, to reinforce the concepts of joint and marginal distributions, with two discrete random variables. This problem covers similar ideas to Edge's first exercise in set 5-3.

You watched 100 female birds last spring, and recorded the number of offspring per bird (X; 1, 2, or 3 chicks). You also recorded the age of each mom (Y; 1, 2, or 3 years).

You observed:
10 1-yr olds, all with one chick.
27 2-yr olds; 13 had one chick, 12 had two chicks, and 2 had three chicks.
63 3-yr olds; 23 had one chick, 36 had two chicks, and 4 had three chicks.

Calculate:

1. The probability of observing each possible outcome (e.g., a 1-yr old bird has 1 chick; a 1-yr old bird has 2 chicks; etc.).

2. The probability of observing a 1-yr old bird; a 2-yr old bird; and a 3-yr old bird.

3. The probability of observing 1 chick per mom; 2 chicks per mom; 3 chicks per mom.

STOP! NO PEEKING ! ANSWER IS BELOW:

Wait for it...

...wait for it ...

...here it is: an excel (gasp!) plot!

![](images/birbs_for_rmd.png){width=200%}

The key here is to recognize that yellow represents the joint probabilities of X and Y; the green and blue represents the marginal probabilities of X and Y, respectively. Stare at this until it clicks. A similar principle applies to continuous distributions, but rather than summing across Y, we integrate across Y to get the marginal distribution of X.

### Exercise set 5-3

I had to walk through Edge's solutions bit by bit; my handwritten version is [here](images/edge_5_3.pdf).

## Conditional distribution, expectation, variance

For two discrete random variables, the conditional probability mass function is:

$$
\begin{aligned}
f_{X|Y}(x |Y = y) =& \text{P}(X = x | Y = y) \\
                  =& \frac{\text{P} (X = x ~\cap ~ Y = y)}{\text{P}(Y = y)} \\
                  =& \frac{f_{X,Y}(x,y)}{f_{Y}(y)}
\end{aligned}
$$

For two continuous random variables, the conditional probability density function is defined similarly:

$$
\begin{aligned}
f_{X|Y}(x |Y = y) =& \frac{f_{X,Y}(x,y)}{f_{Y}(y)}
\end{aligned}
$$

Edge has a nice visualization and explanation of conditional distribution in his Fig 5-5.

## The central limit theorem

Natural populations are large, so we usually gather just a sample and use that as a surrogate for the whole population. If we take $n$ samples, then another $n$ samples, and then another $n$ samples, and calculate $\overline{X}_1$, $\overline{X}_2$, and $\overline{X}_3$, differences in our estimate of $\overline{X}$ are due to sampling variation. The weak law of large numbers (above) tells us that as $n$ approaches $\infty$, our estimate of $\overline{X}_n$ approaches the true population mean, $\mu$, and that the Var($\overline{X}_n$) = $\sigma^2 / n$, approaches 0.

But what is the *shape* of this distribution? That is where the central limit theorem (CLT) comes in. As $n$ approaches $\infty$, the distribution of $\overline{X}_n$ converges to a normal distribution with expectation $\mu$ and variance $\sigma^2 / n$.

An importance consequence of the CLT is the surpising result that the distribution of sample means $\overline{X}_n$ is *approximately* normal even when the distribution of the individual observations are not normally distributed! The implications of the CLT are huge: it allows us to use the normal distribution (and the powerful set of analytical tools that depend on it) in real-world situations where the underlying data are not normally distributed, as long as we have enough samples. What is enough? A general rule of thumb is 30, but will vary with the underlying probability distribution of the population. You will explore this using simulations in the problem set below.

### Exercise set 5-4

1. Bean machine in action!


```r
library(animation)
nball <- 500 #change the number of balls
nlayer <- 10 #change the number of rows of pegs on the board
rate <- 10 #change the speed at which the balls fall
ani.options(nmax = nball + nlayer - 2, interval = 1/rate)
quincunx(balls = nball, layers = nlayer)
```

2. Exploring the beta distribution

To see what the beta distribution looks like for a given set of shape parameters, set the sample size to 1. For example:


```r
library(stfspack)
# dosm.beta.hist(n = 1, nsim = 10000, shape1 = 1, shape2 = 1)
```

will give you a histogram of 10,000 observations from a beta distribution with parameters 1 and 1. If you increase the sample size, then the distribution of the sample mean gets closer to normality. Try this — starting with samples of size 1 and increasing the sample size — with the following sets of parameter values: (1, 1), (0.2, 0.2), (2, 0.5), (0.5, 2), (3, 3). Feel free to try other parameter sets — it’s fun. What do you notice?


```r
sims <- 1000
s1 <- 0.2 # change this
s2 <- 0.2 # change this
par(mfrow = c(2,3))
dosm.beta.hist(n = 1, nsim = sims, shape1 = s1, shape2 = s2)
```

```
## mean of DOSM   SD of DOSM  var of DOSM 
##    0.4976551    0.4193736    0.1758742
```

```r
dosm.beta.hist(n = 4, nsim = sims, shape1 = s1, shape2 = s2)
```

```
## mean of DOSM   SD of DOSM  var of DOSM 
##   0.51873441   0.21324943   0.04547532
```

```r
dosm.beta.hist(n = 8, nsim = sims, shape1 = s1, shape2 = s2)
```

```
## mean of DOSM   SD of DOSM  var of DOSM 
##   0.50331631   0.14985449   0.02245637
```

```r
dosm.beta.hist(n = 16, nsim = sims, shape1 = s1, shape2 = s2)
```

```
## mean of DOSM   SD of DOSM  var of DOSM 
##   0.49738079   0.10502289   0.01102981
```

```r
dosm.beta.hist(n = 32, nsim = sims, shape1 = s1, shape2 = s2)
```

```
## mean of DOSM   SD of DOSM  var of DOSM 
##  0.500954728  0.075780685  0.005742712
```

```r
dosm.beta.hist(n = 64, nsim = sims, shape1 = s1, shape2 = s2)
```

<img src="05_random-variables_files/figure-html/unnamed-chunk-6-1.png" width="672" />

```
## mean of DOSM   SD of DOSM  var of DOSM 
##  0.500007026  0.053298265  0.002840705
```

Let's deconstruct what is going on with this function, where n = 1 (we simulate 10000 observations from a single set of parameter values).


```r
dosm.beta.hist
```

```
## function (n, nsim, shape1 = 1, shape2 = 1, ...) 
## {
##     samps <- rbeta(n * nsim, shape1, shape2)
##     sim.mat <- matrix(samps, nrow = nsim)
##     dosm <- rowMeans(sim.mat)
##     hist(dosm, freq = FALSE, ...)
##     x <- seq(0, 1, length.out = 1000)
##     lines(x, dnorm(x, mean = mean(dosm), sd = sd(dosm)))
##     c(`mean of DOSM` = mean(dosm), `SD of DOSM` = sd(dosm), `var of DOSM` = var(dosm))
## }
## <bytecode: 0x7feef1daee80>
## <environment: namespace:stfspack>
```

```r
nsim <- 10000
n <- 1
s1 <- 0.2 # change this
s2 <- 0.2 # change this
samps <- rbeta(n * nsim, shape1 = s1, shape2 = s2)
str(samps) # here are 10,000 samples
```

```
##  num [1:10000] 0.13472 0.70805 0.99361 0.00268 0.58459 ...
```

```r
# We are converting the vector into a matrix
# So that we can easily calculate the mean of each row
sim.mat <- matrix(samps, nrow = nsim)
dim(sim.mat); head(sim.mat)
```

```
## [1] 10000     1
```

```
##            [,1]
## [1,] 0.13471512
## [2,] 0.70804823
## [3,] 0.99361002
## [4,] 0.00268066
## [5,] 0.58459079
## [6,] 0.99641568
```

```r
# Calculate rowmeans - with n=1, this doesn't change anything
# But change n to anything bigger and inspect the dimensions of the objects
dosm <- rowMeans(sim.mat)
str(dosm) # compare these values to sim.mat
```

```
##  num [1:10000] 0.13472 0.70805 0.99361 0.00268 0.58459 ...
```

```r
par(mfrow = c(1,1))
hist(dosm, freq = FALSE) # plotting the simulated values

# Set up a vector that goes from 0 to 1 to overlay a normal distribution on the histogram
x <- seq(0, 1, length.out = 1000)

# Now plot a normal distribution, using the mean and sd of the simulated values
lines(x, dnorm(x, mean = mean(dosm), sd = sd(dosm)), col = "red")
```

<img src="05_random-variables_files/figure-html/unnamed-chunk-7-1.png" width="672" />

3. The Pareto distribution is a skewed, heavy-tailed, power-law distribution used in description of social, scientific, geophysical, actuarial, and many other types of observable phenomena. It was applied originally to the distribution of wealth in a society, fitting the observation that a large portion of wealth is held by a small fraction of the population. Named after the Italian civil engineer, economist, and sociologist Vilfredo Pareto.

Parameters of the `rpareto` function:

  - a: shape (on the web as $\alpha$)
  - b: scale (on the web as $x_m$)

If the shape parameter is $\leq$ 1, $E(X)$ is $\infty$.
If the shape parameter is $\leq$ 2, $Var(X)$ is $\infty$.

First we simulate many sampes of size 1000 from a Pareto distribution with shape = 4.


```r
# experiment with n and the parameters a and b
n <- 100
n_sims <- 10000
a <- 1
b <- 4

x <- rpareto(n = n, a = a, b = b)
summary(x)
```

```
##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
##   4.076   6.120   9.899  29.924  20.622 928.145
```

```r
# Calculate mean and sd
mu <- mean(x)
stdev <- sd(x)

hist(x, freq = FALSE)
# Set up a vector that goes from 0 to 1 to overlay a normal distribution on the histogram
x_vals <- seq(min(x), max(x), length.out = 1000)
# Now plot a normal distribution, using the mean and sd of the simulated values
lines(x_vals, dnorm(x_vals, mean = mu, sd = stdev), col = "red")
```

<img src="05_random-variables_files/figure-html/unnamed-chunk-8-1.png" width="672" />


```r
# Compare tail to normal
compare.tail.to.normal
```

```
## function (x, k, mu, sigma) 
## {
##     mean(x < (mu - k * sigma) | x > (mu + k * sigma))/(1 - (pnorm(k) - 
##         pnorm(-k)))
## }
## <bytecode: 0x7feef06dde98>
## <environment: namespace:stfspack>
```

```r
k <- 2 # sds
compare.tail.to.normal(x = x, k = k, mu = mu, sigma = stdev)
```

```
## [1] 0.2197789
```

```r
summary(x)
```

```
##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
##   4.076   6.120   9.899  29.924  20.622 928.145
```

```r
mu
```

```
## [1] 29.92446
```

```r
stdev
```

```
## [1] 95.49789
```

```r
# This gives the value of the mean, minus the value k*stdev
# (i.e., an extreme negative value)
# Below I will use my object stdev in place of sigma (the parameter from Edge's function)
(mu - k * stdev)
```

```
## [1] -161.0713
```

```r
# Extreme positive value
(mu + k * stdev)
```

```
## [1] 220.9202
```

```r
# This statement asks whether the value in x is an extreme value
# The operator '|' is 'OR'
# Is x extreme negative OR extreme positive?
x < (mu - k * stdev) | x > (mu + k * stdev)
```

```
##   [1] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [13] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [25] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [37] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [49] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [61] FALSE FALSE FALSE FALSE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [73] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [85] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
##  [97] FALSE FALSE FALSE FALSE
```

```r
# We can get the frequencies of this logical vector using table
table(x < (mu - k * stdev) | x > (mu + k * stdev))
```

```
## 
## FALSE  TRUE 
##    99     1
```

```r
# Or, as Edge, does, calculate the average of TRUEs - which is simply the proportion of TRUEs
mean(x < (mu - k * stdev) | x > (mu + k * stdev))
```

```
## [1] 0.01
```

```r
# What proportion/probability of TRUEs would we expect under a normal probability distribution?
pnorm(k) # probability of observing a value less than k standard deviations above the mean
```

```
## [1] 0.9772499
```

```r
pnorm(-k) # probability of observing a value less than k standard deviations below the mean
```

```
## [1] 0.02275013
```

```r
(1 - (pnorm(k) - pnorm(-k))) # probability of observing an extreme value
```

```
## [1] 0.04550026
```

```r
# So putting it all together, we have the ratio of:
# the probability of observing an extreme value in the data, over the
# the probability of observing an extreme value in a normal distribution:
mean(x < (mu - k * stdev) | x > (mu + k * stdev))/(1 - (pnorm(k) - pnorm(-k)))
```

```
## [1] 0.2197789
```

```r
compare.tail.to.normal(x = x, k = k, mu = mu, sigma = stdev)
```

```
## [1] 0.2197789
```

```r
# If this ratio is < 1, then the data have fewer extreme values than suggested by a normal
# If this ratio is > 1, then the data have more extreme values than suggested by a normal
```

Above, I haven't computed the means of many simulations - which is the crux of the question! So here I just paste Edge's solution. In it, he calculates $E(X)$ and $Var(X)$ using the Pareto probability distribution. I have changed `n` and `n.sim` to match my values above.


```r
#Sample size per simulation (n) and number of simulations.
n <- 100
n.sim <- 10000
#Pareto parameters. Variance is finite, and so
#CLT applies, if a > 2. For large a, convergence to
#normal is better. With small a, convergence is slow,
#especially in the tails.
a <- 4
b <- 1
#Compute the expectation and variance of the distribution
#of the sample mean. a must be above 2 for these expressions
#to hold.
expec.par <- a*b/(a-1)
var.par <- a*b^2 / ((a-1)^2 * (a-2))
sd.mean <- sqrt(var.par / n)
#Simulate data
sim <- matrix(rpareto(n*n.sim, a, b), nrow = n.sim)
# Each column represents ith sample taken per simulation
# Each row represents a different simulation
sim[1:3, 1:10]
```

```
##          [,1]     [,2]     [,3]     [,4]     [,5]     [,6]     [,7]     [,8]
## [1,] 1.146496 1.029705 1.334946 1.060409 1.013868 1.038984 1.804409 1.299151
## [2,] 1.342433 1.205436 1.003869 3.416952 2.248103 1.023516 1.006624 1.044363
## [3,] 1.076866 1.027499 1.061844 1.071026 1.425200 1.069973 1.456830 1.757125
##          [,9]    [,10]
## [1,] 1.153548 1.276303
## [2,] 1.074918 1.304583
## [3,] 1.042708 1.099849
```

```r
# Compute sample means.
means.sim <- rowMeans(sim)
str(means.sim)
```

```
##  num [1:10000] 1.38 1.34 1.33 1.28 1.34 ...
```

```r
#Draw a histogram of the sample means along with the approximate
#normal pdf that follows from the CLT.
hist(means.sim, prob = TRUE)
curve(dnorm(x, expec.par, sd.mean), add = TRUE, col = 'red')
```

<img src="05_random-variables_files/figure-html/unnamed-chunk-10-1.png" width="672" />

```r
compare.tail.to.normal(means.sim, 1/2, expec.par, sd.mean)
```

```
## [1] 0.9639022
```

```r
compare.tail.to.normal(means.sim, 1, expec.par, sd.mean)
```

```
## [1] 0.9407189
```

```r
compare.tail.to.normal(means.sim, 2, expec.par, sd.mean)
```

```
## [1] 0.9384561
```

```r
compare.tail.to.normal(means.sim, 3, expec.par, sd.mean)
```

```
## [1] 2.18535
```

```r
compare.tail.to.normal(means.sim, 4, expec.par, sd.mean)
```

```
## [1] 25.25951
```

```r
compare.tail.to.normal(means.sim, 5, expec.par, sd.mean)
```

```
## [1] 348.8556
```

```r
compare.tail.to.normal(means.sim, 6, expec.par, sd.mean)
```

```
## [1] 0
```


## A probabilistic model for simple linear regression

In this last section, we are going to apply the probabilistic concepts to our linear function:

$$
\begin{aligned}
Y = \alpha + \beta X + \epsilon \\
\end{aligned}
$$

$X, Y, \epsilon$: random variables (probability distributions)  

$\alpha, \beta$: fixed coefficients (scalars)

In words, we are trying to model $Y$ as a linear function of $\alpha, \beta, X$, plus a random disturbance, $\epsilon$. 

In what follows, we are going to make some simplifying assumptions about the random variables $X$ and $\epsilon$.

Why?

Because in doing so, we can make some *claims* about $Y$ - its expectation, and variance; as well as Cov($X, Y$).   

Why is it useful to make these claims? 

Because in doing so, we will be able to decompose the variance of $Y$ into two components: the effect of $X$ on $Y$, and the disturbance $\epsilon$. That is, we'll be able to generate predictions for $Y$ given $X$ - maybe we can predict $Y$ really well, or maybe not. 

I will briefly restate the assumptions below. 

### Assumptions of the linear model

1. $X$ has a known expectation, and the disturbance term has an expectation of 0: 

$$
\begin{aligned}
\text{E}(X) =& ~ \mu_X \\
\text{E}(\epsilon) =& ~ 0 \\
\end{aligned}
$$

*Consequence: we know the expectation of $Y$*

2. The expectation of the disturbance term is 0 for *all* values of $X$:

$$
\begin{aligned}
\text{E}(\epsilon | X = x) =& ~ 0 \\
\end{aligned}
$$
*Consequence: the conditional expectation of $Y$, given any $x$, can be predicted using a line with a slope $\beta$ and intercept $\alpha$. Let that sink in...if this is not true, then the relationship between X and Y is not linear!*

3. The variance of the disturbance is constant, for every $x$: 

$$
\begin{aligned}
\text{Var}(\epsilon | X = x) =& ~ \sigma^2_\epsilon \\
\end{aligned}
$$

*Consequence: the variance of Y, for any x, is constant*

4. $X$ and $\epsilon$ are independent. 

*Consequence: the variance of Y is due to the variation in X, plus the variation due to the disturbance*

### Important claims that follow from these assumptions

The correlation between $X$ and $Y$ is: 

$$
\begin{aligned}
\rho_{X, Y} = \beta \frac{\sigma_X}{\sigma_Y}\\
\end{aligned}
$$

The proportion of variance in $Y$ that is explained by $X$ ($r^2$) is: 

$$
\begin{aligned}
\rho_{X, Y}^2 = 1 - \frac{\text{Var}(Y|X = x)}{\text{Var}(Y)}\\
\end{aligned}
$$

### Checking these assumptions

So you have run a linear model in R using `lm()`. Now what? Check your assumptions, of course! The most important assumptions are *linearity* (# 2 above) and *homoscedasticity* (#3 above). To check these, plot the residuals of your model against the fitted values. 


```r
plot(y1 ~ x1, data = anscombe)
```

<img src="05_random-variables_files/figure-html/unnamed-chunk-11-1.png" width="672" />

```r
lm1 <- lm(y1 ~ x1, data = anscombe)
plot(lm1, which = 1)
```

<img src="05_random-variables_files/figure-html/unnamed-chunk-11-2.png" width="672" />

There should be no trend in the residuals (indicative of *linearity*), and the scatter of the residuals should be consistent across the range of fitted values (indicative of *homoscedasticity*). In the plot above, both of these assumptions are satisfied. Hopefully your residuals will look like this (if not, you have more work to do!). 

Here is a figure (7.5) from Faraway (2002) that illustrates clear violations of these two assumptions: 

![](images/Faraway_fig7.5.png){width=150%}


### Exercise set 5-5

1. Write the square of the correlation coefficient (eq. 5.30) in terms of the variance of Y (eq. 5.32) and the conditional variance of Y given X (eq. 5.31).

$$
\begin{aligned}
\text{eq. 5.30: } \rho_{X,Y} =& \beta \frac{\sigma_X}{\sigma_Y} \\
\text{eq. 5.31: } Var(Y) =& \beta^2 \sigma_X^2 + \sigma_{\epsilon}^2 \\
\text{eq. 5.32: } Var(Y \mid X = x) =& \sigma_{\epsilon}^2  \\
\end{aligned}
$$

Squaring $\rho_{X,Y}$, and expressing $Var(Y)$ using the definition from above:

$$
\begin{aligned}
\rho_{X,Y}^2 = \beta^2 \frac{\sigma_X^2}{\sigma_Y^2} = \beta^2 \frac{\sigma_X^2}{Var(Y)} \\
\end{aligned}
$$

$$
\begin{aligned}
\rho_{X,Y}^2 =  \beta^2 \frac{\sigma_X^2}{\beta^2 \sigma_X^2 + \sigma_{\epsilon}^2} \\
\end{aligned}
$$

Now, we have to employ an algebraic slight of hand. We rewrite the terms on the right as a single fraction, and by adding and subtracting the term $\sigma_{\epsilon}^2$ to the numerator, the numerator remains unchanged, but in a useful form to separate the single fraction into two, with the lefthand fraction equaling 1:

$$
\begin{aligned}
\rho_{X,Y}^2 =& \frac{\beta^2 \sigma_X^2}{\beta^2 \sigma_X^2 + \sigma_{\epsilon}^2} \\
=& \frac{(\beta^2 \sigma_X^2 + \sigma_{\epsilon}^2) - \sigma_{\epsilon}^2}{\beta^2 \sigma_X^2 + \sigma_{\epsilon}^2} \\
=& \frac{\beta^2 \sigma_X^2 + \sigma_{\epsilon}^2}{\beta^2 \sigma_X^2 + \sigma_{\epsilon}^2} - \frac{\sigma_{\epsilon}^2}{\beta^2 \sigma_X^2 + \sigma_{\epsilon}^2} \\
=& 1 - \frac{\sigma_{\epsilon}^2}{\beta^2 \sigma_X^2 + \sigma_{\epsilon}^2} \\
\end{aligned}
$$

And we use the formulas from above again to restate as:

$$
\begin{aligned}
\rho_{X,Y}^2 =& 1 - \frac{Var(Y \mid X = x)}{Var(Y)} \\
\end{aligned}
$$

which gives us the 'proportion of variance explained'. So if there isn't much variance left in $Y$ after conditioning on $X$ (i.e., the numerator is small relative to the denominator), if we subtract it from 1, we get a high $r^2$. And vice versa.

2. Simulating a regression.


```r
library(stfspack)
sim.lm
```

```
## function (n, a, b, sigma.disturb = 1, mu.x = 8, sigma.x = 2, 
##     rdisturb = rnorm, rx = rnorm, het.coef = 0) 
## {
##     x <- sort(rx(n, mu.x, sigma.x))
##     disturbs <- rdisturb(n, 0, sapply(sigma.disturb + scale(x) * 
##         het.coef, max, 0))
##     y <- a + b * x + disturbs
##     cbind(x, y)
## }
## <bytecode: 0x7feef5544aa8>
## <environment: namespace:stfspack>
```

```r
sim_0_1 <- sim.lm(n = 50, a = 0, b = 1)
head(sim_0_1)
```

```
##             x        y
## [1,] 3.427344 2.949380
## [2,] 3.616894 3.644965
## [3,] 3.815677 4.193751
## [4,] 3.912910 3.364430
## [5,] 4.458928 6.025582
## [6,] 5.078764 3.985045
```

```r
plot(sim_0_1[,1], sim_0_1[,2])
```

<img src="05_random-variables_files/figure-html/unnamed-chunk-12-1.png" width="672" />

Still using all the default values for parameters, but I have made all the arguments explicit in the function call:


```r
sim_0_1 <- sim.lm(n = 50, a = 0, b = 1,
                  sigma.disturb = 1, mu.x = 8, sigma.x = 2,
                  rdisturb = rnorm, rx = rnorm, het.coef = 0)
plot(sim_0_1[,1], sim_0_1[,2])
```

<img src="05_random-variables_files/figure-html/unnamed-chunk-13-1.png" width="672" />

Now I'll change one at a time. Here, I've doubled `sigma.disturb`, the error term:


```r
sim_0_1 <- sim.lm(n = 50, a = 0, b = 1,
                  sigma.disturb = 2, mu.x = 8, sigma.x = 2,
                  rdisturb = rnorm, rx = rnorm, het.coef = 0)
plot(sim_0_1[,1], sim_0_1[,2])
```

<img src="05_random-variables_files/figure-html/unnamed-chunk-14-1.png" width="672" />

Next, I have doubled E($X$): 


```r
sim_0_1 <- sim.lm(n = 50, a = 0, b = 1,
                  sigma.disturb = 1, mu.x = 16, sigma.x = 2,
                  rdisturb = rnorm, rx = rnorm, het.coef = 0)
plot(sim_0_1[,1], sim_0_1[,2])
```

<img src="05_random-variables_files/figure-html/unnamed-chunk-15-1.png" width="672" />

Next, I have doubled $\sigma_X$:


```r
sim_0_1 <- sim.lm(n = 50, a = 0, b = 1,
                  sigma.disturb = 1, mu.x = 8, sigma.x = 4,
                  rdisturb = rnorm, rx = rnorm, het.coef = 0)
plot(sim_0_1[,1], sim_0_1[,2])
```

<img src="05_random-variables_files/figure-html/unnamed-chunk-16-1.png" width="672" />

Finally, here I have changed the distribution of the error term to a laplace distribution:


```r
sim_0_1 <- sim.lm(n = 50, a = 0, b = 1,
                  sigma.disturb = 1, mu.x = 8, sigma.x = 2,
                  rdisturb = rlaplace, rx = rnorm, het.coef = 0)
plot(sim_0_1[,1], sim_0_1[,2])
```

<img src="05_random-variables_files/figure-html/unnamed-chunk-17-1.png" width="672" />
