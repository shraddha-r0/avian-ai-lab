# 🐦 Bird Detector Lab  
**A hands-on exploration of BirdDetector, SAHI slicing, and fine-tuning on public aerial bird datasets.**

This project is my practical sandbox for applying machine learning to drone imagery of birds, inspired by ecological ML research.  
It demonstrates zero-shot inference, SAHI slicing for small-object detection, fine-tuning using point annotations or boxes, and species classification.

---

## 📘 What This Project Contains

### 1. Zero-Shot BirdDetector
- Run pretrained BirdDetector (DeepForest)
- Test on a chosen public dataset
- Visualize predictions
- Evaluate precision, recall, F1

### 2. SAHI Inference
- Slice large drone images into windows
- Run detection per slice
- Merge predictions
- Compare results vs no-SAHI

### 3. Fine-Tuning BirdDetector
- Load public dataset
- Convert point annotations → pseudo-boxes (if needed)
- Train with augmentations
- Evaluate using IoU=0.1

### 4. Species Classification
- Add a classifier head or a separate model
- Train on cropped detections
- Evaluate per-species accuracy

### 5. End-to-End Pipeline
- Detection + classification + metrics
- Visual summaries
- Ecological interpretation

---

## 📁 Folder Breakdown

- `notebooks/` — experiments in Jupyter  
- `models/` — inference + training scripts  
- `utils/` — tiling, visualization, metrics  
- `data/` — local data (ignored from git)  
- `results/` — saved outputs + figures  

---

## 🧠 Goals
- Understand how BirdDetector behaves in real ecological conditions  
- Learn SAHI slicing for small-object detection  
- Practice fine-tuning with noisy labels  
- Build skills for conservation ML research  
- Create a polished, portfolio-ready project  

---

## 📄 License  
MIT License