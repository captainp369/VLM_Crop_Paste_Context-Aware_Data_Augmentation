# VLM-Guided Context-Aware Data Augmentation for Semantic Segmentation

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

This repository contains the code for the dissertation project "Dealing with Imbalanced Data using Context-Aware Data Augmentation". This project investigates using Vision-Language Models (VLMs) to guide a crop-and-paste data augmentation strategy, aiming to address class imbalance in remote sensing imagery.

---
## 📜 Overview

Class imbalance is a significant challenge in semantic segmentation, particularly in domains like remote sensing where minority classes (e.g., cars) are underrepresented. While crop-and-paste is a common augmentation technique, random pasting can create unrealistic training samples that degrade model performance.

This project introduces a pipeline that leverages the contextual understanding of VLMs (e.g., Gemini, Qwen2.5-VL, GPT-5) to identify semantically appropriate locations for pasting minority-class objects. The goal is to generate more realistic and effective training data to improve model performance on rare classes without harming overall accuracy.

---
## ⚙️ How It Works

The pipeline is divided into two main stages:

1.  **Cropping Stage**: Minority-class objects are identified and cropped from the training dataset using their ground-truth masks. These cropped instances are saved to create an "object pool" for later use.

2.  **VLM-Guided Pasting Stage**: For a target image, the system:
    * Selects a random object from the pool.
    * Prompts a VLM with the target image, its semantic mask, and a natural language query (e.g., "a realistic place to put a car").
    * The VLM returns candidate coordinates for pasting.
    * A conditional rule filters these coordinates, ensuring the object is only pasted on a valid surface (e.g., a 'car' on a 'road').
    * The object is pasted, and the corresponding image and mask are saved.

---
## ✨ Key Features

* **Automated Pipeline**: End-to-end pipeline for context-aware crop-and-paste.
* **VLM Integration**: Easily configurable to use various VLMs via API for placement suggestions.
* **Semantic Validation**: Includes conditional rules to ensure pastes are contextually valid based on segmentation masks.
* **Reproducible Research**: Scripts for training, evaluation, and comparison against key baselines (Focal Loss, Class Weighting, Random Paste).

---
## 🚀 Getting Started

### Usage

1.  **Configure**: Set up your dataset paths and parameters.

2.  **Run the Cropping Stage**: Generate the object pool from your dataset.

3.  **Run the Pasting Stage**: Generate the VLM-augmented dataset.

4.  **Train the Model**: Fine-tune a DeepLabv3+ model on your new dataset.

5.  **Evaluate**: Test the model's performance.

---
## 📊 Results

Experiments were conducted three times to account for the stochastic nature of the pipeline. The findings indicate that while VLM-guided augmentation shows potential, it did not consistently outperform base model in this study. This suggests that achieving realism is a complex challenge that goes beyond just semantic placement and includes factors like lighting, scale, and object rotation.

Our VLM-augmented model performed better than random pasting and had a less detrimental effect on majority classes compared to Focal Loss.

---
## 🏛️ Citation

If you use this code or find this work helpful in your research, please consider citing the dissertation:

```bibtex
@mastersthesis{Piampatiparn2025,
  author  = {Pakawat Piampatiparn},
  title   = {Project Repository: Dealing with Imbalanced Data using Context-Aware Data Augmentation},
  school  = {the University of Liverpool},
  year    = {2025},
  howpublished = {\url{https://github.com/captainp369/VLM_Crop_Paste_Context-Aware_Data_Augmentation}},
}
