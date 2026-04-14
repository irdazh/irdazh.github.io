---
layout: post
title: Corn Leaf Disease Detector
categories:
- DS Projects
tags:
- classification
- computer vision
- cnn
- transfer learning
description: Corn leaf disease classification using CNN and transfer learning.
media_subpath: "/assets/img/leaf-disease"
date: 2026-04-15 00:00 +0000
---

In this project, I built an end-to-end **image classification** system to detect corn leaf diseases using deep learning — and **deployed** it into a working web application.

![Demo Image](/demo1.png)_Simple demo page_

Follow these links:
- Live demo: [https://leaf-disease-deploy.streamlit.app/](https://leaf-disease-deploy.streamlit.app/)
- GitHub repo: [https://github.com/irdazh/leaf-disease/](https://github.com/irdazh/leaf-disease/)

I will probably make the second part (eak, say the line, wak!) for a geekier explanation on details. Just maybe. As for now, I will make it as concise as the *** suggested!

Ah, and of course, for transparation (tho not really needed), I did amati-tiru-modifikasi (just a bit of modification) from a random kaggle notebook I found. Cheating? Nope, I don't think so, it all is about mindset~

## The Problem

Crop diseases can significantly reduce agricultural yield. Early detection is essential, but manual inspection is time-consuming and error-prone.

Can we automate this using computer vision? (Yeah, ofc.)

## Approach

I experimented with three CNN architectures:

* Simple CNN (baseline)
* Moderate CNN
* Complex CNN (deeper architecture)

I also explored transfer learning using pretrained models: ResNet, VGG, MobileNet, and DenseNet. 


## Key Findings

![Training Complex](/training_complex.png)_Complex CNN model training_

### 1. Model Complexity Matters

The simple CNN achieved:

* 87% validation accuracy

While the deeper CNN improved to:

* 94% validation accuracy


### 2. Performance vs Generalization

Although the complex CNN performed best on validation data (94%), its test performance (89%) suggests slight overfitting.


### 3. Transfer Learning is Competitive

Fine-tuned ResNet achieved similar validation performance (93%) with fewer training epochs, showing the efficiency of pretrained models. 

But somehow, on a random test prediction, it works better (and more stable) than the better-validation-performance (my own) complex CNN model. Should I add my 60% confidence here?

### 4. Where the Model Struggles

![Confusion Matrix](/cm_complex.png)_Confusion matrix of Complex CNN model on test set_

The model often confuses:

* Gray Leaf Spot ↔ Blight

This indicates visual similarity between disease patterns.


## Deployment

To make the model usable, I built:

* A FastAPI backend for local inference
* A Streamlit frontend for user interaction
* A simplified Streamlit app for online deployment

Users can:

* Upload an image
* Select a model (for online deployment, I excluded the ResNet model --- it was way too heavy)
* Get predictions instantly


## What I Learned

* Model performance must be evaluated beyond accuracy (sure, I will probably do it later, mwehehehehe)
* Preprocessing consistency is critical for deployment (how can I forgot to normalize the image?)
* Simpler deployment (Streamlit-only) is often more practical
* UX matters — even for ML projects (what? who the what wrote this nonsense?)
* It's not (that) hard, lol, just duplicate the notebook, click run and waiting. Hhhhh. 


## Final Thoughts

This project helped me bridge the gap between:

> Training models → Deploying real applications


## Demo

Again, follow [this link](https://leaf-disease-deploy.streamlit.app/)  for a live demo!

![Another demonstration](/demo2.png)_See how the complex CNN model predict the disease wrong? Oops, my bad._
