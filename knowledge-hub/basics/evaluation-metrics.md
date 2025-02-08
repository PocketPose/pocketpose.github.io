---
title: Standard Evaluation Metrics
subtitle: "Measuring Pose Estimation Performance with Confidence"
layout: tutorial
description: "Discover the key evaluation metrics—like PCK, MPJPE, and AUC—used to assess the accuracy and reliability of pose estimation models."
parent: Basic Concepts
order: 5
---

This page contains a list of common evaluation metrics used in the field of human pose estimation.

## Percentage of Correct Keypoints (PCK)
- Detected joint is considered correct if the distance between the predicted and the true joint is within a certain threshold (threshold varies)
- PCKh@0.5 is when the threshold = 50% of the head bone link
- PCK@0.2 == Distance between predicted and true joint < 0.2 * torso diameter
- Sometimes 150 mm is taken as the threshold
- Head, shoulder, Elbow, Wrist, Hip, Knee, Ankle → Keypoints
- PCK is used for 2D and 3D (PCK3D)
- Higher the better

## Percentage of Correct Parts (PCP)
- A limb is considered detected and a correct part if the distance between the two predicted joint locations and the true limb joint locations is at most half of the limb length (PCP at 0.5 )
- Measures detection rate of limbs
- Cons - penalizes shorter limbs
- __Calculation__
  - For a specific part, PCP = (No. of correct parts for entire dataset) / (No. of total parts for entire dataset)
  - Take a dataset with 10 images and 1 pose per image. Each pose has 8 parts - ( upper arm, lower arm, upper leg, lower leg ) x2
  - No of upper arms = 10 * 2 = 20
  - No of lower arms = 20
  - No of lower legs = No of upper legs = 20
  - If upper arm is detected correct for 17  out of the 20 upper arms i.e 17 ( 10 right arms and 7 left) → PCP = 17/20 = 85%
- Higher the better

## Percentage of Detected Joints (PDJ)
- Detected joint is considered correct if the distance between the predicted and the true joint is within a certain fraction of the torso diameter
- Alleviates the shorter limb problem since shorter limbs have smaller torsos
- PDJ at 0.2 → Distance between predicted and true join < 0.2 * torso diameter
- Typically used for 2D Pose Estimation
- Higher the better

## Mean Per Joint Position Error (MPJPE)
- Per joint position error = Euclidean distance between ground truth and prediction for a joint
- Mean per joint position error = Mean of per joint position error for all k joints (Typically, k = 16)
- Calculated after aligning the root joints (typically the pelvis) of the estimated and groundtruth 3D pose.
- __PA MPJPE__
  - Procrustes analysis MPJPE.
  - MPJPE calculated after the estimated 3D pose is aligned to the groundtruth by the [Procrustes method](https://www.coursera.org/lecture/robotics-perception/pose-from-3d-point-correspondences-the-procrustes-problem-X22IH)
  - Procrustes method is simply a similarity transformation
- Lower the better
- Used for 3D Pose Estimation

## AUC
- [Let’s learn about AUC ROC Curve!](https://medium.com/greyatom/lets-learn-about-auc-roc-curve-4a94b4d88152)
- [Has My Algorithm Succeeded? An Evaluator for Human Pose Estimators](https://www.robots.ox.ac.uk/~vgg/publications/2012/Jammalamadaka12a/jammalamadaka12a.pdf)