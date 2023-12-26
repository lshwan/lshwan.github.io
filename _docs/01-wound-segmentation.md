---
title: "AiD Regen: 2D Diabetic Foot Ulcer Segmentation"
permalink: /docs/wound-segmentation/
last_modified_at: 2023-12-24
classes: wide
---

Accepted to [CVPR 2022](https://openaccess.thecvf.com/content/CVPR2022/html/Chae_Generating_3D_Bio-Printable_Patches_Using_Wound_Segmentation_and_Reconstruction_To_CVPR_2022_paper.html)

## Introduction

I have developed a system that generates 3D wound models by combining 2D semantic segmentation with 3D reconstruction. This enables the models to be printed using 3D bio-printers during surgeries for treating diabetic foot ulcers (DFUs).

The 2D segmentation module, based on a deep learning model, is designed to simplify the surgical process and minimize the complexities involved in the drawing process of wound areas.

<figure>
  <img src="{{ '/assets/images/dfu-procedure.png' | relative_url }}" >
</figure>


## Dataset

Our business team has collected 818 DFU images from global clinical studies. I established a collaborative labeling pipeline to ensure high-quality labels.

Since we aimed to capture real-world data without controlling the photo capturing process, our dataset exhibits three types of imbalances:

1. The number of images per patient varies significantly; approximately half of the images are from just 11 of the 67 patients.
2. Clinical complications, such as heavy bleeding, are infrequent but crucial for the model's performance.
3. DFU areas are sparsely represented in images, constituting only 3.4% of the total pixels.

## Data Preprocessing Pipeline

To address these imbalances, I developed a preprocessing pipeline:

1. I implemented a deterministic oversampling method to balance the number of images per patient. (S2)
2. A separate oversampling process was conducted to balance images of bleeding and non-bleeding wounds. (S3)
3. I randomly sampled 256 x 256 sized patches of wound and background images, ensuring that a quarter of the patches contained wound samples.

## Model Design

I opted for a CNN-based model, DeepLabv3, enhanced with a scale attention mechanism. The choice of a CNN-based model was driven by its data-efficient characteristics on small datasets. Additionally, I incorporated an attention mechanism to preserve details of wound boundaries. 

<figure>
  <img src="{{ '/assets/images/wound-segmentation-model.png' | relative_url }}">
</figure>

## Human-In-The-Loop Interaction

Deep learning models can sometimes yield unpredictable predictions, which can be critical in the risk-sensitive medical field. Furthermore, clinical decisions during operations often vary among clinicians.

To address this, I designed a Human-In-The-Loop (HITL) user interaction system to manage inter-operator variability and maximize model performance, including:

1. Seed point declaration to clarify the target wound area.
2. Adaptive thresholding for semantic expansion or shrinkage of the wound boundary.
3. Manual drawing or modification.

<figure>
  <img src="{{ '/assets/images/human-in-the-loop.png' | relative_url }}">
</figure>

## Performences

- The scale attention machanism outperforms the native DeepLabV3 model (DeepLabV3 vs. Our model).
- The data preprocessing pipeline proves effective in improving segmentation accuracy. (S2, S3). 
- Human-AI-interaction futher improves the performences and enhances clinical customizability (HITL).

<figure>
  <img src="{{ '/assets/images/model-performances.png' | relative_url }}">
</figure>