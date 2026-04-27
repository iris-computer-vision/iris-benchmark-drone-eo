# Evaluation Notes

This benchmark highlights differences in model behavior that are not fully captured by aggregate metrics. Observations below are based on repeated inspection across validation samples.

---

## YOLOv8 (Small)

YOLOv8s demonstrated the most stable generalization across evaluated conditions.

- no missed detections observed across validation samples  
- no significant localization instability  
- consistent performance across distance and cluttered environments  

The primary limitation is reduced confidence in more challenging conditions:

- confidence scores frequently decreased into the low 70% range  
- this effect was most pronounced at long range and in cluttered scenes  

Despite lower confidence, detections remained consistent and reliable.

---

## YOLOv8 (Large)

YOLOv8l showed improved sensitivity to distant objects relative to the small variant.

- stronger detection performance at range  
- improved confidence in challenging scenarios  

However, this came with tradeoffs:

- instances of duplicate detection in cluttered backgrounds  
- occasional localization instability  

This suggests increased sensitivity at the cost of precision under complex conditions.

---

## YOLOv11 (Small)

YOLOv11s showed measurable improvements in confidence over YOLOv8s.

- higher confidence scores across distance and background variation  
- improved IoU (97.2 vs 96.5 for YOLOv8s)  

Aggregate performance remained similar:

- mAP: 89.5 vs 89.7 (YOLOv8s)  
- other metrics largely equivalent  

Overall, YOLOv11s provides incremental improvement in localization and confidence while maintaining stable behavior.

---

## RT-DETR (Large)

RT-DETR exhibited strong detection confidence, particularly under difficult conditions.

- high confidence at distance and in cluttered environments  
- strong recall across evaluated scenarios  

However, several consistent issues were observed:

- duplicate detections on the same target  
- reduced localization precision relative to YOLO models (lower IoU)  

The duplicate detection behavior was the primary factor impacting overall performance.

Inference time was also higher than YOLO variants:

- ~4 ms slower than YOLO small models  
- ~2.3 ms slower than YOLO large  

---

## Faster R-CNN (ResNet50 FPN v2)

Faster R-CNN produced the highest confidence detections under favorable conditions.

- confidence frequently reached 99–100% in cluttered and low-light environments  
- strong precision when objects were clearly visible  

However, a consistent failure mode was observed:

- all instances of the drone at long range were missed  
- no successful detections were recorded at extended distance  

This failure mode was repeatable across validation samples and represents a significant limitation for long-range detection tasks.

Additionally:

- inference time was significantly higher than all other evaluated models  

---

## Cross-Model Observations

Across all architectures:

- performance degraded as object size decreased  
- background complexity impacted localization stability  
- confidence scores did not consistently reflect detection reliability  

Key differentiators between models were:

- recall at distance  
- susceptibility to duplicate detection  
- localization stability under clutter  

---

## Summary

Aggregate metrics alone do not fully explain model performance.

Observed differences in behavior were:

- consistent across validation samples  
- specific to model architecture  
- directly relevant to deployment scenarios  

These findings reinforce the need to evaluate models based on behavior under real-world conditions, not solely on summary metrics.
