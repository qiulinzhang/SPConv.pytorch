# SPConv.pytorch
[ IJCAI-20 ] Split to Be Slim: An Overlooked Redundancy in Vanilla Convolution

This repo provides Pytorch implementation of IJCAI 2020 paper [Split to Be Slim: An Overlooked Redundancy in Vanilla Convolution](https://arxiv.org/abs/2006.12085)

# Requirements
- Python 3
- Pytorch 1.1
- NVIDIA DALI for GPU dataloader 
- NVIDIA APEX for mixed precision

# Introduction of SPConv
## Redundancy in Feature Maps

![redundant_feature_maps](https://github.com/qiulinzhang/SPConv.pytorch/blob/master/images/redundant_feature_maps.png)

## SPConv Module

![spconv_module](https://github.com/qiulinzhang/SPConv.pytorch/blob/master/images/spconv_module.png)

## Performance
outperform state-of-the-art baselines in both accuracy and **inference time on GPU**, with FLOPs and parameters dropped sharply.
### Small Scale Classification
![cifar_10](https://github.com/qiulinzhang/SPConv.pytorch/blob/master/images/cifar_10.png)
### Large Scale Classification
![imagenet](https://github.com/qiulinzhang/SPConv.pytorch/blob/master/images/imagenet.png)
