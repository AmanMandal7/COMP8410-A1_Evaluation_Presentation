# COMP8410 Assignment 1 - AI System Evaluation 

Author: Aman Kumar Mandal (48698040)
Session 2, 2026

## Overview
This repository contains the evaluation code and dataset for Assignment 1. Here, I have evaluated pairs of AI models in the context of a digital identity-verification organisation which covers two systems:
- System A: Onboarding & Verification
- System B: Fraud & Trust Monitoring

Each pair folder contains one or two evaluation notebooks. All notebooks were run on Google Colab and all of them can be reproduced by running the cells top to bottom.

## How to reproduce
1. Open the notebook in each folder in your preferred environment.
2. Run all cells in order. 
3. Required libraries are installed in the provided cells of each notebook.  
4. Datasets are either included in the folder or can be downloaded automatically. 

## Folders

### pair1_cv_recognition
Topic: Computer Vision / Recognition
- Model A: Face recognition (ArcFace via DeepFace) evaluated on 100 LFW pairs.
- Model B: Face anti-spoofing (MiniFASNet via DeepFace) evaluated on a 
  self-made set of 4 real and 4 spoof (print-attack) images in data/real 
  and data/spoof.
- The LFW dataset is downloaded automatically via scikit-learn.
- Outputs: accuracy, AUC, APCER/BPCER, and a similarity histogram.

### pair2_diffusion
Topic: Image Editing / Diffusion
- Model A: AI-generated image detector (Organika/sdxl-detector) via 
  Hugging Face.
- Model B: Deepfake detector (dima806/deepfake_vs_real_image_detection) 
  via Hugging Face.
- Test images (5 real, 5 fake) are in data/real and data/fake. The fake 
  images are AI-generated faces from thispersondoesnotexist.com.
- Outputs: accuracy, false accepts, false rejects for both models.

### pair3_deep_variational
Topic: Deep Variational (VAE/GAN)
- Model A: Autoencoder (AE) anomaly detector.
- Model B: Variational Autoencoder (VAE) anomaly detector.
- Both trained only on normal transactions and tested on a held-out mix of normal and fraud transactions.
- The credit-card fraud dataset is downloaded automatically from a public URL in the first cell (original source: Dal Pozzolo et al., 2015).
- Outputs: AUC for both models.

### pair4_multimodal
Topic: Multimodal / LMM
- Model A: CLIP document-type classifier (openai/clip-vit-base-patch32) via Hugging Face, using zero-shot classification.
- Model B: CLIP claim-consistency checker, using the same model to compare an image against a claimed label.
- Test set is 10 images in the data folder: publicly available specimen 
  document images, my own selfies, and free-stock random images, each with a known ground-truth label.
- Outputs: Model A classification accuracy, and Model B true-vs-false claim scores.

## Notes
- All evaluation code and analysis is my own work.
- Pre-trained models are used via their public libraries
- The small self-made image sets were created by me for testing.