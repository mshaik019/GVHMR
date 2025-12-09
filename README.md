Generative Video Human Mesh Recovery (GVHMR)

This repository contains the full implementation of Generative Video Human Mesh Recovery (GVHMR) — a complete video-to-3D mesh reconstruction pipeline that generates temporally consistent human meshes from standard RGB input videos. Unlike per-frame pose estimation approaches that produce jittery outputs, this project reconstructs a smooth, coherent 3D motion sequence and exports results in SMPL-X format for downstream applications.

This project was implemented with reference to the SIGGRAPH Asia 2024 paper
“World-Grounded Human Motion Recovery via Gravity-View Coordinates (GVHMR)” by Shen et al.
This README summarizes the full pipeline, architecture, techniques, datasets, implementation details, deployment challenges, and final deliverables.

Team Members

Mohammad Adil Shaik

Vamsi Aakash Samudrala

Sai Vishnu Sathwik Gurijala

Harshith Reddy Pasham

Rohan Siddharth Gudla

Abstract

We implemented GVHMR, an end-to-end framework that reconstructs a temporally consistent sequence of 3D human meshes from monocular RGB video. The goal was to overcome limitations of traditional per-frame prediction methods — which often suffer from jitter, drift, and incomplete geometry — to produce smooth, realistic 3D motion while preserving full-body shape. We generated mesh-overlaid videos for visual validation and exported SMPL-X mesh outputs for downstream usage.

1. Introduction

Reconstructing full-body 3D motion from monocular video is challenging due to:

Occlusions

Motion blur

Camera movement

Lighting variations

Depth ambiguity

Traditional frame-by-frame reconstruction lacks temporal coherence and often generates unstable mesh predictions.
To overcome this, we built a pipeline inspired by GVHMR that ensures:

Smooth temporal consistency

Dense, complete mesh geometry

Accurate global trajectories

Support for large videos (up to 5 GB)

2. Problem Statement

Given a single RGB video, reconstruct a full-body 3D mesh sequence parameterized in SMPL-X such that:

Motion is smooth and continuous

Geometry remains stable under occlusions or blur

Global translation and rotation are accurate

Output meshes are temporally consistent

Challenges include:

Fast motion and occlusion

Camera shaking or poor lighting

Depth ambiguity

Extremely large video inputs

3. What We Built

We implemented a complete GVHMR-based system capable of:

Extracting frame-wise features

Performing initial 3D mesh reconstruction

Applying transformer-based temporal modeling

Converting outputs into SMPL-X format

Rendering mesh-overlay videos for evaluation

This creates a fully functional 3D motion reconstruction pipeline suitable for animation, VR/AR, biomechanics, simulation, and research.

4. End-to-End Pipeline

Video Input

Feature Extraction (Pose, Visual Tokens)

Per-Frame Mesh Reconstruction

Temporal Generative Modeling (Transformers)

Gravity-View Coordinate Mapping

SMPL-X Mesh Conversion

Rendering & Mesh Overlay Video Generation

5. Architecture Overview

Our implementation mirrors the GVHMR architecture:

Early fusion of multi-modal tokens

Temporal transformer layers with relative positional encoding

Multitask MLP prediction heads

Gravity-View coordinate transformation

Root trajectory estimation

Dense 3D mesh decoding

SMPL-X output conversion

6. Key Techniques

Temporal Generative Modeling for long-range motion smoothing

Volumetric Mesh Reconstruction for robust geometry

SMPL-X Parameterization for standardized human modeling

Neural Rendering & Overlay Visualization for evaluation

7. Data & Dataset Usage
• Public Dataset

3DPW for outdoor, real-world evaluation

• Custom Large Videos (~5 GB each)

Collected under varied indoor/outdoor environments.

🔗 Input Folder Download Link

Due to size limitations, input videos and checkpoints are stored externally:

👉 Google Drive (Inputs + Checkpoints):
https://drive.google.com/drive/folders/1IonJr1S4dyqp0VGj-VlpfV0i_w0XQlwx?usp=sharing

📁 Input Files and Checkpoints Setup

Download the folder and place it inside:

GVHMR/inputs/

1️⃣ Input Videos (.mp4)

Place video files in:

GVHMR/inputs/


Example:

GVHMR/inputs/tennis.mp4
GVHMR/inputs/jumping.mp4
GVHMR/inputs/demo1.mp4

2️⃣ Model Checkpoints

Place pretrained weights here:

GVHMR/inputs/checkpoints/
GVHMR/inputs/ckpts/

✔️ Final Folder Structure Must Look Like
GVHMR/
├── docs/
├── hmr4d/
├── tools/
├── third-party/
├── README.md
├── GVHMR.ipynb
└── inputs/
      ├── tennis.mp4
      ├── walking.mp4
      ├── demo1.mp4
      ├── checkpoints/
      └── ckpts/

Set the Video Path in Notebook
VIDEO_PATH = "/content/GVHMR/inputs/tennis.mp4"

8. Implementation & Deployment Challenges

CUDA & PyTorch version conflicts

GPU memory limits

Path inconsistencies

Dependency conflicts requiring pinned versions

✔ All issues have been resolved inside GVHMR.ipynb.

📄 Direct Notebook Access (GVHMR.ipynb)

For easier execution and proof of results:

🔗 Google Colab Notebook:
https://colab.research.google.com/drive/1lG-S4v5tkoHNOg-OpI_-M8Ma3-yLHFDu?usp=sharing

9. How to Run (Using Google Colab)

Open GVHMR.ipynb in Colab

Switch runtime to GPU

Upload or mount the GVHMR/ folder

Ensure inputs/ contains videos & checkpoints

Set video path:

VIDEO_PATH = "/content/GVHMR/inputs/your_video.mp4"


Run all cells

Output files appear in:

outputs/

10. Project Folder Structure
GVHMR/
│
├── GVHMR.ipynb
├── preprocess/
├── scripts/
├── outputs/
├── sample_data/
└── README.md

11. Deliverables

Mesh-overlay videos

SMPL-X mesh exports

Full runnable notebook

GVHMR.zip source code

Input dataset (Google Drive link)

Complete documentation (README.md)

12. Reference to Original Paper
@inproceedings{shen2024gvhmr,
title = {World-Grounded Human Motion Recovery via Gravity-View Coordinates},
author = {Shen, Zehong and Pi, Huaijin and Xia, Yan and Cen, Zhi and Peng, Sida and Hu, Zechen and Bao, Hujun and Hu, Ruizhen and Zhou, Xiaowei},
booktitle = {SIGGRAPH Asia Conference Proceedings},
year = {2024}
}

13. Acknowledgements

We gratefully acknowledge the authors of:

GVHMR

WHAM

4D-Humans

ViTPose-Pytorch

Their open-source contributions formed the backbone of this project.

Contact

📧 Email: mshaik10@charlotte.edu

👤 Team Lead: Mohammad Adil Shaik