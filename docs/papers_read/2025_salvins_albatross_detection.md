# Automated Detection of Salvin's Albatrosses (2025) — Notes

📄 **Paper**: [arXiv:2505.10737](https://arxiv.org/abs/2505.10737)

## 1. What Problem Is This Paper Solving?
- Manual counting of seabirds from drone imagery is extremely time-consuming.  
- Field conditions make direct surveying difficult, dangerous, or unreliable.  
- The goal: evaluate how BirdDetector (pretrained), SAHI, and fine-tuning improve detection of Salvin’s albatross in aerial orthomosaics.

**Why this matters:**  
Seabird population estimates are foundational for conservation decisions in vulnerable species.

---

## 2. Data Used
- Orthomosaic drone imagery from the Bounty Islands (8 islands).  
- Labels: point annotations → converted to 50×50 px bounding boxes.  
- Each island = slightly different habitat, lighting, and rock texture.  
- Dataset size: ~66,600 birds detected manually.

Key factors:
- Noisy labels  
- Domain shift between islands  
- Tiny birds relative to image size  

---

## 3. Methods
### Models
- BirdDetector (RetinaNet + ResNet-50 backbone)  
- SAHI for small-object slicing  
- Fine-tuning with augmentations

### Preprocessing
- Tiling large orthomosaics into 1500×1500 chips  
- Creating pseudo-boxes from point annotations  

### Evaluation
- Leave-One-Island-Out validation  
- Precision, recall, F1  
- IoU threshold of 0.1 (accommodating noisy box boundaries)

---

## 4. Key Findings
- Zero-shot BirdDetector works *but* misses many birds.  
- SAHI dramatically improves detection of tiny birds,
- Fine-tuning boosts recall significantly.  
- Fine-tuning + SAHI = best overall model.  
- False positives come from rocks, shadows, and penguins.  
- Habitat differences (texture, lighting) are major sources of model error.

---

## 5. Technical Takeaways for My Work
- SAHI improves small-object detection in huge drone images by slicing the image into smaller tiles, running detection on each tile, then stitching the results back together. This makes tiny birds appear larger relative to the input size, letting the model detect them more reliably.SAHI is extremely useful for drone imagery. Because:
    - orthomosaics are HUGE
    - birds are TINY
    - BirdDetector is NOT a multi-scale model like YOLOv8
    - RetinaNet really struggles with tiny objects
    - SAHI rescues the detector.
    In the paper, SAHI:
    - increased recall
    - found more birds
    - improved F1
    - reduced missed detections
- Fine-tuning requires careful augmentations to simulate habitat variation.  
- LOIOCV is a strong strategy for ecological generalization.  
- Background complexity matters as much as the model. Using all tiles introduces habitat representation bias: islands with more tiles influence the model disproportionately, leading to uneven learning of background patterns. However, because ecological datasets are naturally imbalanced, this choice provides a realistic test of model performance in practical deployment scenarios.
- Noisy pseudo-labels → use lower IoU thresholds: The evaluation thresholds were intentionally loosened because both the dataset and the labeling method introduce unavoidable noise. Low IoU and confidence thresholds improve recall, while the extremely low NMS threshold prevents double-counting birds in overlapping slices. This balanced strategy respects ecological priorities: undercounts are far worse than occasional false positives.

---

## 6. Ecological Insights
- Accurate seabird counts = essential for conservation monitoring.  
- Drones reduce human disturbance.  
- Automated detection improves scalability and consistency.  
- False positives inflate population estimates; false negatives hide declines.

---

## 7. My Questions for Later
- How adaptable is BirdDetector to Chilean seabirds?  
- How can I incorporate a species classifier?  
- Can I gather or curate a Chile-specific aerial dataset?  
- How does habitat shift affect generalization?  
- How to choose augmentations that mimic real-world ecology?
