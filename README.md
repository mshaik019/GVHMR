

# **Generative Video Human Mesh Recovery (GVHMR)**

This repository contains the full implementation of **Generative Video Human Mesh Recovery (GVHMR)** — a complete video-to-3D mesh reconstruction pipeline that generates **temporally consistent human meshes** from standard RGB input videos. Unlike per-frame pose estimation approaches that produce jittery outputs, this project reconstructs a **smooth, coherent 3D motion sequence** and exports results in **SMPL-X format** for downstream applications.

This project was implemented with reference to the **SIGGRAPH Asia 2024 paper**
**“World-Grounded Human Motion Recovery via Gravity-View Coordinates (GVHMR)”** by Shen et al.
This README summarizes the full pipeline, architecture, techniques, datasets, implementation details, deployment challenges, and final deliverables.

---

## **Team Members**

* **Mohammad Adil Shaik**
* **Vamsi Aakash Samudrala**
* **Sai Vishnu Sathwik Gurijala**
* **Harshith Reddy Pasham**
* **Rohan Siddharth Gudla**

---

## **Abstract**

We implemented GVHMR, an end-to-end framework that reconstructs a **temporally consistent sequence of 3D human meshes** from monocular RGB video. The goal was to overcome limitations of traditional per-frame prediction methods — which often suffer from jitter, drift, and incomplete geometry — to produce **smooth, realistic 3D motion** while preserving full-body shape. We generated mesh-overlaid videos for visual validation and exported SMPL-X mesh outputs for downstream usage.

---

# **1. Introduction**

Reconstructing full-body 3D motion from monocular video is challenging due to:

* Occlusions
* Motion blur
* Camera movement
* Lighting variations
* Depth ambiguity

Traditional frame-by-frame reconstruction lacks temporal coherence and often generates unstable mesh predictions.

Our GVHMR-based pipeline ensures:

* **Smooth temporal consistency**
* **Dense, complete mesh geometry**
* **Accurate global trajectories**
* **Support for videos up to 5GB**

---

# **2. Problem Statement**

Given a single RGB video, reconstruct a **full-body 3D mesh sequence** parameterized in **SMPL-X** such that:

* Motion is smooth and continuous
* Geometry remains stable even under occlusions or blur
* Global translation and rotation are accurate
* Output meshes are temporally consistent

**Key challenges:**

* Fast motion & occlusion
* Camera shaking
* Lighting variation
* Extremely large input videos

---

# **3. What We Built**

Our GVHMR-based system performs:

* Frame-wise feature extraction
* Initial per-frame 3D mesh reconstruction
* Transformer-based temporal smoothing
* SMPL-X export
* Mesh-overlay video rendering

This creates a fully functional reconstruction pipeline for **VR/AR, graphics, animation, and research**.

---

# **4. End-to-End Pipeline**

1. **Video Input**
2. **Feature Extraction**
3. **Per-Frame Mesh Reconstruction**
4. **Temporal Generative Modeling**
5. **Gravity-View Coordinate Mapping**
6. **SMPL-X Mesh Conversion**
7. **Rendering & Overlay Video Generation**

---

# **5. Architecture Overview**

The architecture includes:

* Early fusion of multi-modal tokens
* Temporal transformer layers
* Multitask MLP prediction heads
* Gravity-View coordinate transformation
* Root trajectory estimation
* Dense 3D mesh decoding
* SMPL-X output conversion

---

# **6. Key Techniques**

* **Temporal Generative Modeling**
* **Volumetric Mesh Reconstruction**
* **SMPL-X Parameterization**
* **Neural Rendering for mesh overlays**

---

# **7. Data & Input Setup**

We tested using:

### **Public dataset**

* 3DPW (outdoor real-world sequences)

### **Custom videos (~5GB each)**

Indoor + outdoor motion videos.

---

## 🔗 **Input Folder Download Link**

Because of repository size limits, all input videos + checkpoints are hosted on Google Drive:

👉 **Download Inputs & Checkpoints:**
[https://drive.google.com/drive/folders/1IonJr1S4dyqp0VGj-VlpfV0i_w0XQlwx?usp=sharing](https://drive.google.com/drive/folders/1IonJr1S4dyqp0VGj-VlpfV0i_w0XQlwx?usp=sharing)

---

## **📁 Input Files & Checkpoints Setup**

Place the downloaded folder inside:

```
GVHMR/inputs/
```

### **1️⃣ Input Videos (.mp4)**

Examples:

```
GVHMR/inputs/tennis.mp4
GVHMR/inputs/jumping.mp4
GVHMR/inputs/demo1.mp4
```

### **2️⃣ Checkpoints**

Place pretrained weights here:

```
GVHMR/inputs/checkpoints/
GVHMR/inputs/ckpts/
```

---

## ✔️ **Correct Final Folder Structure**

```
GVHMR/
├── docs/
├── hmr4d/
├── tools/
├── third-party/
├── GVHMR.ipynb
├── README.md
└── inputs/
      ├── tennis.mp4
      ├── walking.mp4
      ├── demo1.mp4
      ├── checkpoints/
      └── ckpts/
```

### **Set video path in notebook:**

```python
VIDEO_PATH = "/content/GVHMR/inputs/tennis.mp4"
```

---

# **8. Implementation & Deployment Challenges**

* CUDA + PyTorch mismatches
* GPU memory limitations
* Path inconsistencies
* Dependency conflicts

All resolved in **GVHMR.ipynb**.

---

# **📄 Direct Notebook (Colab Link)**

Open the full runnable notebook here:

👉 [https://colab.research.google.com/drive/1lG-S4v5tkoHNOg-OpI_-M8Ma3-yLHFDu?usp=sharing](https://colab.research.google.com/drive/1lG-S4v5tkoHNOg-OpI_-M8Ma3-yLHFDu?usp=sharing)

---

# **9. How to Run (Colab)**

1. Open notebook in Colab
2. Enable **GPU** runtime
3. Upload or mount the GVHMR folder
4. Ensure `inputs/` contains videos & checkpoints
5. Set video path
6. Run all cells
7. Outputs appear in:

```
outputs/
```

---

# **10. Folder Structure**

```
GVHMR/
├── GVHMR.ipynb
├── preprocess/
├── scripts/
├── outputs/
├── sample_data/
└── README.md
```

---

# **11. Deliverables**

* Mesh-overlay output videos
* SMPL-X mesh exports
* Fully runnable Colab notebook
* GVHMR.zip code
* Dataset download link
* Complete documentation

---

# **12. Reference**

```bibtex
@inproceedings{shen2024gvhmr,
title = {World-Grounded Human Motion Recovery via Gravity-View Coordinates},
author = {Shen, Zehong and Pi, Huaijin and Xia, Yan and Cen, Zhi and Peng, Sida and Hu, Zechen and Bao, Hujun and Hu, Ruizhen and Zhou, Xiaowei},
booktitle = {SIGGRAPH Asia Conference Proceedings},
year = {2024}
}
```

---

# **13. Acknowledgements**

* GVHMR
* WHAM
* 4D-Humans
* ViTPose-Pytorch

---

# **Contact**

📧 **[mshaik10@charlotte.edu](mailto:mshaik10@charlotte.edu)**
👤 **Team Lead: Mohammad Adil Shaik**

---
