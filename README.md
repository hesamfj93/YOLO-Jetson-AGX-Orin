# YOLO-Jetson-AGX-Orin
# Training YOLO Models on NVIDIA Jetson AGX Orin with Custom Datasets

## 1. Introduction

This repository provides a comprehensive guide for training YOLO models, specifically **YOLOv8** and **YOLOv11**, on the **NVIDIA Jetson AGX Orin** platform using custom datasets. 

The datasets consist of images cropped from high-resolution sources into three square sizes:
- **1280×1280**
- **1536×1536**
- **2048×2048**

This guide covers:
- **Dataset preparation**
- **Model selection and batch size recommendations**
- **Setting up YOLO for GPU acceleration**
- **Training procedures**
- **Optimizing performance with TensorRT**
- **Evaluating results**

---

## 2. NVIDIA Jetson AGX Orin Overview

The **NVIDIA Jetson AGX Orin** is a powerful **AI computing platform** designed for edge devices, offering **exceptional performance** for AI and machine learning applications.

### **Key Specifications:**
- **GPU:** NVIDIA Ampere architecture with **2,048 CUDA cores** and **64 Tensor Cores**, delivering up to **275 TOPS (INT8)**
- **CPU:** 12-core **Arm Cortex-A78AE v8.2** 64-bit CPU with **3MB L2 and 6MB L3 cache**
- **Memory:** 32GB or 64GB **LPDDR5**, providing **204.8 GB/s bandwidth**
- **Storage:** **64GB eMMC 5.1**, microSD card slot, and **M.2 Key M** connector for NVMe
- **Video Encode/Decode:** Supports multiple **4K and 1080p video streams**

---

## 3. Dataset Preparation

### 3.1 Dataset Structure

Organize your dataset as follows for each image size (1280, 1536, 2048):

```
/dataset
 ├── /1280
 │   ├── train/
 │   │   ├── images/
 │   │   └── labels/
 │   ├── valid/
 │   │   ├── images/
 │   │   └── labels/
 │   └── test/
 │       ├── images/
 │       └── labels/
 │   └── data.yaml
 ├── /1536
 ├── /2048
```

### 3.2 Annotation Format

Annotations must be in **YOLO format**, where each line corresponds to **one object**:

```
<class_id> <x_center> <y_center> <width> <height>
```
All values should be **normalized between 0 and 1** relative to the image dimensions.

### 3.3 `data.yaml` Configuration

Each `data.yaml` file should specify paths and class names:

```yaml
train: ../train/images
val: ../valid/images
test: ../test/images

nc: 14  # Number of classes
names: ['-', 'Aplysina aerophoba', 'Asteroidea', 'Astropecten spp', 'Condylactis aurantiaca', 'Echinaster sepositus', 'Gobius sp', 'Holothuria tubulosa', 'Keratosa -cfr Sarcotragus-', 'Phaeophyceae -cfr Cystoseira-', 'Rifiuto', 'Sarcotragus spinosulus', 'Serranus scriba', 'Sphaerechinus granularis']
```

---

## 4. Model Selection and Batch Size Recommendations

Selecting an appropriate **YOLO model** and **batch size** is crucial for efficient training.

| Image Size | Recommended Model  | Batch Size | Jetson AGX Orin Compatible |
|------------|-------------------|------------|----------------------------|
| 1280×1280  | YOLOv8n (Nano)    | 64         | ✅ Yes |
|            | YOLOv8s (Small)   | 32         | ✅ Yes |
|            | YOLOv11n (Nano)   | 64         | ✅ Yes |
|            | YOLOv11s (Small)  | 32         | ✅ Yes |
| 1536×1536  | YOLOv8s (Small)   | 32         | ✅ Yes |
|            | YOLOv8m (Medium)  | 16         | ✅ Yes |
|            | YOLOv11s (Small)  | 32         | ✅ Yes |
|            | YOLOv11m (Medium) | 16         | ✅ Yes |
| 2048×2048  | YOLOv8m (Medium)  | 16         | ✅ Yes |
|            | YOLOv8l (Large)   | 8          | ✅ Yes |
|            | YOLOv11m (Medium) | 16         | ✅ Yes |
|            | YOLOv11l (Large)  | 8          | ✅ Yes |

---

## 5. Repository Structure

```
/dataset
 ├── /1280
 ├── /1536
 ├── /2048
 ├── runs/                  # Training logs & results
 ├── models/                # Trained models
 ├── ultralytics/           # YOLO codebase
 ├── README.md              # Documentation
```

---

## 6. Conclusion

By following this guide, you can **successfully train and deploy YOLOv8 & YOLOv11** on **NVIDIA Jetson AGX Orin**, leveraging **GPU acceleration** and **TensorRT** optimizations.

---

### 🔗 **Additional Resources**
- [YOLO Official Documentation](https://docs.ultralytics.com/)
- [NVIDIA Jetson AGX Orin](https://developer.nvidia.com/embedded/jetson-agx-orin)

