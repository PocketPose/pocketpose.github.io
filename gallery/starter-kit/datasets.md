---
title: Supported Datasets
layout: page
---

This page provides a list of supported datasets for training and evaluation. We provide scripts to download and prepare the datasets, including the annotations converted to our JSON format in some cases.

Dataloaders for the following datasets are provided:
- [x] [COCO](http://cocodataset.org/#keypoints-challenge2017)
- [x] [MPII](http://human-pose.mpi-inf.mpg.de)
- [x] [Leeds Sports Pose (LSP)](http://sam.johnson.io/research/lsp.html)

## 2D Keypoint Datasets

### MPII Human Pose Dataset

- Download the [dataset](https://datasets.d2.mpi-inf.mpg.de/andriluka14cvpr/mpii_human_pose_v1.tar.gz) and create a link to the `images` directory at `./data/mpii/
images`
  ```
  ln -s ${MPII_PATH}/images ./data/mpii/images
  ```

- Download the [annotation file](https://drive.google.com/open?id=1mQrH_yVHeB93rzCfyq5kC9ZYTwZeMsMm) in our JSON format, and save it to `./data/mpii/mpii_annotations.json`


### COCO Keypoints 2014/2017

- Download datasets:
  ```
  cd ./data/mscoco
  wget http://images.cocodataset.org/zips/train2014.zip
  wget http://images.cocodataset.org/zips/val2014.zip
  wget http://images.cocodataset.org/zips/train2017.zip
  wget http://images.cocodataset.org/zips/val2017.zip
  unzip train2014.zip -d images
  unzip train2014.zip -d images
  unzip train2014.zip -d images
  unzip train2014.zip -d images
  rm -rf *.zip
  ```

  - Download the [coco_annotations_2014.json](https://drive.google.com/open?id=1jrxis4ujrLlkwoD2GOdv3PGzygpQ04k7) and [coco_annotations_2017.json](https://drive.google.com/open?id=1YuzpScAfzemwZqUuZBrbBZdoplXEqUse) in our JSON format, and save it to `./data/mscoco`


### Leeds Sports Pose (LSP)
- Download datasets:
  ```
  mkdir -p ./data/lsp/images
  cd ./data/lsp/images
  wget http://sam.johnson.io/research/lsp_dataset.zip
  wget http://sam.johnson.io/research/lspet_dataset.zip
  unzip lsp_dataset.zip -d lsp_dataset
  unzip lspet_dataset.zip -d lspet_dataset
  ```

  - Download the [LEEDS_annotations.json](https://drive.google.com/open?id=1GZxlTLuMfA3VRvz2jyv8fhJDqElNrgKS) in our JSON format, and save it to `./data/lsp`
