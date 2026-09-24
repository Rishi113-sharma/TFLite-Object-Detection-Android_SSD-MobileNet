# Android Object Detection using TensorFlow Lite

An Android-based real-time object detection application using **TensorFlow Lite** and the **SSD MobileNet V2 FPNLite 320×320** model. The application processes camera frames directly on the device and displays detected objects with bounding boxes, labels, and confidence scores.

## Overview

This project demonstrates the deployment of a deep learning object detection model on an Android device for real-time inference.

The application uses a lightweight SSD MobileNet V2 FPNLite model converted to **TensorFlow Lite**, allowing object detection to be performed locally without requiring continuous internet connectivity.


## Features

* Real-time object detection using the device camera
* TensorFlow Lite model integration
* SSD MobileNet V2 FPNLite 320×320 model
* Bounding boxes around detected objects
* Object labels and confidence scores
* On-device/offline inference
* CameraX-based image analysis
* Image preprocessing and resizing
* Confidence-based detection filtering
* Custom detection overlay
* Camera permission handling
* Lightweight architecture suitable for Android devices

## Technology Stack

### Android

* Android Studio
* Java
* XML
* Android CameraX

### Machine Learning

* TensorFlow
* TensorFlow Lite
* SSD MobileNet V2 FPNLite 320×320
* Computer Vision
* Deep Learning

### Dataset & Annotation

* Pascal VOC XML
* LabelImg
* TensorFlow Object Detection API

### Development Tools

* Python
* Anaconda
* TensorFlow Model Zoo

## System Architecture

The application consists of three main layers:

```text
                 ┌──────────────────────┐
                 │      Android UI      │
                 │     XML Layouts      │
                 └──────────┬───────────┘
                            │
                            ▼
                 ┌──────────────────────┐
                 │  Application Logic   │
                 │     Java / CameraX   │
                 └──────────┬───────────┘
                            │
                            ▼
                 ┌──────────────────────┐
                 │   Image Processing   │
                 │ Resize & Normalize   │
                 └──────────┬───────────┘
                            │
                            ▼
                 ┌──────────────────────┐
                 │   TensorFlow Lite    │
                 │ SSD MobileNet V2     │
                 └──────────┬───────────┘
                            │
                            ▼
                 ┌──────────────────────┐
                 │ Detection Results    │
                 │ Boxes + Labels +     │
                 │ Confidence Scores    │
                 └──────────────────────┘
```

The project architecture follows a modular approach consisting of the Android UI, application logic, image preprocessing, TensorFlow Lite inference, result processing, and detection overlay.

## Object Detection Pipeline

The complete pipeline works as follows:

```text
Camera Input
     ↓
Capture Frame
     ↓
Image Preprocessing
     ↓
Resize to 320 × 320
     ↓
Normalize Pixel Values
     ↓
TensorFlow Lite Model
     ↓
SSD MobileNet V2 Detection
     ↓
Bounding Boxes + Class IDs + Scores
     ↓
Confidence Filtering
     ↓
DetectionResult
     ↓
OverlayView
     ↓
Display Results
```

The application resizes the camera frame according to the model input dimensions and converts RGB pixel values into normalized float values before inference.

## Model

The project uses:

**SSD MobileNet V2 FPNLite 320×320 COCO17 TPU-8**

The model is designed for efficient object detection and is suitable for mobile and edge-device deployment.

The trained TensorFlow model is converted into TensorFlow Lite format and integrated into the Android application.

## Dataset Preparation

The object detection dataset is prepared using **LabelImg** with annotations stored in **Pascal VOC XML format**.

The workflow is:

```text
Images
   ↓
LabelImg
   ↓
Pascal VOC XML Annotations
   ↓
Training / Testing Split
   ↓
TensorFlow Record Files
   ↓
Model Training
   ↓
TensorFlow Lite Conversion
   ↓
Android Deployment
```

The project uses XML annotations containing object classes and bounding-box coordinates. The training and testing data are converted into `train.record` and `test.record` files for the TensorFlow object detection pipeline.

