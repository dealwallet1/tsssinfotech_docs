# ANPR (Automatic Number Plate Recognition) System Documentation

## Project Overview

This project implements an end-to-end Automatic Number Plate Recognition
(ANPR) system using:

-   YOLOv8 (Object Detection)
-   Roboflow (Dataset Management and Annotation)
-   EasyOCR (Text Recognition)
-   OpenCV (Video Processing)
-   Google Colab (Training Environment)

Goal: Detect vehicle license plates from video and extract text from
detected plates.

------------------------------------------------------------------------

# End-to-End Workflow

Dataset Collection (Roboflow) ↓ Dataset Annotation ↓ Export Dataset in
YOLOv8 Format ↓ Google Colab Setup ↓ YOLOv8 Fine-Tuning ↓ Model Training
↓ best.pt Generated ↓ Video Upload ↓ License Plate Detection ↓ OCR
Processing ↓ Output Video Generation

------------------------------------------------------------------------

# Technologies Used

  Technology     Purpose
  -------------- -------------------------
  Python         Programming
  YOLOv8         License Plate Detection
  Roboflow       Dataset Annotation
  OpenCV         Video Processing
  EasyOCR        Text Extraction
  Google Colab   GPU Training

------------------------------------------------------------------------

# Dataset Preparation

Dataset Source: Roboflow License Plate Dataset

Dataset Structure:

train/ valid/ test/ data.yaml

Annotation Format:

class_id x_center y_center width height

------------------------------------------------------------------------

# Model Training

Base Model:

yolov8n.pt

Training Configuration:

Epochs: 50

Image Size: 640

Batch Size: 16

GPU: Tesla T4

Training Command:

model.train( data="data.yaml", epochs=50, imgsz=640, batch=16, device=0
)

------------------------------------------------------------------------

# Training Results

Final Metrics:

Precision: 0.984

Recall: 0.966

mAP50: 0.983

mAP50-95: 0.708

Generated Files:

best.pt

last.pt

best.pt selected for inference.

------------------------------------------------------------------------

# OCR Pipeline

Steps:

1.  Detect License Plate
2.  Crop Plate Region
3.  Convert to Grayscale
4.  Resize Image
5.  Apply Thresholding
6.  OCR using EasyOCR
7.  Text Stabilization
8.  Display Final Output

------------------------------------------------------------------------

# OCR Stabilization Logic

Problem:

OCR output flickers between frames.

Solution:

Sliding Window Buffer

Majority Voting

Example:

Frame 1: AP39AB1234

Frame 2: AP39A81234

Frame 3: AP39AB1234

Final Stable Output:

AP39AB1234

------------------------------------------------------------------------

# Video Processing Flow

Input Video

↓

YOLO Detection

↓

Plate Crop

↓

EasyOCR

↓

Bounding Box Drawing

↓

Output Video

------------------------------------------------------------------------

# Output Generated

Final Output:

output.mp4

Output Features:

-   License Plate Detection
-   OCR Text Reading
-   Bounding Box Visualization
-   Stabilized Detection
-   Real-Time Video Processing

------------------------------------------------------------------------

# Challenges Faced

1.  Corrupted model download
2.  Dataset path mismatch
3.  FileNotFoundError issues
4.  OCR flickering
5.  Video filename mismatch

Solutions:

-   Re-downloaded model
-   Verified dataset path
-   Added preprocessing
-   Added stabilization buffer

------------------------------------------------------------------------

# Final Outcome

Successfully built an end-to-end ANPR pipeline.

Completed Components:

Dataset Preparation

YOLOv8 Fine-Tuning

Custom Model Training

License Plate Detection

OCR Integration

Output Video Generation

------------------------------------------------------------------------

# Deliverables

1.  Roboflow Dataset
2.  YOLOv8 Custom Model
3.  best.pt Model
4.  OCR Pipeline
5.  Output Video

Project Status:

Completed Successfully
