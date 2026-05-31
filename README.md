# Panorama Stitching: Homography Estimation & RANSAC 📸
* **Course:** CMSC426
* **Author:** Arik Gershman

## Viewing This Project
The Jupyter notebook contains embedded output and visualizations, which makes it too large to render directly on GitHub. For the best experience:
* 📄 **[View the PDF](CMSC426_Assignment3_sp26.pdf)** — recommended for a quick look at the code and results
* 📓 **[View the notebook on nbviewer](https://nbviewer.org/github/arikgershman/panorama-image-stitching/blob/main/CMSC426_Assignment3_sp26.ipynb)** — for interactive notebook rendering
* 💾 Download the `.ipynb` file to run it locally

## Project Overview
This project implements an algorithm for estimating homography (projective transformation) with RANSAC from scratch to stitch images together into seamless panoramas. The implementation relies on fundamental computer vision techniques and mathematical models to compute perspective transformations rather than using pre-existing built-in functions from libraries like OpenCV.

## Methodology
The pipeline is broken down into several main components:

**1. Homography Estimation (Direct Linear Transformation)**
* Computes the 3x3 homography matrix $\mathbf{H}$ mapping planar surface point correspondences between two images.
* Constructs the linear system of equations from $n \geq 4$ point correspondences.
* Solves the system using Singular Value Decomposition (SVD) to extract the transformation parameters.

**2. Robust Estimation with RANSAC**
* Iteratively selects random subsets of point correspondences to estimate candidate homographies.
* Evaluates each candidate by transforming all points and counting the number of "inliers" (points that fall within a strict distance threshold).
* Isolates the homography matrix with the highest number of inliers to robustly handle noise, outliers, and incorrect feature matches.

**3. Panorama Stitching & Blending**
* Projects multiple images onto a common viewing plane using the robustly estimated homography matrices.
* Combines the aligned images and applies blending techniques (evaluating simple blending vs. Laplacian Pyramid Image Blending) to prevent ghosting effects and create a smoother visual transition between the image borders.

## Technologies Used
* **Language:** Python
* **Environment:** Jupyter Notebook
* **Libraries:** NumPy, SciPy (for n-dimensional image processing), Matplotlib, OpenCV (strictly for basic image I/O and unit testing evaluations)
