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
- Model B: Face anti-spoofing (MiniFASNet via DeepFace) evaluated on a self-made set of 4 real and 4 spoof (print-attack) images in data/real and data/spoof.
- The LFW dataset is downloaded automatically via scikit-learn.
- Outputs: accuracy, AUC, APCER/BPCER, and a similarity histogram.

### pair2_diffusion
Topic: Image Editing / Diffusion
- Model A: AI-generated image detector (Organika/sdxl-detector) via Hugging Face.
- Model B: Deepfake detector (dima806/deepfake_vs_real_image_detection) via Hugging Face.
- Test images (5 real, 5 fake) are in data/real and data/fake. The fake images are AI-generated faces from thispersondoesnotexist.com.
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
- Test set is 10 images in the data folder: publicly available specimen document images, my own selfies, and free-stock random images, each with a known ground-truth label.
- Outputs: Model A classification accuracy, and Model B true-vs-false claim scores.

### pair5_video_temporal
Topic: Video / Temporal Analysis
- Model A: Frame-based deepfake detector, baseline (dima806/deepfake_vs_real_image_detection) via Hugging Face.
- Model B: Frame-based deepfake detector, newer training set (prithivMLmods/Deep-Fake-Detector-v2-Model) via Hugging Face. Same ViT backbone as Model A, trained on a different dataset.
- Test set is 3 short videos in the data folder: two real (one self-recorded, one public sample) and one deepfake (celeb_synthesis.mp4).
- Each video is reduced to ~12 sampled frames, scored per-frame by both models, then combined into a per-video decision (mean probability + majority vote). Temporal consistency (score variance, frame-to-frame change) is also measured.
- Outputs: per-video real/fake decision and accuracy for both models, plus temporal consistency stats.

### pair6_gnn_heterophily
Topic: Graph Neural Networks under Heterophily
- Model A: Standard GCN (homophily) using PyTorch Geometric's GCNConv.
- Model B: FAGCN (heterophily) using PyTorch Geometric's FAConv, which learns a signed weight per edge.
- Dataset is the Wisconsin web-page graph (WebKB), a known heterophilous graph with an edge homophily ratio of 0.196. It downloads automatically via PyTorch Geometric in the notebook.
- Both models are trained with the same setup (cross-entropy, Adam, 200 epochs) and evaluated across the 10 standard train/test splits, with results averaged.
- Outputs: accuracy and macro-F1 for both models, plus the graph's edge homophily ratio.

### pair7_fairness_governance
Topic: Fairness and Governance
- Model A: Logistic Regression classifier (scikit-learn).
- Model B: Random Forest classifier (scikit-learn).
- Both predict whether a person earns over 50K, trained and tested on the same features, then audited for fairness across the sex groups.
- Dataset is the Adult Income dataset (~48,800 records). It downloads automatically via fairlearn in the notebook (original source: Becker & Kohavi, 1996).
- Outputs: accuracy, demographic parity difference, and equalized odds difference for both models, plus accuracy broken down by group.

## Notes
- All evaluation code and analysis is my own work.
- Pre-trained models are used via their public libraries.
- The small self-made image and video sets were created by me for testing.
- Datasets that download automatically (LFW, credit-card fraud, Wisconsin, Adult) are public and fetched at runtime, so no large data files are stored in this repository.
- No real identity documents or sensitive personal data are included; all face/video test samples are either my own or from public sources.