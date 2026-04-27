# Evaluation Notes

This benchmark highlights differences in model behavior not fully captured by aggregate metrics.

All observations are derived from repeated inspection across validation samples.

---

## Key Observations

### YOLOv8 (Small)

- no missed detections observed  
- 1 duplicate detection instance  
- stable localization across conditions  

Primary limitation:
- reduced confidence at long range and in clutter  

---

### YOLOv8 (Large)

- improved detection at distance  
- 5 false positives in cluttered backgrounds  
- 1 duplicate detection with degraded localization  

---

### YOLOv11 (Small)

- similar behavior to YOLOv8s  
- higher confidence and improved IoU  
- 1 duplicate detection at distance with stable localization  

---

### RT-DETR (Large)

- strong recall and high confidence  
- effective under clutter and distance  

Observed issue:
- 1 duplicate detection in clutter  

Localization remained strong.

---

### Faster R-CNN

- highest confidence detections in favorable conditions  
- strong performance in clutter and low light  

Observed failure mode:
- 8 missed detections  
- all failures occurred at long range  

No duplicate detections or false positives observed.

---

## Cross-Model Patterns

- recall at distance is the primary differentiator  
- duplicate detection occurs in multiple architectures under clutter  
- false positives increase with sensitivity to background variation  
- confidence does not reliably indicate robustness  

---

## Summary

Aggregate metrics alone do not fully explain model performance.

Behavioral differences are:

- consistent across validation samples  
- architecture-dependent  
- directly relevant to deployment scenarios

| Model        | Misses | False Positives | Duplicate Detections | Notes |
|-------------|--------|----------------|----------------------|-------|
| YOLOv8s     | 0      | 0              | 1                    | Stable localization |
| YOLOv8l     | 0      | 5              | 1                    | Localization degraded in duplicate case |
| YOLOv11s    | 0      | 0              | 1                    | Similar to YOLOv8s |
| RT-DETR     | 0      | 0              | 1                    | Strong localization |
| Faster R-CNN| 8      | 0              | 0                    | All misses at distance |
