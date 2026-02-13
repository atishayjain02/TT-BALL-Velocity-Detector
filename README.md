# 🏓 Table Tennis Ball Velocity Estimation using YOLOv8 & CLIP

An end-to-end computer vision project that detects, tracks, and estimates the real-world velocity of a table tennis ball from match videos using YOLOv8, object tracking, and physics-based computation, with a small CLIP multimodal experiment for semantic understanding.

---

## 🚀 Project Overview

The goal of this project is to estimate the speed of a table tennis ball from video footage.  
Due to the ball’s small size, high speed, and motion blur, traditional OpenCV-based approaches are unreliable.  
This project uses deep learning–based object detection and tracking, combined with frame timing and calibration, to compute ball velocity.

---

## 🧠 Key Features

- Small-object detection using YOLOv8  
- Custom dataset with human-in-the-loop annotation  
- Training analysis using loss curves, precision, recall, and mAP  
- Ball tracking using ByteTrack  
- Physics-based pixel-to-meter speed estimation  
- Speed vs time visualization  
- CLIP zero-shot experiment for multimodal understanding  
- GPU-accelerated training using PyTorch  

---

## 🛠️ Tech Stack

- Language: Python  
- Frameworks: PyTorch, Ultralytics YOLOv8  
- Computer Vision: OpenCV  
- Tracking: ByteTrack  
- Multimodal Model: CLIP (ViT-B/32)  
- Annotation Tool: Roboflow  
- Compute: NVIDIA GPU (Kaggle / Google Colab)  

---

## 📂 Project Pipeline

Video Input  
→ Frame Extraction  
→ Manual Annotation (Initial Subset)  
→ Human-in-the-Loop Auto-Labeling  
→ YOLOv8 Training & Evaluation  
→ Ball Detection + Tracking  
→ Pixel-to-Meter Calibration  
→ Speed Calculation (FPS-based)  
→ Visualization & Analysis  

---

## 📊 Dataset Preparation

- Frames extracted from table tennis match videos  
- Initial ~200 frames manually annotated  
- Remaining frames auto-labeled using a rough YOLOv8 model  
- Manual correction applied to auto-labeled frames  
- Single class used: `ball`  

Human-in-the-loop annotation reduced labeling effort by approximately 60–70% while maintaining data quality.

---

## 🧪 Model Training

- Base model: `yolov8n.pt` (pretrained on COCO)  
- Transfer learning on custom dataset  
- Image size: 640 × 640  
- Batch size: 16  
- Epochs: 30  
- Metrics monitored:
  - Train Box Loss
  - Validation Box Loss
  - Train Class Loss
  - Precision
  - Recall
  - mAP@0.5 and mAP@0.5–0.95  

---

## 🎯 Inference & Tracking

- YOLOv8 used for frame-wise ball detection  
- ByteTrack used to maintain consistent ball identity across frames  
- Tracking improves robustness against motion blur and missed detections  

---

## ⚙️ Velocity Estimation Logic

1. Extract ball center coordinates per frame  
2. Compute pixel displacement between consecutive frames  
3. Convert pixel distance to meters using table calibration  
4. Compute time difference using video FPS  
5. Calculate ball speed in m/s and km/h  
6. Apply temporal smoothing to reduce noise  

Note: This is a single-camera 2D approximation. True physical accuracy would require multi-camera calibration.

---

## 📈 Results & Visualization

- Speed vs frame graph shows realistic rally dynamics  
- Peaks correspond to fast smashes  
- Dips occur during bounces, direction changes, or brief occlusions  

---

## 🧩 CLIP Multimodal Experiment

A small CLIP (ViT-B/32) zero-shot experiment was conducted to demonstrate semantic understanding:

- Image frames compared against text prompts such as:
  - “a table tennis ball”
  - “a table tennis player”
  - “an empty table tennis table”
- Demonstrates how YOLO answers *where* an object is, while CLIP answers *what* is happening in the scene  

---

## 🧠 Key Learnings

- Importance of data quality for small-object detection  
- Trade-offs between precision and recall via confidence thresholds  
- Role of tracking in downstream tasks like speed estimation  
- Practical limitations of single-camera vision systems  
- Value of multimodal models for higher-level understanding  

---

## 🚧 Limitations & Future Work

- Single-camera 2D approximation  
- No depth estimation  
- Future improvements:
  - Multi-camera 3D calibration
  - Kalman filter–based smoothing
  - Rally-level analytics
  - Multimodal fusion with temporal models  

---

## 🧑‍💻 Author

Atishay Jain  
Machine Learning & Computer Vision Enthusiast  

---

## ⭐ Final Note

This project focuses on understanding the complete computer vision pipeline—from dataset creation and model training to inference, tracking, and physics-based reasoning—rather than only running pretrained models.
