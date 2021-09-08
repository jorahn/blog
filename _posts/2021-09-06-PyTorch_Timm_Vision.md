---
toc: false
layout: post
description: Comparison of PyTorch CV Models on DeepFashion Dataset
categories: [Vision,Fine Tuning]
title: Fine-Tuning PyTorch Vision Models 
---
After the surprising Image Classification results with [zero-shot CLIP]({{ site.baseurl }}/clip/prompt%20engineering/2021/08/23/Zero_Shot.html),
I've run a test over a number of deep computer vision architectures from [torchvision](https://github.com/pytorch/vision/tree/main/torchvision/models), 
[fastai](https://github.com/fastai/fastai/blob/master/nbs/11_vision.models.xresnet.ipynb) and the awesome [timm library](https://github.com/rwightman/pytorch-image-models) by Ross Wightman.


I'm using a 20-class subset of [DeepFashion](http://mmlab.ie.cuhk.edu.hk/projects/DeepFashion.html) with around 100k images
as the dataset. To accomodate memory requirements of different architectures, I've set batch_size to 32 (this leaves room for improvements
in smaller models). All models are pretrained on ImageNet, are built with a new initialized head and subsequently 
fine-tuned on DeepFashion for one epoch with frozen weights (new head only) and three epochs with unfrozen weights.


![image]({{ site.baseurl }}/images/finetuning_deepfashion/deepfashion.png "DeepFashion Dataset")


Training took on average ~20 minutes per epoch for all models on my hardware, so around 1:15h per model 
(the first epoch with frozen weights is generally a bit faster, than the others). The full run took around 18 hours in total.
Eventually, I might do a few more runs, just to get a feel for the actual distribution of results. Here are the results:


| Model | Library | Accuracy | Training per epoch (mins) |
|-|-|-|-|
| resnet34 | torch | 0.428767 | 12:34 |
| resnet50 | torch | 0.441164 | 18:08 |
| resnet101 | torch | 0.446995 | 24:50 |
| resnet152 | torch | 0.448151 | 32:15 |
| xresnet34 | fastai | 0.326014 | 12:44 |
| xresnext34 | fastai | 0.255726 | 15:24 |
| efficientnet_b0 | timm | 0.382433 | 13:39 |
| efficientnet_b2 | timm | 0.385690 | 16:47 |
| efficientnet_b4 | timm | 0.360475 | 24:01 |
| densenet121 | timm | 0.395409 | 20:14 |
| inception_v4 | timm | 0.395409 | 23:00 |
| inception_resnet_v2 | timm | 0.405652 | 25:18 |
| mobilenetv3_large_100 | timm | 0.385007 | 11:40 |
| vit_base_patch16_224 | timm | failed | n/a |
| xception41 | timm | 0.389262 | 23:40 |


I was a little surprised, how well the good-old ResNets perform in this setting. Even the smaller ones.
Certainly in terms of efficiency (cost/time to accuracy), they are a great choice.
I guess, it's partly due to the training setup (dataset, hardware, batch size, epochs ...),
that some models didn't perform better. But for my use case, this was quite informative.


![image]({{ site.baseurl }}/images/finetuning_deepfashion/training_efficiency.png "Normalized Training Efficiency")


I'm investigating, why the timm-ViT model failed to run my benchmark and also, how to run the same
test with one of the pretrained CLIP vision models (ViT or ResNet).


*Update:*  
I've wanted to try [Weights and Biases](https://wandb.ai/) for some time now, and this project has provided me 
with a great opportunity. After comparing architectures, I've run a couple of (parallel) experiments locally and in Colab
to compare ResNet34 with different Learning Rate Schedules on the same dataset. Please see 
[here](https://wandb.ai/jrahn/finetune_resnet34_deepfashion) for more details.


![image]({{ site.baseurl }}/images/finetuning_deepfashion/rn34_deepfashion_learning-rates.png "Learning Rate Schedules with W&B (showing 5 out of 8 runs)")
