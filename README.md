# 📷 Camera Calibration and Sub-Pixel Corner Detection using OpenCV

> A complete computer vision pipeline for camera calibration using checkerboard images, Harris corner detection, sub-pixel corner refinement, intrinsic camera parameter estimation, distortion correction, and reprojection error analysis with OpenCV.

![Python](https://img.shields.io/badge/Python-3.10-blue)
![OpenCV](https://img.shields.io/badge/OpenCV-Computer_Vision-green)
![NumPy](https://img.shields.io/badge/NumPy-Scientific_Computing-orange)
![Calibration](https://img.shields.io/badge/Camera-Calibration-red)
![Master](https://img.shields.io/badge/Master-MIV-lightgrey)

---

# 📖 Overview

This project presents a complete **camera calibration pipeline** developed using **Python** and **OpenCV**.

The objective is to estimate the intrinsic parameters of a camera from multiple images of a calibration checkerboard. Accurate calibration is a fundamental prerequisite for many computer vision applications such as:

- 3D Reconstruction
- Stereo Vision
- Augmented Reality
- Robotics
- Object Measurement
- Pose Estimation
- SLAM (Simultaneous Localization and Mapping)

The project includes every major stage of the calibration workflow:

- Checkerboard corner detection
- Harris corner extraction
- Sub-pixel corner refinement
- Camera intrinsic calibration
- Lens distortion estimation
- Reprojection error computation
- Calibration parameter storage

This project was developed as part of the **Master's Program in Image Processing & Artificial Intelligence (MIV)** at **USTHB**.

---

# ✨ Features

- 📷 Camera intrinsic calibration
- ♟️ Checkerboard corner detection
- 🎯 Harris Corner Detection
- 🔬 Sub-pixel corner refinement
- 📐 Camera Matrix estimation
- 📏 Distortion coefficient estimation
- 🔄 Rotation and Translation vector estimation
- 📊 Reprojection error computation
- 💾 Calibration parameter saving
- 🧠 OpenCV implementation
- 📈 Calibration accuracy evaluation

---

# 📑 Project Report

## Project Objective

Every digital camera introduces optical distortions that affect image geometry. Without calibration, measurements extracted from images are inaccurate, making many computer vision tasks unreliable.

The objective of this project is to estimate the internal characteristics of a camera by observing multiple images of a checkerboard calibration pattern.

The estimated parameters include:

- Camera intrinsic matrix
- Focal lengths
- Optical center
- Lens distortion coefficients
- Rotation vectors
- Translation vectors

These parameters allow the camera to be accurately modeled for future vision applications.

---

# 🧠 Why Camera Calibration?

Camera calibration is one of the most important preprocessing steps in computer vision.

Most imaging systems suffer from:

- Radial distortion
- Tangential distortion
- Perspective errors
- Optical imperfections

Calibration allows us to remove these distortions and recover the true geometry of the observed scene.

Applications include:

- Stereo Vision
- Drone Navigation
- Autonomous Vehicles
- Industrial Inspection
- Robotics
- Medical Imaging
- Photogrammetry
- Augmented Reality

Without calibration, depth estimation and 3D reconstruction become significantly less accurate.

---

# 🔬 Why Checkerboard Calibration?

A checkerboard is one of the most commonly used calibration patterns because:

- Corners are easy to detect
- Grid geometry is perfectly known
- High localization accuracy
- Robust against illumination changes
- Supported directly by OpenCV

Knowing the exact geometric arrangement of checkerboard corners allows OpenCV to establish correspondences between:

- Real-world 3D coordinates
- Image pixel coordinates

These correspondences are used to estimate the camera parameters.

---

# 🎯 Why Sub-Pixel Corner Detection?

Standard corner detection provides pixel-level accuracy.

However, camera calibration requires significantly higher precision.

This project improves corner localization using **Sub-Pixel Refinement** with OpenCV's `cornerSubPix()` algorithm.

Advantages include:

- Higher localization precision
- Reduced calibration error
- Better reprojection accuracy
- More reliable intrinsic parameters
- Improved stereo vision performance

Sub-pixel refinement estimates the corner position with fractional pixel precision, making calibration considerably more accurate.

---

# ⚙️ Camera Calibration Theory

The calibration process estimates the camera projection model:

Image Point = Camera Matrix × World Point

The estimated camera matrix contains:

- fx (horizontal focal length)
- fy (vertical focal length)
- cx (principal point x)
- cy (principal point y)

The project also estimates:

- Radial distortion coefficients
- Tangential distortion coefficients

These parameters completely describe the imaging characteristics of the camera.

---

# 🏗️ Pipeline

## 1️⃣ Checkerboard Image Acquisition

Multiple images of a checkerboard are captured from different viewpoints.

The diversity of viewpoints improves calibration robustness.

---

## 2️⃣ Corner Detection

Each calibration image is processed using OpenCV.

The checkerboard corners are automatically detected using:

```python
cv2.findChessboardCorners()
```

Detected corners establish the 2D image correspondences.

---

## 3️⃣ Sub-Pixel Refinement

The detected corners are refined using:

```python
cv2.cornerSubPix()
```

This step greatly improves localization accuracy.

---

## 4️⃣ Object Point Generation

The real-world coordinates of checkerboard corners are generated.

Since the checkerboard geometry is known, each corner receives a fixed 3D coordinate.

---

## 5️⃣ Camera Calibration

The intrinsic parameters are estimated using:

```python
cv2.calibrateCamera()
```

The algorithm computes:

- Camera Matrix
- Distortion Coefficients
- Rotation Vectors
- Translation Vectors

---

## 6️⃣ Calibration Evaluation

Calibration quality is measured through the **Reprojection Error**.

Each 3D point is projected back into the image.

The distance between:

- Observed corner
- Reprojected corner

is measured.

A smaller reprojection error indicates a better calibration.

---

# 📊 Estimated Parameters

The project computes:

- Camera Matrix
- Distortion Coefficients
- Rotation Vectors
- Translation Vectors
- Mean Reprojection Error

These values are saved for later use in other computer vision projects.

---

# 📂 Project Structure

```text
Camera-Calibration-and-Subpixel-Corner-Detection-Using-OpenCV/
│
├── calibrate.py
├── calibrate_camera.py
├── board.py
├── subpixels.py
├── prog1.py
│
├── images/
│   ├── calibration_01.png
│   ├── calibration_02.png
│   └── ...
│
├── images_MOBILE/
│   ├── image01.jpg
│   ├── image02.jpg
│   └── ...
│
├── camera_params/
│   ├── ret.npy
│   ├── mtx.npy
│   ├── dist.npy
│   ├── rvecs.npy
│   └── tvecs.npy
│
├── results/
│   ├── checkerboard_detection.png
│   ├── subpixel_refinement.png
│   ├── calibration_results.txt
│   └── reprojection_error.txt
│
└── README.md
```

---

# ▶️ Running the Project

Install dependencies

```bash
pip install opencv-python numpy matplotlib
```

Run the calibration

```bash
python calibrate.py
```

or

```bash
python calibrate_camera.py
```

To visualize sub-pixel corner refinement

```bash
python subpixels.py
```

---

# 📈 Output

The project estimates:

- Camera Matrix
- Distortion Coefficients
- Rotation Vectors
- Translation Vectors
- Mean Calibration Error

Calibration parameters are automatically stored as NumPy arrays for reuse.

---

# ✅ Strengths

- Complete OpenCV calibration pipeline
- Accurate checkerboard detection
- Sub-pixel corner refinement
- Intrinsic parameter estimation
- Distortion correction
- Reprojection error evaluation
- Reusable calibration parameters
- Modular Python implementation

---

# ⚠️ Limitations

- Requires multiple checkerboard images
- Sensitive to poor image quality
- Calibration accuracy depends on viewpoint diversity
- Motion blur may reduce corner detection accuracy

---

# 🚀 Future Improvements

- Automatic image quality assessment
- Camera undistortion visualization
- Stereo camera calibration
- Fisheye camera calibration
- Real-time calibration interface
- Charuco board support
- AprilTag calibration
- Bundle adjustment optimization

---

# 🛠️ Technologies Used

- Python
- OpenCV
- NumPy
- Camera Calibration
- Harris Corner Detection
- Sub-Pixel Refinement
- Linear Algebra
- Computer Vision

---

# 📚 References

- OpenCV Camera Calibration Documentation
- OpenCV Corner Detection Documentation
- Zhang, Z. (2000). A Flexible New Technique for Camera Calibration.
- OpenCV Python Tutorials
- Hartley & Zisserman — Multiple View Geometry in Computer Vision
- Richard Szeliski — Computer Vision: Algorithms and Applications
