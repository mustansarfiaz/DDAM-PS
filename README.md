# DDAM-PS: Diligent Domain Adaptive Mixer for Person Search

## Introduction

This is the official implementation for our DDAM-PS: Diligent Domain Adaptive Mixer for Person Search in WACV2024. 

Performance :
we tried some hyper-parameters and got better ReID performance reported in our paper.

|  Source   |  Target   | mAP  | Top-1 |                             CKPT                             |                             log                              |
| :-------: | :-------: | :--: | :---: | :----------------------------------------------------------: | :----------------------------------------------------------: |
|    PRW    | CUHK-SYSU | 79.5 | 81.3  | [ckpt]() |
| CUHK-SYSU |    PRW    | 36.7 | 81.2  | [ckpt]() | 

![framework](doc/framework.png)

## Installation

run `python setup.py develop` to enable SPCL

Install Nvidia [Apex](https://github.com/NVIDIA/apex)

Run `pip install -r requirements.txt` in the root directory of the project.


## Data Preparation

1. Download [CUHK-SYSU](https://drive.google.com/open?id=1z3LsFrJTUeEX3-XjSEJMOBrslxD2T5af) and [PRW](https://goo.gl/2SNesA) datasets, and unzip them.
2. Modify `configs/prw_da.yaml` and `configs/cuhk_sysu_da.yaml` to change the dataset store place (Line 1,5,6) to your own path.

## Testing

1. Following the link in the above table, download our pretrained model to anywhere you like

2. Evaluate its performance by specifing the paths of checkpoint and corresponding configuration file.

PRW as the target domain:

```
python train_da_dy_cluster.py --cfg configs/cuhk_sysu_da.yaml --eval --ckpt $MODEL_PATH
```

CUHK-SYSU as the target domain:

```
python train_da_dy_cluster.py --cfg configs/prw_da.yaml --eval --ckpt $MODEL_PATH
```

## Training

PRW as the target domain:

```
python train_da_dy_cluster.py --cfg configs/cuhk_sysu_da.yaml
```

CUHK-SYSU as the target domain:

```
python train_da_dy_cluster.py --cfg configs/prw_da.yaml
```

**Note**: At present, our script only supports single GPU training, but distributed training will be also supported in future. By default, the batch size is set to 4 for CUHK-SYSU. If your GPU cannot provide the required memory, try smaller batch size and learning rate (*performance may degrade*). 
