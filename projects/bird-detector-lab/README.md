# 🐦 Bird Detector Lab  
**Exploring practical approaches to bird detection in real-world ecological data, including what works, what breaks, and why.**

This project is my practical sandbox for applying machine learning to bird detection in aerial and non‑aerial imagery, inspired by ecological ML research.  
It is **not** just a “look, it runs” demo — it is a record of **attempts, dead ends, and working paths** when trying to do bird detection with imperfect, evolving tools.

The goal is to think and work like a researcher:
- try plausible approaches,
- see where they fail in practice,
- document those failures clearly,
- and then design better, more realistic pipelines.

---

## 📘 What This Project Currently Contains (and Learns From)

### 1. DeepForest + BirdDetector Attempt (Drone Imagery)

**Status:** ❌ Abandoned as a primary path, kept for lessons learned.

- Tried to use DeepForest + BirdDetector for drone bird detection, following older papers and repos.
- Ran into:
  - severe version conflicts (Python, torch, albumentations),
  - outdated APIs (`use_bird_detector`, `load_model`),
  - missing or shifting model weights,
  - confusing, hard‑coded labels (`Tree`) despite loading bird weights.
- **Key takeaway:** older academic code can be extremely brittle; reproducing results often requires pinning old environments and manually loading weights. This is valuable to know, but not a good foundation for a modern portfolio project.

I’m keeping notes and minimal code from this attempt as a **“what went wrong and why”** case study.

---

### 2. Hugging Face Bird Models (Non‑Drone, Species‑Level)

**Status:** ⚠️ Informative but not directly suitable for drone imagery.

- Explored using models like `weecology/everglades-bird-species-detector` from Hugging Face.
- These models:
  - are trained mostly on ground‑level or non‑orthomosaic imagery,
  - do provide species labels and clean APIs,
  - but don’t straightforwardly transfer to high‑altitude drone imagery where birds are tiny.
- **Key takeaway:** even when a model is “for birds” and “for detection”, domain shift (viewpoint, scale, background, resolution) makes direct reuse non‑trivial.

These experiments helped sharpen my understanding of **domain shift** and why “just grab a HF model” is rarely enough in ecology.

---

## 🧪 What This Lab Is Moving Toward

Instead of pretending there is a single perfect plug‑and‑play model for drone birds (there isn’t), this lab is evolving toward:

- **Realistic pipelines** that combine:
  - a general wildlife detector (e.g., MegaDetector or YOLO‑based models),
  - SAHI or tiling for small objects,
  - optional species classifiers on cropped detections.
- **Transparent documentation** of:
  - which models were tried,
  - under what conditions they break,
  - and what I would do next to make them work in practice.
- **Reproducible notebooks** where:
  - environment assumptions are explicit,
  - limitations are acknowledged instead of hidden.

Future notebooks will likely be renamed and reorganized around this idea:
- `01_exploratory_detection.ipynb` – trying different detectors on a small set of images.
- `02_sahi_and_tiling.ipynb` – inspecting how slicing affects small bird detection.
- `03_realistic_pipeline.ipynb` – combining a working detector + post‑processing.

---

## 📁 Folder Breakdown (Conceptual)

- `notebooks/` — experiments and exploratory analysis (including failed/abandoned paths, clearly marked).  
- `models/` — wrappers around whatever detector(s) I end up using (e.g., HF models, YOLO, MegaDetector).  
- `utils/` — tiling, visualization, metrics helpers.  
- `data/` — local data (ignored from git).  
- `results/` — saved visualizations, logs, and comparison outputs.

---

## 🧠 Higher‑Level Goals

- Understand **why** drone bird detection is hard (tiny objects, noisy labels, habitat shift).
- Experience first‑hand the **friction of working with academic ML code**.
- Build a habit of documenting:
  - what I tried,
  - what broke,
  - what I learned,
  - and how I’d design a better next iteration.
- Slowly converge on a **robust, modern, reproducible bird‑detection pipeline** that I’d be comfortable showing to a conservation‑tech employer.

---

## 📄 License  

MIT License