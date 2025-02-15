English | [简体中文](README_cn.md)

# CLRNet (CLRNet: Cross Layer Refinement Network for Lane Detection)

## Table of Contents
- [Introduction](#Introduction)
- [Model Zoo](#Model_Zoo)
- [Citations](#Citations)

## Introduction

[CLRNet](https://arxiv.org/abs/2203.10350)is a lane detection model. The CLRNet model is designed with line prior for lane detection, line iou loss as well as nms method, fused to extract contextual high-level features of lane line with low-level features, and refined by FPN multi-scale.Finally, the model achieved SOTA performance in lane detection datasets.

## Model Zoo

### CenterNet Results on COCO-val 2017

| backbone       | mF1 | F1@50   |    F1@75    | download | config |
| :--------------| :------- |  :----: | :------: | :----: |:-----: |
| ResNet-18         | 54.98 |  79.46  |    62.10   | [model]() | [config](./clr_resnet18_culane.yml) |


### Training
- single GPU
```shell
export CUDA_VISIBLE_DEVICES=0
python tools/train.py -c configs/clrnet/clr_resnet18_culane.yml
```
- multi GPU
```shell
export CUDA_VISIBLE_DEVICES=0,1,2,3
python -m paddle.distributed.launch --gpus 0,1,2,3 tools/train.py -c configs/clrnet/clr_resnet18_culane.yml
```

### Evaluation 
```shell
mkdir evaluation
python tools/eval.py -c configs/clrnet/clr_resnet18_culane.yml -o weights=output/clr_resnet18_culane/model_final.pdparams output_eval=evaluation/ use_gpu=true
```

### Inference
```shell
python tools/infer_culane.py -c configs/clrnet/clr_resnet18_culane.yml -o weights=output/clr_resnet18_culane/model_final.pdparams use_gpu=true --infer_img=demo/lane00000.jpg
```
The demo result is as shown below：
![](../../demo/lane00000_result.jpg)

## Citations
```
@InProceedings{Zheng_2022_CVPR,
    author    = {Zheng, Tu and Huang, Yifei and Liu, Yang and Tang, Wenjian and Yang, Zheng and Cai, Deng and He, Xiaofei},
    title     = {CLRNet: Cross Layer Refinement Network for Lane Detection},
    booktitle = {Proceedings of the IEEE/CVF Conference on Computer Vision and Pattern Recognition (CVPR)},
    month     = {June},
    year      = {2022},
    pages     = {898-907}
}
```
