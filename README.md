# Vehicle Detection & Tracking Project

This repository provides a complete **end-to-end pipeline** for real-time vehicle detection, refinement, and tracking using a hybrid YOLOv8 + Faster R-CNN detector integrated with DeepSORT. It’s organized as a professional project you can run, explore, or adapt for your own datasets.

---

## 📂 Directory Structure

```
vehicle_detection_project/
│
├── data/                     # Download manually from Roboflow
│   ├── voc_format/            
│   │   ├── train/             # Pascal VOC images + XML annotations for Faster R-CNN  
│   │   └── valid/             
│   └── yolo_format/           # YOLOv8–style images + .txt labels  
│       ├── train/             
│       └── valid/             
│       └── data.yaml          
│
├── inputs/
│   ├── 2252223-sd_960...mp4          # Raw traffic video input
│   └── vecteezy_slow-mo...mp4        # Another test video

├── models/
│   ├── best.pt                # Trained YOLOv8 weights  
│   ├── faster_rcnn_final.pth  # Final Faster R-CNN weights  
│   └── checkpoints/           # RCNN epoch‐by‐epoch checkpoints  

├── outputs/
│   ├── tracked_output.mp4     # Video with hybrid detection & tracking overlay  
│   └── tracking_report.txt    # Summary report (total counts & lifespans)  

├── final_project.ipynb        # Jupyter notebook with full pipeline  
├── .gitattributes             # Git LFS tracked files
├── .gitignore                 # Ignored folders/files
└── README.md                  # Project overview & instructions  
```

---

## 📥 Dataset

Due to GitHub file size limits, the dataset is **not included in this repo**.

👉 **Download from Roboflow**:  
[UA-DETRAC Dataset (10K)](https://universe.roboflow.com/rjacaac1/ua-detrac-dataset-10k)

Then place them under:

```
data/voc_format/train
data/voc_format/valid
data/yolo_format/train
data/yolo_format/valid
```

---

## ⚙️ Prerequisites

- **Python 3.8+**  
- **PyTorch 1.12+** & **torchvision 0.13+**  
- **ultralytics** (YOLOv8)  
- **opencv-python**  
- **deep_sort_realtime**  
- **tqdm**, **Pillow**, **numpy**

Install all dependencies:
```bash
pip install torch torchvision ultralytics opencv-python deep_sort_realtime tqdm Pillow numpy
```

---

## 🚀 Usage

1. **Prepare your data**  
   - VOC-style: `data/voc_format/{train,valid}`  
   - YOLO-style: `data/yolo_format/{train,valid,data.yaml}`  

2. **Train or skip**  
   - **YOLOv8:**  
     `python scripts/train_yolov8.py`  
     → Saves model to `models/best.pt`  
   - **Faster R-CNN:**  
     `python scripts/train_rcnn.py`  
     → Saves model to `models/faster_rcnn_final.pth`  

3. **Run in Notebook**  
   Open `final_project.ipynb` for:
   - Hybrid model setup  
   - Refinement logic  
   - Object tracking  
   - Metric logging  
   - Final video/report generation  

4. **Run entire pipeline as script** (if provided):
   ```bash
   python scripts/run_hybrid_tracking.py
   ```

---

## 🎥 Output Video

![Detection Demo](outputs/demo.gif)

---

## 📑 Tracking Report

Check `outputs/tracking_report.txt` for a readable summary:

```
=== Tracking Report ===

Video processed: inputs/2252223-sd_960...mp4
Total frames: 1200

BUS:
  • Total unique seen : 23
  • Avg lifespan      : 45.2 frames

CAR:
  • Total unique seen : 58
  • Avg lifespan      : 60.8 frames
...
```

---

## 🔧 Customization

- **Thresholds**: Adjust YOLO/RCNN confidence & NMS thresholds  
- **Tracker config**: Modify `max_age`, `n_init` in the tracker  
- **Video input**: Add more videos to `inputs/` and change paths in the notebook  

---

## 📄 License & Acknowledgments

This project is for academic and demonstration purposes. Please cite if you use the pretrained models, dataset, or pipeline.

Enjoy building your vehicle detection & tracking system!
