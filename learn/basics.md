---
title: Basic Concepts
layout: tutorial
description: Get started with Human Pose Estimation and understand the basics of the field.
parent: Learn Human Pose Estimation
order: 1
---

Human Pose Estimation is the task of estimating the pose of a person from an image or a video by localizing the different keypoints on the person. The keypoints are the different joints on the body, such as the elbow, shoulder, hip, knee, etc. The pose estimation problem can be represented as a regression problem to fit a model that predicts the location of these keypoints given an image. The keypoints can be represented as a set of points (x,y) coordinates.

The number of keypoints varies by dataset. For example, the [LSP dataset](http://sam.johnson.io/research/lsp.html) has 14 keypoints, the [MPII dataset](http://human-pose.mpi-inf.mpg.de/) has 16 keypoints, and the [COCO dataset](http://cocodataset.org/#home) has 17 keypoints

Pose Estimation can be broadly classified into two categories: 
- [__2D Pose Estimation__](https://arxiv.org/abs/1804.06208v2): Estimate (x,y) coordinates for each joint in pixel space from RGB input.
- [__3D Pose Estimation__](https://arxiv.org/abs/1705.03098v2): Estimate (x,y,z) coordinates in metric space from RGB input.

This [presentation by Wei Yang](https://www.slideshare.net/plutoyang/mmlab-seminar-2016-deep-learning-for-human-pose-estimation) provides an informative roadmap on 2D Human Pose Estimation research.
