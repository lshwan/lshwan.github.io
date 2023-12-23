---
title: "AiD Regen: 2D Diabetic Foot Ulcer Segmentation"
permalink: /docs/wound-segmentation/
last_modified_at: 2023-12-24
classes: wide
---

## Introduction

I've developed a system that generates 3D wound models combining 2D semantic segmentation with 3D reconstruction so that they can be printed via 3D bio-printers during the surgery to treat diabetic foot ulcers (DFUs).   

The 2D segmentation module based on deep learning model aims to simplify the surgery process and reduce difficulties of elaborate drawing of wound area.

<figure>
  <img src="{{ '/assets/images/dfu-procedure.png' | relative_url }}" >
</figure>


## Dataset

Our business team collected 818 DFU images from global clinical studies. I built colaborative labeling pipeline for high-quality label.

As we did not control the photo capturing process in order to gather real-world data, the dataset contains three different types of imbalances.

1. The number of images per patient highly varies; about half of the images are from 11 out of 67 patients.
2. Clinical complications such as heavy bleeding are rare; there are crucial to the model perfomances.
3. DFU areas are sparse in images; only 3.4% of the total pixels are classified as DFU.

## Data Preprocessing Pipeline

I designed a preprocessing pipeline to handle the imbalances of the dataset.

1. In order to balance the number of images per patient, I applied a deterministic oversampling
method. (S2)
2. I performed another oversampling to balance bleeding and non-bleeding wound images. (S3)
3. I randomly sampled 256 X 256 sized wound and background image patches, guaranteeing a quarter of the patches to be wound samples.

## Model

I used a CNN-based model, DeepLabv3, and advanced with scale attention mechanism to it. The choice of the CNN-based model was origined by their data-efficient characteristics on small datasets. I also applied the attention mechanism to preserve details of wound boundaries. 

<figure>
  <img src="{{ '/assets/images/wound-segmentation-model.png' | relative_url }}">
</figure>

## Human-In-The-Loop Interaction

Deep learning model might occasionally produce unexpected predictions; however, such errors can be disastrous in the risksensitive medical field. Moreover clinical decisions during operation often vary from clinician to clinician. I designed a HITL user interaction to handle inter-operator variability. It consists of three major interactions.

1. Seed point declaration to clarify the target wound.
2. Adaptive thresholding to sementically expand or shirink the wound boundary.
3. Manual drawing or modification.

<figure>
  <img src="{{ '/assets/images/human-in-the-loop.png' | relative_url }}">
</figure>

## Performences

- The scale attention machanism outperforms the native DeepLabV3 model (DeepLabV3 vs. Our model).
- The data preprocessing pipeline shows their effectiveness on segmentation performances (S2, S3). 
- Human-AI-interaction futher improves the performences and enhances clinical customizability (HITL).

<figure>
  <img src="{{ '/assets/images/model-performances.png' | relative_url }}">
</figure>