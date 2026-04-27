# EO Drone Detection Benchmark

A standardized evaluation of object detection architectures on EO (electro-optical) drone imagery under real-world conditions.

---

<p align="center">
  <img src="assets/iris-benchmark-drone-eo-hero.png" width="100%" />
</p>

---

## Overview

This benchmark evaluates how modern object detection models behave when applied to long-range EO drone detection.

The focus extends beyond aggregate performance metrics to include **model behavior under operational conditions**, including:

- detection at long range and small object scale  
- sensitivity to background clutter  
- localization stability  
- emergence of failure modes  

All models are evaluated under aligned training and validation conditions to ensure comparability.

---

## Scope

This repository provides **evaluation results only**.

Model weights and deployment artifacts are not distributed.

The purpose of this benchmark is to:

- provide a controlled comparison across architectures  
- expose behavior not captured by aggregate metrics  
- document failure modes relevant to real-world deployment  

Deployable models derived from this evaluation are available in the IRIS Model Zoo.

---

## Problem Context

Drone detection in EO imagery introduces challenges not well represented in standard datasets:

- targets occupy very few pixels  
- contrast degrades significantly with distance  
- environmental clutter introduces ambiguity  
- object appearance varies across lighting and perspective  

Under these conditions, differences between architectures become more pronounced, particularly in recall and localization stability.

---

## Models Evaluated

The following architectures were evaluated:

- YOLOv8 (Small, Large)  
- YOLOv11 (Small)  
- RT-DETR (Large)  
- Faster R-CNN (ResNet50 FPN v2)  

All models were trained and evaluated using a consistent dataset split and aligned preprocessing pipeline.

---

## Key Result

Model performance varies significantly across architectures under identical conditions.

<p align="center">
  <img src="assets/iris-benchmark-drone-eo-comparison.png" width="90%" />
</p>

In this example:

- RT-DETR successfully detects a distant target  
- Faster R-CNN fails to detect the same target (missed detection)  
- YOLOv8 detects the target but exhibits instability in localization  

These patterns are observed consistently across multiple validation samples.

---

## Observed Behavior

### RT-DETR (Large)

- highest recall across evaluated models  
- maintains detection performance at longer distances  
- exhibits occasional duplicate detections  

---

### YOLO (v8 / v11)

- balanced performance across precision and recall  
- stable detection in moderate conditions  
- gradual degradation at long range  

---

### Faster R-CNN (ResNet50 FPN v2)

- high-confidence detections when targets are clearly visible  
- consistent failure mode at long range  
- misses small or low-contrast targets  

This failure mode is observed across multiple scenes and is not attributable to isolated data artifacts.

---

## Interpretation

Aggregate metrics such as mAP and mAR provide a summary of performance, but do not fully capture model behavior.

In this benchmark:

- recall at distance is a primary differentiator  
- failure modes are consistent and architecture-dependent  
- confidence does not always correlate with detection reliability  

As a result, **model selection based solely on metrics is insufficient for deployment decisions**.

---

## Metrics

Models are evaluated using:

- mAP (mean Average Precision)  
- mAR (mean Average Recall)  
- IoU (Intersection over Union)  
- precision and recall  

Additional behavior-aware metrics:

- small object recall  
- miss rate  
- duplicate detection rate  

Full results:
→ `results/metrics-summary.csv`

Detailed interpretation:
→ `results/notes.md`

---

## Dataset

The evaluation uses EO drone imagery derived from real-world video data.

A subset of 23 sequences was selected from the Anti-UAV dataset:
→ https://anti-uav.github.io/dataset/

Frames were extracted and curated to capture variation in:

- object distance and scale  
- visual representation  
- background complexity  

The resulting dataset contains **1,000 validated annotations** for a single class:

- drone  

Full details:
→ `dataset/description.md`

---

## Methodology

To ensure fair comparison:

- all models are trained on the same dataset split  
- preprocessing and augmentation are aligned  
- evaluation is performed on a shared validation set  

The evaluation protocol is designed so observed differences reflect model behavior, not experimental variation.

Full protocol:
→ `methodology/evaluation-protocol.md`

---

## Positioning Within IRIS

- Benchmark → structured comparison of model behavior  
- Experiments → analysis of behavior across conditions  
- Model Zoo → deployment of validated models  

---

<p align="center">
  <strong>IRIS is built for lifecycle-driven computer vision.</strong>
</p>
