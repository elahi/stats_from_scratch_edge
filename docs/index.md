--- 
title: "Notes on Statistical Thinking from Scratch"
author: "Robin Elahi"
date: "2020-04-21"
site: bookdown::bookdown_site
output: bookdown::gitbook
documentclass: book
bibliography: [book.bib, packages.bib]
biblio-style: apalike
link-citations: yes
github-repo: elahi/stats_from_scratch_edge
description: "Cliff notes for Statistical Thinking from Scratch, by Doc Edge."
---

# Preface {-}

This project is a set of notes for [Statistical Thinking from Scratch](https://global.oup.com/academic/product/statistical-thinking-from-scratch-9780198827634?cc=us&lang=en&#), by [M.D. Edge](https://www.doc-edge.net/). The goal is to become more comfortable with the nitty gritty underlying the statistical tools I commonly use - essentially, regression. Edge takes a unique approach in that he takes a small dataset, and dissects regression 'from scratch'. Each of these `bookdown` chapters corresponds to each of Edge's 10 book chapters. The impetus for this `bookdown` project was the cancellation of my spring 2020 course [Experimental Design and Probability](https://elahi.github.io/xdp/) due to [COVID-19](https://healthalerts.stanford.edu/). So, I'll be filling in some gaps in my stats toolkit and learning how to use [bookdown](https://bookdown.org/). 

The **stfs** package can be installed from Github:


```r
install.packages("devtools")
library(devtools) 
install_github("mdedge/stfspack")
library(stfspack)
```




As Edge points out in his **Prelude**, the typical introductory course in biological statistics (including my own) revolves around learning a series of *tests*: t-tests, regression, ANOVA . In *STFS*, the focus instead is on one procedure - simple linear regression - and takes 'little for granted' (translation: we'll be working through the math, lightly). The primary dataset consists of 11 observations. To heck with big data. So in this project, you will find mostly code - I'll leave the exposition to Edge, who does a nice job explaining the concepts in his textbook. I'll chime in whenever it seems useful.

The chapters will work through the following:    
1. Probability  
2. Estimation (using data to guess the values that describe a data generating process)  
3. Inference (testing hypotheses about the processes that might have generated an observed dataset)  

<!-- What is a [data generating process](https://en.wikipedia.org/wiki/Data_generating_process)? This wikipedia entry is not all that helpful, aside from the fact that it highlights the difficulty in defining this term. For now, let's just think of the DGP as a set of rules (e.g., a deterministic equation) plus 'noise' that allows us to describe a set of obervations (i.e., data).  -->

#### How to publish a `bookdown` project on github {-}

https://community.rstudio.com/t/hosting-bookdown-in-github/20427  
http://seankross.com/2016/11/17/How-to-Start-a-Bookdown-Book.html

