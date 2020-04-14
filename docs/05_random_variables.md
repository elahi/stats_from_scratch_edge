---
output: html_document
editor_options: 
  chunk_output_type: console
---



# Properties of random variables {#randomvars}


```r
library(tidyverse)
theme_set(theme_bw(base_size = 12) + 
            theme(strip.background = element_blank(), 
                  panel.grid = element_blank())) 
```

## Expected values and the law of large numbers

### Exercise set 5-1

1. On paper

2.


```r
samp.size <- 1
n.samps <- 1000
samps <- rnorm(samp.size * n.samps, mean = 0, sd = 1)
samp.mat <- matrix(samps, ncol = n.samps)
samp.means <- colMeans(samp.mat)
hist(samp.means)
```

<img src="05_random_variables_files/figure-html/unnamed-chunk-1-1.png" width="672" />



```r
samp.size <- 100
n.samps <- 1000
samps <-matrix(rexp(samp.size*n.samps, rate = 1), ncol = n.samps)
samp.means <- colMeans(samps)
hist(samp.means)
```

<img src="05_random_variables_files/figure-html/unnamed-chunk-2-1.png" width="672" />

## Variance and standard deviation

## Joint distributions, covariance, and correlation

## Conditional distribution, expectation, variance

## The central limit theorem

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
## <bytecode: 0x7fa3d5e854a0>
## <environment: namespace:stfspack>
```

will give you a histogram of 10,000 observations from a beta distribution with parameters 1 and 1. If you increase the sample size, then the distribution of the sample mean gets closer to normality. Try this — starting with samples of size 1 and increasing the sample size—with the following sets of parameter values: (1, 1), (0.2, 0.2), (2, 0.5), (0.5, 2), (3, 3). Feel free to try other parameter sets—it’s fun. What do you notice?


```r
sims <- 10000
s1 <- 0.2 # change this
s2 <- 0.2 # change this
par(mfrow = c(2,3))
dosm.beta.hist(n = 1, nsim = sims, shape1 = s1, shape2 = s2)
```

```
## mean of DOSM   SD of DOSM  var of DOSM 
##    0.4990109    0.4228197    0.1787765
```

```r
dosm.beta.hist(n = 8, nsim = sims, shape1 = s1, shape2 = s2)
```

```
## mean of DOSM   SD of DOSM  var of DOSM 
##    0.4995383    0.1503004    0.0225902
```

```r
dosm.beta.hist(n = 16, nsim = sims, shape1 = s1, shape2 = s2)
```

```
## mean of DOSM   SD of DOSM  var of DOSM 
##   0.50007775   0.10551245   0.01113288
```

```r
dosm.beta.hist(n = 32, nsim = sims, shape1 = s1, shape2 = s2)
```

```
## mean of DOSM   SD of DOSM  var of DOSM 
##  0.501064679  0.074632731  0.005570045
```

```r
dosm.beta.hist(n = 64, nsim = sims, shape1 = s1, shape2 = s2)
```

```
## mean of DOSM   SD of DOSM  var of DOSM 
##   0.49972645   0.05220469   0.00272533
```

```r
dosm.beta.hist(n = 128, nsim = sims, shape1 = s1, shape2 = s2)
```

<img src="05_random_variables_files/figure-html/unnamed-chunk-5-1.png" width="672" />

```
## mean of DOSM   SD of DOSM  var of DOSM 
##  0.500424795  0.037352264  0.001395192
```

Let's deconstruct what is going on with this function, where n = 1 (we simulate 10000 observations from a single set of parameter values). 


```r
nsim <- 10000
n <- 1
s1 <- 0.2 # change this
s2 <- 0.2 # change this
samps <- rbeta(n * nsim, shape1 = s1, shape2 = s2)
str(samps) # here are 10,000
```

```
##  num [1:10000] 0.26 0.99 0.916 0.231 0.767 ...
```

```r
# We are just converting the vector into a matrix
# So that we can easily calculate the mean of each row
sim.mat <- matrix(samps, nrow = nsim)
dim(sim.mat)
```

```
## [1] 10000     1
```

```r
head(sim.mat) 
```

```
##           [,1]
## [1,] 0.2596638
## [2,] 0.9902874
## [3,] 0.9162283
## [4,] 0.2309883
## [5,] 0.7674306
## [6,] 0.5669877
```

```r
# Calculate rowmeans - with n=1, this doesn't change anything
# But change n to anything bigger and inspect the dimensions of the objects
dosm <- rowMeans(sim.mat)
str(dosm)
```

```
##  num [1:10000] 0.26 0.99 0.916 0.231 0.767 ...
```

```r
head(dosm) # compare these values to sim.mat
```

```
## [1] 0.2596638 0.9902874 0.9162283 0.2309883 0.7674306 0.5669877
```

```r
par(mfrow = c(1,1))
hist(dosm, freq = FALSE) # plotting the simulated values
# Set up a vector that goes from 0 to 1 to overlay a normal distribution on the histogram
x <- seq(0, 1, length.out = 1000) 
# Now plot a normal distribution, using the mean and sd of the simulated values
lines(x, dnorm(x, mean = mean(dosm), sd = sd(dosm)), col = "red")
```

<img src="05_random_variables_files/figure-html/unnamed-chunk-6-1.png" width="672" />


## A probabilistic model for simple linear regression


