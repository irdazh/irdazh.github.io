---
layout: post
title: Corn Leaf Disease Detector 2
categories:
- DS Projects
tags:
- classification
- computer vision
- cnn
- transfer learning
description: Corn leaf disease classification using CNN and transfer learning extended version. Awokokoow.
media_subpath: "/assets/img/leaf-disease"
---

In this project, I built an end-to-end **image classification** system to detect corn leaf diseases using deep learning — and **deployed** it into a working web application.

Yup, if you guys remember, this is the second article of the previous [Leaf Disease Detector](https://irdazh.github.io/posts/leaf-disease) article which might contain a more detailed explanation. Let's see. 

I think it's best to be work in progress. Most topics are pretty new to me, and definitely much more complicated than I anticipated. Nah, not sure tho.


## Problem
Here are some things worth explaining. I'm not sure about the coverage, but whatsoever, let's start this thing.  

1. Imbalance Data
2. Image Normalization
3. Rule of Thumb
4. Image Augmentation

**Current Progress** 

5. Model Evaluation
6. Probabilty Adjustment
7. ROC Score & Curve
8. Error Analysis
9. Lime Explanation
10. Shap Explanation

## Data
We used [Corn or Maize Leaf Disease Dataset](https://www.kaggle.com/datasets/smaranjitghose/corn-or-maize-leaf-disease-dataset) from kaggle dataset for this project.

![Sample Data](/sample_data.png)_Sample image of training set_

The dataset contains images of corn leaves with 4 classes: healthy, common rust, blight, and gray leaf spot. The data is pretty much balanced except for gray leaf spot disease, which only exist half the frequency (?)

![Imbalanced](/imbalanced.png)_Class proportion_

## Modeling & Training
### Image Normalization

From an AI Overview by Google, it ensures consistent input data (in case too dark/too bright data), leading to faster training convergence, **stable gradients**, reduced sensitivity to input variance, and improved **model generalization**. 

![Warning](/warning_difference.png)_Warning screenshot_

I suggest those are the main reason some warning of difference in training calculation thingy --. Ugh. Because of model unstability (?) since the value differs so much for dark compared with bright case (?)

> Eh, a quick revision here: based on my hazy memory, it cause I don't use batchnormalization (?) Oh what's wrong with my memory recently.

#### Comparison

![Training](/training_complex.png)_Training without normalization_

![Training](/training_normalization.png)_Training with normalization_

Why does the one without normalization look better? What. boom. Worry not, it's too complicated for now, so just drop it.

### Rule of Thumb

There are several rule of thumb, I asked LLM model about it, and yeah, you can find it inside the notebook. Should I copy-paste them here? Nah, for what? 

What did it say? A funnel-like structure? Right. And a sprinkle of salt to taste!

### Callbacks
I think it's safe to use early stopping, reduce LR on plateau, and add model checkpoint. Even for a simpler model (?) With 20 epochs kinda enough? 

Oh, and you can continue training the model again by fitting the model again? And it will continue from the previous epochs, I guess....


### Image Augmentation

It supposed to help, but statistically, I got no proof. 

For future references, I added the augmented version in the notebook. 

## `Best` Model

### Model Evaluation

Model performance with normalization:
* Base model: 84/85/82 percent and 0.36/0.32/0.41 loss.
* Complex: 97/95/92 percent and 0.10/0.15/0.17 loss. 

**Conclusion**
* So, in complex model, can I say the model kinda overfit in training and validation (but 2 percent diff is kinda expected no? But loss, hmm, I can't decide whether to use absolute or relative diff)
* Validation set overfitting? Cuz I try to minimize val loss in model checkpoint and use save best only == True?
* Choice you have: overfit to training data vs overfit to validation data hhhh. Well, it's not that bad tho. So, chill dude. 

### Error Analysis



### Probability Adjustment
It's good enough in validation set, since we make sure `to fit` the validation set nicely. Let's compare them with or without confidence adjustment in test set. 







