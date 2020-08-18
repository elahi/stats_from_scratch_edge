---
output: html_document
editor_options: 
  chunk_output_type: console
---



# Parametric estimation and inference {#parametric}



If all of the random variables in our model can be described by a finite set of parameters, we are using *parametric* estimation and inference. In paremetric estimation, the most important mathematical concept is the likelihood function, or **likelihood**. 

> The likelihood allows us to compare values of a parameter in terms of their (the values') ability to explain the observed data. In other words, if the true value of the parameter is y, how likely is the observed dataset?

Suppose the observations, which we call $d$, are instances drawn from a random variable $D$, which is governed by a probability distribution function. *We do not know what this probability distribution is!* We have to think about the data - are they continuous or discrete; are they bounded at 0 or elsewhere; is the variance uniform or not? Based on the answers to these questions, we then assume a probability distribution function, $f_D$. 

We can use $f_D$ to evaluate the probability of the data, $d$, at every potential value of the parameter $\theta$ we are trying to estimate, and we call this the likelihood $L(\theta)$:

$$
\begin{aligned}
L(\theta) = f_D(d | \theta)
\end{aligned}
$$

It is tempting to think of the likelihood as a probability distribution. But it is not, because the function does not sum or integrate to 1 with respect to $\theta$ (which is a requirement for a probability distribution function). This is partly why we are defining it (the likelihood) as separate idea: the likelihood is a function of the parameters, and we use it to ask questions about the plausibility of the data (which are fixed), assuming different values of the parameters. If $L(\theta_1|d) > L(\theta_2|d)$, then the data we have observed are more likely to have occurred if $\theta = \theta_1$ than $\theta = \theta_2$. We interpret this result as: $\theta_1$ is a more plausible value for $\theta$ than $\theta_2$. 

Ok, so how do we actually calculate the likelihood? Suppose the data are $n$ independent observations, $x_1, x_2, ..., x_n$ each with the density function $f_X(x)$, which depends on parameter $\theta$. This means that these observations are independent and identically distributed, and the joint density function (of the *data* and the *likelihood*) is given by:

$$
\begin{aligned}
f_{X_1, X_2, ..., X_n}(x_1, x_2, ..., x_n) =& ~ f_X(x_1) * f_X(x_2) * ... * f_X(x_n) \\
=& ~ \prod_{i = 1}^n f_X(x_i)
\end{aligned}
$$

where the symbol $\prod$ denotes multiplication in the same way that the symbol $\sum$ denotes addition. Instead of multiplying, we'd prefer to work with sums for numerical reasons. Because the log of a product is the sum of the logarithms of the terms being multiplied, 

$$
\begin{aligned}
\text{ln}(yz) = \text{ln}(y) + \text{ln}(z)
\end{aligned}
$$

we can express the joint density function as a sum instead:

$$
\begin{aligned}
\text{ln}[f_X(x_1) * f_X(x_2) * ... * f_X(x_n)] =& ~ \sum_{i = 1}^n \text{ln}[f_X(x_i)]
\end{aligned}
$$

and define it as follows:

$$
\begin{aligned}
l(\theta) = \text{ln}[L(\theta)]
\end{aligned}
$$

The likelihood provides a framework for estimation and inference. 

### Exercise set 9-1 

1. Is this statement true / false? 

*The value of $\theta$ that maximizes $L(\theta)$ is the most probable value of $\theta$ given the observed data.*

False - see Edge explanation. Change to:

*The value of $\theta$ that maximizes $L(\theta)$ is the one that maximizes the probability of obtaining the observed data.*

2. Write all of the following in the simplest form:

  a. The pdf of $X$, a Normal($\mu, \sigma^2$) random variable:
  
$$
\begin{aligned}
f_X(x) = \frac{1}{\sigma \sqrt{2 \pi}}e^{-\frac{(x - \mu)^2}{2 \sigma^2}}
\end{aligned}
$$

  b. The log-likelihood of $\mu$ given an observation of $x$, which is assumed to be an instance of $X$:
  
$$
\begin{aligned}
l(\mu) =& ~ \text{ln}(\frac{1}{\sigma \sqrt{2 \pi}}e^{-\frac{(x - \mu)^2}{2 \sigma^2}}) \\
       =& ~ \text{ln}(\frac{1}{\sigma \sqrt{2 \pi}}) + \text{ln}(e^{-\frac{(x - \mu)^2}{2 \sigma^2}}) \\
       =& ~ \text{ln}(\frac{1}{\sigma \sqrt{2 \pi}}) - \frac{(x - \mu)^2}{2 \sigma^2} \\
\end{aligned}
$$

  c. The joint density of $X_1$ and $X_2$, two independent Normal($\mu, \sigma^2$) random variables. 
  
$$
\begin{aligned}
f_{X_1, X_2}(x_1, x_2) =& ~ \frac{1}{\sigma \sqrt{2 \pi}}e^{-\frac{(x_1 - \mu)^2}{2 \sigma^2}} *
                         \frac{1}{\sigma \sqrt{2 \pi}}e^{-\frac{(x_2 - \mu)^2}{2 \sigma^2}} \\
                        & \text{consider each of these terms as a, b, and c:} \\
                       =& ~ (ab)*(ac) \\
                       =& ~ a^2(bc) \\
                        & \text{therefore we can write} \\
                       =& ~ \frac{1}{\sigma^2 2 \pi} e^{-\frac{(x_1 - \mu)^2}{2 \sigma^2}} * 
                            e^{-\frac{(x_2 - \mu)^2}{2 \sigma^2}} \\
                        & \text{we know that } a^m * a^n = a^{m + n} \text{, so} \\
                       =& ~ \frac{1}{\sigma^2 2 \pi} e^{-\frac{(x_1 - \mu)^2 + (x_2 - \mu)^2}{2 \sigma^2}} \\
\end{aligned}
$$  

  d. The log-likelihood of $\mu$ given an observation of $x_1$ and $x_2$, which are assumed to be instances of $X_1$ and $X_2$:
  
$$
\begin{aligned}
l(\mu) =& ~ \text{ln}(\frac{1}{\sigma^2 2 \pi} e^{-\frac{(x_1 - \mu)^2 + (x_2 - \mu)^2}{2 \sigma^2}}) \\
       =& ~ \text{ln}(\frac{1}{\sigma^2 2 \pi}) + \text{ln}( e^{-\frac{(x_1 - \mu)^2 + (x_2 - \mu)^2}{2 \sigma^2}}) \\
       =& ~ \text{ln}(\frac{1}{\sigma^2 2 \pi}) -\frac{(x_1 - \mu)^2}{2 \sigma^2} -\frac{(x_2 - \mu)^2}{2 \sigma^2}\\
       & \text{though I don't know how to get to Edge's answer:} \\
       =& ~ 2~\text{ln}(\frac{1}{\sigma \sqrt {2 \pi}}) -\frac{(x_1 - \mu)^2}{2 \sigma^2} -\frac{(x_2 - \mu)^2}{2 \sigma^2}\\
\end{aligned}
$$  

  d. The log-likelihood of $\mu$ given observations of $x_1, x_2, ..., x_n$, which are assumed to be instances of $n$ independent random variables with a Normal($\mu, \sigma^2$) distribution:
  
$$
\begin{aligned}
l(\mu) =& ~ n~\text{ln}(\frac{1}{\sigma \sqrt {2 \pi}}) - \sum_{i = 1}^n \frac{(x_i - \mu)^2}{2 \sigma^2} \\
\end{aligned}
$$  
  
## 9.1 Parametric estimation using maximum likelihood

### Exercise set 9-2

### Exercise set 9-3

## 9.2 Parametric interval estimation: the direct approach and Fisher information

### Exercise set 9-4

## 9.3 Parametric hypothesis testing using the Wald test

### Exercise set 9-5

## 9.4 Parametric hypothesis testing using the likelihood-ratio test

### Exercise set 9-6
