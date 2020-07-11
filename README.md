# SPConv.pytorch
[ IJCAI-20 ] Split to Be Slim: An Overlooked Redundancy in Vanilla Convolution

This repo provides Pytorch implementation of IJCAI 2020 paper   
[Split to Be Slim: An Overlooked Redundancy in Vanilla Convolution](https://arxiv.org/abs/2006.12085)

Pretrained models will be released soon.

# Requirements
- Python 3
- Pytorch 1.1
- NVIDIA DALI for GPU dataloader 
- NVIDIA APEX for mixed precision

# Introduction of SPConv
## Redundancy in Feature Maps

<div align=center><img width='400' height='330' src="https://github.com/qiulinzhang/SPConv.pytorch/blob/master/images/redundant_feature_maps.png"/></div>

## Abstract
We reveal that many feature maps within a layer share similar but not identical patterns. However, it is difficult to identify if features with similar patterns are redundant or contain essential details. Therefore, instead of directly removing uncertain redundant features, we propose a **sp**lit based convolutional operation, namely **SPConv**, to tolerate features with similar patterns but require less computation. 

Specifically, we split input feature maps into the representative part and the uncertain redundant part, where intrinsic information is extracted from the representative part through relatively heavy computation while tiny hidden details in the uncertain redundant part are processed with some light-weight operation.

## SPConv Module

<div align=center><img src="https://github.com/qiulinzhang/SPConv.pytorch/blob/master/images/spconv_module.png"/></div>


## Performance
**Outperforms SOTA baselines in both accuracy and inference time on GPU, with FLOPs and parameters dropped sharply.**
### Small Scale Classification

<table class="tg">
<thead>
  <tr>
    <th class="tg-c3ow" colspan="6">CIFAR_10 - VGG_16</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td class="tg-c3ow">Model</td>
    <td class="tg-c3ow">FLOPs</td>
    <td class="tg-c3ow">FLOPs<br>Reduced</td>
    <td class="tg-c3ow">Params</td>
    <td class="tg-c3ow">Params<br>Reduced</td>
    <td class="tg-c3ow">Acc@1</td>
  </tr>
  <tr>
    <td class="tg-c3ow">VGG_16-Baseline</td>
    <td class="tg-c3ow">349.51M</td>
    <td class="tg-c3ow">-</td>
    <td class="tg-c3ow">16.62M</td>
    <td class="tg-c3ow">-</td>
    <td class="tg-c3ow">94.00%</td>
  </tr>
  <tr>
    <td class="tg-c3ow">Ghost-VGG_16-s2</td>
    <td class="tg-c3ow">158M</td>
    <td class="tg-c3ow">45.20%</td>
    <td class="tg-c3ow">7.7M</td>
    <td class="tg-c3ow">53.67%</td>
    <td class="tg-c3ow">93.70%</td>
  </tr>
  <tr>
    <td class="tg-7btt"><b>SPConv-VGG_16-α1/2</b></td>
    <td class="tg-7btt">118.27M</td>
    <td class="tg-7btt">66.24%</td>
    <td class="tg-7btt">5.6M</td>
    <td class="tg-7btt">66.30%</td>
    <td class="tg-7btt">94.40%</td>
  </tr>
  <tr>
    <td class="tg-c3ow">HetConv-VGG_16-P4</td>
    <td class="tg-c3ow">105.98M</td>
    <td class="tg-c3ow">69.67%</td>
    <td class="tg-c3ow">5.17M</td>
    <td class="tg-c3ow">68.89%</td>
    <td class="tg-c3ow">93.92%</td>
  </tr>
  <tr>
    <td class="tg-7btt"><b>SPConv-VGG_16-α1/4</b></td>
    <td class="tg-7btt">79.34M</td>
    <td class="tg-7btt">77.29%</td>
    <td class="tg-7btt">3.77M</td>
    <td class="tg-7btt">77.31%</td>
    <td class="tg-7btt">93.94%</td>
  </tr>
  <tr>
    <td class="tg-c3ow">HetConv-VGG_16-P8</td>
    <td class="tg-c3ow">76.89M</td>
    <td class="tg-c3ow">78.00%</td>
    <td class="tg-c3ow">3.54M</td>
    <td class="tg-c3ow">78.70%</td>
    <td class="tg-c3ow">93.86%</td>
  </tr>
  <tr>
    <td class="tg-7btt"><b>SPConv-VGG_16-α1/8</b></td>
    <td class="tg-7btt">59.87M</td>
    <td class="tg-7btt">82.87%</td>
    <td class="tg-7btt">2.85M</td>
    <td class="tg-7btt">82.85%</td>
    <td class="tg-7btt">93.77%</td>
  </tr>
  <tr>
    <td class="tg-7btt"><b>SPConv-VGG 16-α1/16</b></td>
    <td class="tg-7btt">55.14M</td>
    <td class="tg-7btt">84.22%</td>
    <td class="tg-7btt">2.39M</td>
    <td class="tg-7btt">85.62%</td>
    <td class="tg-7btt">93.43%</td>
  </tr>
  <tr>
    <th class="tg-c3ow" colspan="6">CIFAR_10 - ResNet_20</th>
  </tr>
  <tr>
    <td class="tg-c3ow">ResNet_20-Baseline</td>
    <td class="tg-c3ow">41.62M</td>
    <td class="tg-c3ow">-</td>
    <td class="tg-c3ow">0.27M</td>
    <td class="tg-c3ow">-</td>
    <td class="tg-c3ow">92%</td>
  </tr>
  <tr>
    <td class="tg-7btt"><b>SPConv-ResNet_20-α1/2</b></td>
    <td class="tg-7btt">17.91M</td>
    <td class="tg-7btt">56.96%</td>
    <td class="tg-7btt">0.10M</td>
    <td class="tg-7btt">63.00%</td>
    <td class="tg-7btt">92.23%</td>
  </tr>
  <tr>
    <td class="tg-7btt"><b>SPConv-ResNet_20-α1/4</b></td>
    <td class="tg-7btt">12.89M</td>
    <td class="tg-7btt">75.88%</td>
    <td class="tg-7btt">0.071M</td>
    <td class="tg-7btt">73.70%</td>
    <td class="tg-7btt">91.15%</td>
  </tr>
</tbody>
</table>

### Large Scale Classification


<table class="tg">
<thead>
  <tr>
    <th class="tg-c3ow" colspan="9">ImageNet2012-ResNet50</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td class="tg-c3ow">Model</td>
    <td class="tg-c3ow">FLOPs</td>
    <td class="tg-c3ow">FLOPs<br>Reduced</td>
    <td class="tg-c3ow">Params</td>
    <td class="tg-c3ow">Params<br>Reduced</td>
    <td class="tg-c3ow">Acc@1</td>
    <td class="tg-c3ow">Acc@5</td>
    <th class="tg-c3ow">Inference Time<br>on GPU</th>
    <td class="tg-baqh">Download</td>
  </tr>
  <tr>
    <td class="tg-c3ow">ResNet50-Baseline</td>
    <td class="tg-c3ow">4.14G</td>
    <td class="tg-c3ow">-</td>
    <td class="tg-c3ow">25.56M</td>
    <td class="tg-c3ow">-</td>
    <td class="tg-c3ow">75.91%</td>
    <td class="tg-c3ow">92.78%</td>
    <td class="tg-c3ow">1.32 ms</td>
    <td class="tg-baqh">-</td>
  </tr>
  <tr>
    <td class="tg-c3ow">SPConv-ResNet50-α1/2</td>
    <td class="tg-c3ow">2.97G</td>
    <td class="tg-c3ow">28.26%</td>
    <td class="tg-c3ow">18.34M</td>
    <td class="tg-c3ow">28.24%</td>
    <td class="tg-c3ow">76.26%</td>
    <td class="tg-c3ow">93.05%</td>
    <td class="tg-c3ow">1.23 ms</td>
    <td class="tg-baqh"><a href="https://bupteducn-my.sharepoint.com/:u:/g/personal/qiulinzhang_bupt_edu_cn/Eacma1q0fspOgDrOHTtLhT8BHUCKCVCNJl-QY3iuMHa5qg?e=5RTyaO">model</a></td>
  </tr>
  <tr>
    <td class="tg-c3ow">HetConv-ResNet50-P4</td>
    <td class="tg-c3ow">2.85G</td>
    <td class="tg-c3ow">30.32%</td>
    <td class="tg-c3ow">-</td>
    <td class="tg-c3ow">-</td>
    <td class="tg-c3ow">76.16%</td>
    <td class="tg-c3ow"></td>
    <td class="tg-c3ow">-</td>
    <td class="tg-baqh">-</td>
  </tr>
  <tr>
    <td class="tg-c3ow">SPConv-ResNet50-α1/4</td>
    <td class="tg-c3ow">2.74G</td>
    <td class="tg-c3ow">33.82%</td>
    <td class="tg-c3ow">16.93M</td>
    <td class="tg-c3ow">33.76%</td>
    <td class="tg-c3ow">75.95%</td>
    <td class="tg-c3ow">92.99%</td>
    <td class="tg-c3ow">1.19 ms</td>
    <td class="tg-baqh"><a href="https://bupteducn-my.sharepoint.com/:u:/g/personal/qiulinzhang_bupt_edu_cn/ERYv3or59alFqGJ-P6ahrNsBgq7mEfg7BO2spoptdnYyww?e=Ls6aTZ">model</a></td>
  </tr>
  <tr>
    <td class="tg-c3ow">SPConv-ResNet50-α1/8</td>
    <td class="tg-c3ow">2.62G</td>
    <td class="tg-c3ow">36.72%</td>
    <td class="tg-c3ow">16.22M</td>
    <td class="tg-c3ow">36.54%</td>
    <td class="tg-c3ow">75.40%</td>
    <td class="tg-c3ow">92.77%</td>
    <td class="tg-c3ow">1.17 ms</td>
    <td class="tg-baqh"><a href="https://bupteducn-my.sharepoint.com/:u:/g/personal/qiulinzhang_bupt_edu_cn/EegfE1Ei2h5Kn9tpg47J_lsBQcXJHJodZs7EqMbZdl9U1g?e=OBeUju">model</a></td>
  </tr>
  <tr>
    <td class="tg-c3ow">OctConv-ResNet50-α0.5†</td>
    <td class="tg-c3ow">2.40G</td>
    <td class="tg-c3ow">42.00%</td>
    <td class="tg-c3ow">25.56M</td>
    <td class="tg-c3ow">0.00%</td>
    <td class="tg-c3ow">76.40%</td>
    <td class="tg-c3ow">93.14%</td>
    <td class="tg-c3ow">3.51 ms</td>
    <td class="tg-baqh">-</td>
  </tr>
  <tr>
    <td class="tg-c3ow">Ghost-ResNet50-s2</td>
    <td class="tg-c3ow">2.20G</td>
    <td class="tg-c3ow">46.85%</td>
    <td class="tg-c3ow">13.0M</td>
    <td class="tg-c3ow">49%</td>
    <td class="tg-c3ow">75%</td>
    <td class="tg-c3ow">92.3%</td>
    <td class="tg-c3ow">-</td>
    <td class="tg-baqh">-</td>
  </tr>
</tbody>
</table>

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
