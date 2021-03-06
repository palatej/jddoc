---
layout: left-menu
title: Ljung-Box
tagline: technical documentation for JDemetra+ using GitHub Pages
description: Ljung-Box test
category: White noise tests
order: 1010
---
# {{page.description}}

#### Overview

The Ljung-Box test checks the "overall" randomnes of a time series using a given number of [autocorrelations](../../descriptive.md).   
It tests wether any of a group of autocorrelations of a time series are significantly different from 0.

#### Algorithm

We consider the autocorrelations $\hat\gamma_l, \cdots, \hat\gamma_{l\cdot k}$. Typically, $l=1$ when testing the independence of the series or $l=freq$ when testing seasonality.

The value of the test is defined by

$$ lb=n \left(n+2\right)\sum_{i=1}^k\frac{\hat\gamma_{i \cdot l}^2}{n-i \cdot l}$$

It is asymptotically distributed as a $\chi \left(k\right)$

####  References

Ljung G. M. and G. E. P. Box (1978). "On a Measure of a Lack of Fit in Time Series Models". Biometrika 65 (2): 297–303. doi:10.1093/biomet/65.2.297


#### Implementation

This test is implemented in the class `demetra.stats.tests.LjungBoxTest`

#### Example

```java
    int N=100;
    DataBlock sample=DataBlock.make(N);
    Random rnd=new Random();
    sample.set(rnd::nextDouble);
    LjungBoxTest lb=new LjungBoxTest(sample);
    StatisticalTest test = lb
             .lag(3)
             .autoCorrelationsCount(10)
             .build();
```
