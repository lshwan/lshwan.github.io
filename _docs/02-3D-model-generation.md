---
title: "AiD Regen: 3D Bioprintable Patch Generation"
permalink: /docs/3d-model-generation/
last_modified_at: 2023-12-26
classes: wide
---

## Introduction

I have developed a system that generates 3D wound models by combining 2D semantic segmentation with 3D reconstruction. This enables the models to be printed using 3D bio-printers during surgeries for treating diabetic foot ulcers (DFUs).

Following the delineation process in [2D Diabetic Foot Ulcer Segmentation](/docs/wound-segmentation), I merge the outlined wound boundary with the depth map to create a 3D reconstructed, bioprintable patch model.

<figure>
  <img src="{{ '/assets/images/dfu-procedure.png' | relative_url }}" >
</figure>

The effectiveness of the 3D reconstruction is evaluated based on two critical metrics:
1. Surface Area Accuracy: Ensuring the printed patch covers the entire wound area.
2. Shape Retention: Facilitating clinicians in easily aligning the patch with the wound.

## Dataset

The dataset consists of two distinct components:

1. **Synthetic Dataset for Quantitative Evaluation**: This dataset is used for the quantitative evaluation of surface area. It employs SeedMarkers to construct surface geometries of arbitrary shapes with known ground truth areas.
    <figure> 
        <img src="{{ '/assets/images/synthetic-dataset.png' | relative_url }}" > 
    </figure>

2. **Real-World Dataset from Clinical Trials for Qualitative Evaluation**: This dataset comprises images captured during surgeries using our system. It offers a diverse range of clinical scenarios and operation room environments. However, it lacks the ability to provide ground truth measurements for wound areas.


## Limitation of Depth Camera

Prior to the 3D reconstruction algorithm, an assessment of the depth camera's limitations was conducted:
1. **Distance Limitation**: Objects positioned farther than 30cm from the camera exhibit depth inaccuracies.
2. **Angle Limitation**: A tilting angle greater than 30° leads to depth inaccuracies.
3. **Environmental Factors**: Reflective and transparent objects, distant backgrounds, and thick mediums (e.g., water) on the object's surface severely impair depth measurement by hindering normal IR pattern reflection.

To mitigate these limitations, I focused on addressing the third issue, while system restrictions (e.g., limiting capture distance) were implemented to handle the first two, due to their irreversible nature and lack of error correction cues.


## Depth Error Correction and Meshing

After employing the projection from depth pixel to point cloud and constrained Delaunay triangulation, The process of depth error correction involves two key steps:

1. **Outlier Detection**: Outliers in the point cloud, often sparse in 3D space and forming triangles with larger areas, are detected and isolated.
2. **Outlier Compansation**: A surface fitting method is employed to create a surface function using inliers. Subsequently, outliers are adjusted to align with this surface, optimizing along the camera ray using the least mean square method.

This mesh cleaning process not only significantly improves area accuracy but also remarkably retains the surface shape.

<figure> 
    <img src="{{ '/assets/images/mesh-cleaning.png' | relative_url }}" > 
</figure>

## Flattening the Mesh

Flattening the mesh is a crucial step in enhancing the printability of liquid-type bioink. It eliminates the need for supports and prevents the material from flowing down along surface curves during printing.

To achieve this flattening, I utilized Principle Component Analysis (PCA) to identify the least significant axis of the surface mesh and then compressed along this axis. 

This method effectively flattens the mesh but can sometimes lead to the loss of important information, particularly in cases of wounds with significant curvature.

Recognizing this limitation, I am exploring alternative flattening algorithms, such as Angle Based Flattening (ABF) and Boundary First Flattening (BFF), to better preserve the critical features of more complex wound shapes.

## Performances

1. Quantitative Results
    - The mesh cleaning process notably enhances area accuracy.
    - The flattening step, while effective, results in a slight loss of information, thereby reducing accuracy.
    
    <figure> 
        <img src="{{ '/assets/images/3d-performances.png' | relative_url }}" > 
    </figure>

2. Qualitative Result
  - Due to privacy considerations, I am presenting the results using mockups.

    <figure> 
        <img src="{{ '/assets/images/3d-qualitative-result.png' | relative_url }}" > 
    </figure>