## Android Implementation

The Android application contains several important components:

### MainActivity

Handles the main user interface and navigation to the camera detection screen.

### CameraActivity

Responsible for:

* Camera initialization
* Camera permission
* CameraX preview
* Image analysis
* TensorFlow Lite inference
* Detection result processing

### DetectionResult

Stores:

* Bounding box
* Object label
* Class ID
* Confidence score

### OverlayView

Draws the detected bounding boxes and labels over the camera preview.

## Camera Processing

CameraX is configured with an image analysis pipeline using:

* Back camera
* `STRATEGY_KEEP_ONLY_LATEST`
* RGBA_8888 image format
* Background analysis executor

This allows the application to continuously process camera frames while avoiding unnecessary frame backlog.

## Detection Output

For every detected object, the application generates:

```text
Object Label
Confidence Score
Bounding Box
Class ID
```

For example:

```text
Person (94.2%)
Bottle (87.5%)
```

Objects below the configured confidence threshold are ignored before being displayed.

## Project Structure

A typical project structure is:

```text
Android-Object-Detection-TFLite/
│
├── app/
│   └── src/
│       └── main/
│           ├── java/
│           │   └── ...
│           │
│           ├── res/
│           │   ├── layout/
│           │   ├── drawable/
│           │   └── values/
│           │
│           └── assets/
│               ├── model.tflite
│               └── label.txt
│
├── README.md
└── LICENSE
```

## Requirements

### Software

* Android Studio
* Android SDK
* Java
* Python 3.9.x for the model-training environment
* TensorFlow 2.10
* CUDA 11.2
* cuDNN 8.1
* LabelImg

The project report specifies a Python 3.9.23 environment, TensorFlow 2.10, CUDA Toolkit 11.2, cuDNN 8.1, and LabelImg for the model-development workflow.

### Hardware

An Android device with a camera is required for real-time detection.

For model training, a CUDA-compatible GPU can be used to accelerate training.

## Installation

### 1. Clone the repository

```bash
git clone https://github.com/YOUR_USERNAME/Android-Object-Detection-TFLite.git
```

```bash
cd Android-Object-Detection-TFLite
```

### 2. Open the project

Open the project using **Android Studio**.

Allow Android Studio to download and configure the required Gradle dependencies.

### 3. Connect an Android device

Enable:

```text
Developer Options
USB Debugging
```

Then connect the Android device to your computer.

### 4. Build and run

Run the application from Android Studio.

Grant camera permission when requested.

## How to Use

1. Launch the application.
2. Grant camera permission.
3. Start the detection camera.
4. Point the camera toward an object.
5. The application processes the camera frame.
6. Detected objects appear with bounding boxes.
7. Labels and confidence scores are displayed in real time.

The application performs inference directly on the Android device, so continuous internet connectivity is not required.

## Testing

The project was tested using:

* Unit Testing
* Integration Testing
* System Testing
* User Acceptance Testing

Testing covered camera initialization, image preprocessing, TensorFlow Lite inference, detection-result handling, bounding-box rendering, multi-object detection, error handling, and device compatibility.

## Limitations

* Detection is dependent on the objects supported by the trained model.
* Detection accuracy can decrease under poor lighting or complex backgrounds.
* Small or heavily occluded objects can be difficult to detect.
* Continuous camera processing can consume battery.
* Low-end devices may experience reduced frame rates.
* The current system does not provide in-app custom model training.

The report identifies the fixed COCO object classes, lighting/background conditions, device performance, battery usage, and fixed 320×320 input resolution as key limitations.

## Future Improvements

Possible future improvements include:

* Custom object detection models
* Additional object classes
* GPU / NNAPI acceleration
* Improved frame-processing optimization
* Better detection accuracy
* Real-time video streaming optimization
* Cloud-based analytics
* Multiple model support

The project report specifically proposes custom object training, hardware acceleration, frame-processing optimization, cloud integration, and support for additional object classes.

