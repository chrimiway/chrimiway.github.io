---
layout:     post
title:      Completing Squares
subtitle:   
date:       2018-09-20
author:     Zhenhua Wang
header-img: img/post-bg-coffee.jpeg
catalog: true
tags:
    - linear algebra
---

> A technique which can be used to check whether a function is always positive

## Background

In linear algebra or machine learning, we sometimes need to check whether a matrix is a positive definite matrix (a symmetric matrix with all of its eigenvalue greater than zero). During this procedure, we first calculate *x'Ax*, whose results is a quadratic function of the elements of **arbitrary** vector x. The next step is to check whether this function is always greater than zero on all valid x.

## Steps

One way to show that a function is a straightly positive is completing square. 
1. we fisrt look at the *interaction term* between elements of x. 
2. Then, we choose one of the elements that is in the interaction term as the base. 
3. We then write down beta1(x1 + beta2* x2)^2, where beta1 is , beta2 is to be determined by the coefficient of the interaction term. 
4. The last step is to count how many x2^2 we have used, and add up all the left x2^2 (Notes: the number of x2^2 left could be negtive, zero or positive)

## Example:
    
