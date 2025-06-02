# 🌄 Image Panorama Stitching

A Python implementation of automatic image panorama stitching using feature detection, matching, and homography estimation. This project creates seamless panoramic images from a sequence of overlapping photographs.

## ✨ Features

- **Harris Corner Detection**: Robust feature point detection using the Harris corner detector
- **Adaptive Non-Maximal Suppression (ANMS)**: Intelligent selection of the most significant corner points
- **Feature Description**: 8x8 Gaussian-blurred patch descriptors for robust matching
- **Feature Matching**: Distance-based matching with ratio testing for reliability
- **RANSAC Homography Estimation**: Robust homography computation to handle outliers
- **Image Blending**: Seamless panorama creation with perspective transformation

## 🔍 Algorithm Overview

### 1. Feature Detection
- Uses Harris corner detector to identify key points in each image
- Applies Adaptive Non-Maximal Suppression to select the best corners
- Extracts the top 500 strongest corners for each image

### 2. Feature Description
- Creates 40x40 pixel patches around each corner point
- Applies Gaussian blur (σ = 0.5) for noise reduction
- Resizes patches to 8x8 for computational efficiency
- Normalizes patches by subtracting mean and dividing by standard deviation

### 3. Feature Matching
- Computes Euclidean distances between feature descriptors
- Uses Lowe's ratio test (threshold = 0.75) to filter reliable matches
- Eliminates ambiguous matches to improve robustness

### 4. Homography Estimation
- Employs RANSAC algorithm with 1000 iterations
- Randomly samples 4 point correspondences to compute candidate homographies
- Uses distance threshold of 5 pixels to determine inliers
- Selects the homography with the maximum number of inliers

### 5. Image Blending
- Computes optimal canvas size based on transformed image boundaries
- Applies perspective transformations to align images
- Blends images using OpenCV's warping functions

## 📋 Requirements

```
opencv-python
numpy
matplotlib
```

## Installation

```bash
pip install opencv-python numpy matplotlib
```

## 📁 Usage

1. ** Prepare your images**: Place your overlapping images in directories:
   ```
   images/
   ├── set1/
   │   ├── image1.jpg
   │   ├── image2.jpg
   │   └── image3.jpg
   ├── set2/
   └── set3/
   ```

2. ** Run the script**

3. ** View results**: The script generates visualizations showing:
   - Detected feature points on each image
   - Feature matches between image pairs
   - Final stitched panorama

## 🔧 Key Functions

- `imregionalmax()`: Finds regional maxima (similar to MATLAB's function)
- `amns()`: Adaptive Non-Maximal Suppression for corner selection
- `get_feature_descriptors()`: Creates normalized patch descriptors
- `get_feature_matches()`: Matches features between image pairs
- `est_homography()`: Computes homography matrix using SVD
- `ransac()`: Robust homography estimation with outlier rejection
- `blend_images()`: Creates final panoramic image

## 📊 Results

The script produces:
1. ** Feature Detection Visualization**: Shows detected corners on input images
2. ** Feature Matching Visualization**: Displays matched points between image pairs
3. ** Final Panorama**: Seamlessly stitched panoramic image
