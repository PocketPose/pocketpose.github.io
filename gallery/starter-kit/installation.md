---
title: Installation Guide
layout: page
---

# Installation Guide

## Prerequisites
- PyTorch 0.4.1 or higher

Note that the original code was developed with Python2 and has not been tested with Python3 yet. If you would like to contribute to the project and update the code to Python3 and a newer version of PyTorch, please feel free to submit a pull request.

## Installation
1. Clone the repository:
```
git clone --recursive https://github.com/saifkhichi96/human-pose-estimation-starter.git
```
2. Install the required Python packages:
```
pip install -r requirements.txt
```
3. Create a symbolic link to the `images` directory of the MPII dataset:
   ```
   ln -s PATH_TO_MPII_IMAGES_DIR data/mpii/images
   ```
   For training/testing on COCO, please refer to [COCO Readme](../datasets/coco.md).
4. Download annotation file:
    * (MPII) Download [mpii_annotations.json](https://drive.google.com/open?id=1mQrH_yVHeB93rzCfyq5kC9ZYTwZeMsMm) and save it to `data/mpii`
    * (COCO) Download [coco_annotations_2014.json](https://drive.google.com/open?id=1jrxis4ujrLlkwoD2GOdv3PGzygpQ04k7) or/and [coco_annotations_2017.json](https://drive.google.com/open?id=1YuzpScAfzemwZqUuZBrbBZdoplXEqUse) and save it to `data/coco`

## Usage
1. Download and prepare the dataset following the instructions in the `data/` folder.
2. Train a human pose estimation model by running the training script:
```
python src/train.py --config configs/config.yaml
```
3. Evaluate the model on the test dataset:
```
python src/evaluate.py --config configs/config.yaml
```

## Structure
- `data/`: A folder containing a small dataset for testing purposes and instructions for obtaining larger datasets.
- `notebooks/`: A folder containing Jupyter notebooks to demonstrate the implementation.
- `src/`: A folder containing the main source code for human pose estimation.
- `models/`: A folder with code for various pose estimation models (ViTPose, TokenPose, etc.).
- `utils/`: A folder with utility functions for data loading, preprocessing, and postprocessing.
- `configs/`: A folder containing configuration files for different models and training settings.
- `requirements.txt`: A list of required Python packages.