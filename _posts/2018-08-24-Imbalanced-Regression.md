---
toc: false
layout: post
description: Initial Results with Synthetic Minority Over-Sampling Technique for Regression
categories: [Regression,Imbalanced Data]
title: Tackling Imbalanced Regression with SMOGN 
---
Imbalanced data is ubiquitous in practice and both research and high quality 
[open source software](https://github.com/scikit-learn-contrib/imbalanced-learn)
exist for dealing with Imbalanced Classification tasks. Generally speaking, the approaches are
under-sampling observations from classes that are dominating the data or over-sampling
observations from rare classes. This can be done in naive ways (sampling with replacement)
or in more sophisticated ways, e.g. by creating synthetic observations based on real
observations with added noise.


When working on a Regression problem with imbalanced target variable distribution, I've found
three main approaches:
1. [LogTransform](https://scikit-learn.org/stable/auto_examples/compose/plot_transformed_target.html) of the Target Variable
2. [Synthetic Minority Over-Sampling Technique for Regression](https://github.com/nickkunz/smogn) - SMOGN
3. [Deep Imbalanced Regression](https://github.com/YyzHarry/imbalanced-regression) - DIR


LogTransform is in my standard toolbox and helped to boost performance as expected. But 
the imbalance/distribution skew was still far from resolved and thus predictions still centered in
the range of most frequent observations. My Ridge, Gradient Boosting and FC-DNN models would completely 
ignore a significant range of (rare) target values in their predictions. Problem not solved!


Preprocessing the data with SMOGN took around 10 minuts and lead to a slightly worse MAPE performance, 
but a much better coverage of the entire target value range. SMOGN provides roughly [three stages](https://github.com/nickkunz/smogn/tree/master/examples)
of customization for this re-sampling process. I'd characterize these as automated, automated within bounds
and manual. So far I've tested the automated preprocessing and while I'm satisfied with the result,
the new distribution has become multimodal and still not ideal for training. But I'm optimistic that
adding bounds or going for full manual configuration of the re-sampling should lead to
further improvements. Problem still not solved, but a step in the right direction.


On my dataset, the total number of observations was slightly reduced after SMOGN upsampled rare observations
and downsampled the frequent ones. Having taken care of all other preprocessing (missing data, numeric 
representations etc.), the number of columns was not affected. Lastly, I've compared 2D principal component 
analysis of the original dataset and the same dataset after re-sampling with SMOGN and found the scatterplots
to overlap very well.


So far, I've not tried to apply DIR, as it seems a bit less straightforward, consisting of both label smoothing
and feature smoothing and the examples include integration into the PyTorch model and training loop. 
So this might not be applicable to the Ridge and Gradient Boosting models I keep running for comparison.
