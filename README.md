# SPConv.pytorch
[ IJCAI-20 ] Split to Be Slim: An Overlooked Redundancy in Vanilla Convolution

This repo provides Pytorch implementation of IJCAI 2020 paper [Split to Be Slim: An Overlooked Redundancy in Vanilla Convolution](https://arxiv.org/abs/2006.12085)

Pretrained models will be released soon.

# Requirements
- Python 3
- Pytorch 1.1
- NVIDIA DALI for GPU dataloader 
- NVIDIA APEX for mixed precision

# Introduction of SPConv
## Redundancy in Feature Maps

<div align=center><img width='400' height='330' src="https://github.com/qiulinzhang/SPConv.pytorch/blob/master/images/redundant_feature_maps.png"/></div>

## SPConv Module

<div align=center><img src="https://github.com/qiulinzhang/SPConv.pytorch/blob/master/images/spconv_module.png"/></div>


## Performance
**Outperforms SOTA baselines in both accuracy and inference time on GPU, with FLOPs and parameters dropped sharply.**
### Small Scale Classification
<div align=center><img src="https://github.com/qiulinzhang/SPConv.pytorch/blob/master/images/cifar_10.png"/></div>

### Large Scale Classification
<div align=center><img src="https://github.com/qiulinzhang/SPConv.pytorch/blob/master/images/imagenet.png"/></div>

## Citation

If you find this work or code is helpful in your research, please cite:

```
@inproceedings{zhang2020spconv,
  title={Split to Be Slim: An Overlooked Redundancy in Vanilla Convolution},
  author={Zhang, Qiulin and Jiang, Zhuqing and Lu, Qishuo and Han, Jia'nan and Zeng, Zhengxin and Gao, Shang-Hua and Men, Aidong},
  booktitle={International Joint Conference on Artificial Intelligence (IJCAI)},
  year={2020}
}
```
