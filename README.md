Computer Vision Semester Project 

Deep Vision Pipeline for Brain Tumor MRI Analysis

This project implements an end-to-end computer vision pipeline on the BraTS-PED brain tumor MRI dataset. The work covers radiometric preprocessing, noise mitigation, structural masking, texture feature extraction, traditional machine learning classification, and CNN-based deep learning recognition.

The pipeline follows:

Acquisition → Preprocessing → Segmentation → Description → Recognition
Project Overview

Medical MRI images require careful preprocessing before they can be used for segmentation, feature extraction, and deep learning. This project uses 3D pediatric brain tumor MRI volumes stored in .nii.gz format and converts selected slices into 2D images for computer vision processing.

The project is divided into four major parts:

    Assignment 1: Radiometric preprocessing and noise mitigation
    Assignment 2: Mid-level structural representation and masking
    Assignment 3: Statistical texture analysis and traditional classification
    Final Project: Deep vision pipeline using CNN-based tumor classification

Dataset

The dataset used is the BraTS-PED brain tumor MRI dataset.

Each patient folder contains MRI modalities such as:

    t1n — T1 native MRI
    t1c — T1 contrast-enhanced MRI
    t2w — T2 weighted MRI
    t2f — T2-FLAIR MRI
    seg — segmentation mask

The dataset is stored as 3D MRI volumes in .nii.gz format. For image processing tasks, representative 2D slices are extracted from each volume.
Project Pipeline
1. Acquisition

MRI files are loaded from patient folders using the nibabel library. Each .nii.gz file is read as a 3D volume.
2. Preprocessing

The selected MRI slices are normalized into 8-bit grayscale images for visualization and filtering. Noise mitigation is performed using:

    Mean filter
    Gaussian filter
    Median filter

The filtering results are evaluated using:

    PSNR
    SSIM

Anti-aliasing is also applied before downsampling using Gaussian pre-filtering.
3. Segmentation and Masking

Tumor regions are extracted using edge detection and segmentation masks. The project applies:

    Sobel edge detection
    Canny edge detection
    Binary mask generation
    Morphological cleaning

Morphological operations include:

    Erosion
    Dilation
    Opening
    Closing

4. Boundary Representation

The cleaned tumor masks are used to extract object boundaries. Boundary representation includes:

    8-directional chain code
    First difference
    Shape number
    Convex hull using Graham Scan

5. Statistical Feature Extraction

Texture and geometric features are extracted from masked tumor regions.

GLCM texture features:

    Energy
    Entropy
    Contrast

Geometric features:

    Area
    Centroid
    Perimeter
    Circularity

These features are saved as a feature vector CSV file.
6. Traditional Classification

A Random Forest classifier is trained using handcrafted texture and geometric features. The model generates:

    Accuracy score
    Precision
    Recall
    F1-score
    Confusion matrix

7. Deep Learning Recognition

A CNN model is used for tumor vs no-tumor slice classification. The model is trained on selected MRI slices and evaluated using:

    Accuracy
    Precision
    Recall
    Confusion matrix
    Training and validation curves

Repository Structure

deep-vision-brain-tumor-mri/
│
├── notebooks/
│   └── 231140_220444_cvproj.ipynb
│
├── reports/
│   └── deep_vision_pipeline_research_report.docx
│
├── assignment_1_outputs/
│   ├── before_after_dataset/
│   ├── anti_aliasing_examples/
│   ├── bit_depth_summary.csv
│   └── metrics/
│
├── assignment_2_outputs/
│   ├── masks/
│   ├── morphological_cleaning/
│   ├── chain_code_tables/
│   ├── convex_hull_overlays/
│   └── assignment_2_summary.csv
│
├── assignment_3_outputs/
│   ├── feature_vectors/
│   ├── classification_report/
│   └── plots/
│
├── final_project_outputs/
│   ├── final_annotated_dataset/
│   ├── train_test_dataset/
│   ├── evaluation_report/
│   ├── plots/
│   └── cnn_tumor_classifier.h5
│
├── requirements.txt
└── README.md

