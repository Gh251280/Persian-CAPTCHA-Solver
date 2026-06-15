# Persian CAPTCHA Solver

A multi-stage deep learning pipeline for solving Persian CAPTCHA images using Computer Vision and Deep Learning techniques.

## Overview

This project is designed to recognize Persian CAPTCHA images containing different font styles.

Instead of using a single recognition model, the pipeline first identifies the CAPTCHA font and then routes the image to a dedicated recognition model trained specifically for that font.

This approach improves recognition quality and reduces model confusion between different font styles.

---

## Pipeline Architecture

Input CAPTCHA Image

↓

Image Preprocessing

↓

Font Classification (EfficientNet-B0)

↓

Font Routing Logic

↓

Mask R-CNN (Detectron2)

↓

Character Detection

↓

String Reconstruction

↓

Final CAPTCHA Text

---

## Project Stages

### 1. Image Preprocessing

The raw CAPTCHA image is cleaned before recognition.

Tasks include:

- Noise removal
- Image enhancement
- Preparation for classification

---

### 2. Font Classification

An EfficientNet-B0 model is used to classify the CAPTCHA font.

The classifier predicts one of three font categories:

- Font Type 1
- Font Type 2
- Font Type 3

Since EfficientNet requires 224×224 images, the original CAPTCHA images are padded before inference.

---

### 3. Font-Based Routing

Based on the predicted font class, the system automatically selects the corresponding recognition model.

This design allows each recognition model to specialize in a single font style.

---

### 4. Character Detection and Segmentation

Character detection is performed using:

- Detectron2
- Mask R-CNN

A separate Mask R-CNN model is trained for each font family.

The model detects and segments CAPTCHA characters from the image.

---

### 5. String Reconstruction

Detected characters are sorted and converted into the final CAPTCHA string.

Example:

Image:

[Persian CAPTCHA]

Output:

12345

---

## Technologies Used

- Python
- PyTorch
- Detectron2
- Mask R-CNN
- EfficientNet-B0
- OpenCV
- Google Colab

---

## Repository Structure

```text
Persian-CAPTCHA-Solver/

├── notebooks/
│   ├── efficientnet_font_classifier.ipynb
│   └── mask_rcnn_training_and_inference.ipynb
│
├── src/
│   ├── preprocessing.py
│   └── font_router.py
│
├── examples/
│   ├── input_sample.png
│   └── output_sample.png
│
└── README.md# Persian-CAPTCHA-Solver
Persian CAPTCHA recognition using Detectron2, Mask R-CNN and EfficientNet-B0
