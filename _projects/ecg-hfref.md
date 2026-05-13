---
layout: page
title: Echo-HFrEF Classifier
description: 3D CNN vs. Vision Transformer for heart failure detection from echocardiogram video, under a 6 GB VRAM constraint
img: assets/img/ecg_results.png
importance: 1
category: machine learning
---

Can a Vision Transformer outperform a 3D CNN at detecting heart failure from 
echocardiogram video, trained on a 6 GB laptop GPU?

I compared R(2+1)D-18 (~31.5M parameters) against MViT v2 Small (~34.5M parameters) 
on the EchoNet-Dynamic dataset (10,030 videos), holding pretraining data (Kinetics-400) 
constant to isolate architecture as the variable. Models were evaluated at a clinical 
operating target — sensitivity at 90% specificity — with thresholds locked on the 
validation set before any test-set evaluation.

Before fine-tuning, the models tied. Paired bootstrap confirmed the difference was not 
statistically significant, which pointed to a shared ceiling: Kinetics-400 pretraining on 
natural video wasn't transferring well to noisy ultrasound data for either architecture. 
After fine-tuning, MViT v2 pulled ahead — ROC-AUC 0.936 vs. 0.902, sensitivity 0.825 
vs. 0.725 at ~90% specificity. The gap was statistically significant (95% CI: [0.013, 0.057]).

The cost: MViT's self-attention required halving the batch size to stay within 6 GB, 
doubling steps per epoch and pushing training time to ~10 minutes per epoch versus 
~2 min 45 sec for the CNN — roughly 3.6x slower, despite exposing fewer trainable 
parameters. Better accuracy, but the CNN stays the more practical choice anywhere 
frequent retraining matters.

**Stack:** Python, PyTorch, OpenCV, AMP, R(2+1)D-18, MViT v2 Small

[GitHub](https://github.com/farrellsid/ecg-hfref-classifier)