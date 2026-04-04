---
layout: post
title: "Understanding Customer Reviews: Sentiment & Topics"
categories:
- DS Projects
tags:
- classification
- sentiment analysis
- topic modeling
description: 'Sentiment analysis and topic modeling on customer reviews.'
media_subpath: "/assets/img/customer-review"
---

## The Why

When looking at e-commerce reviews, a simple question came up:

> “Are customers actually satisfied, and if not, why?”

(Believe me, it didn't happen that way, the AI wrote them up!)

This project explores that using:
- Sentiment analysis
- Topic modeling
- An interactive dashboard


## The Data Reality

![Sentiment](/sentiment_dist.png)

After cleaning the dataset:
- No duplicate reviews
- Still heavily imbalanced
  → ~92.6% positive reviews

This immediately tells: Accuracy alone will be misleading!

## What Customers Talk About

From simple word frequency:

![Positive reviews](/common_positive.png)

**Positive reviews**
→ fast delivery, good quality, matches expectation

**Negative and Neutral reviews**
→ tbh i can't really tell tho, but somehow, it mostly contains negation like `tidak` and `tapi`, as well as several stop words. 

## Modeling Approach

I tested multiple models:
- Naive Bayes
- Logistic Regression
- HistGradientBoosting

With simple TF-IDF approach that works by extracting keywords, count the term frequency and inverse document frequency, then combine those two. 

This approach works pretty well for short review, and more importantly, not that heavy. Fyi, this dataset have 9 words (after cleaned) in average (median).

![Length](/text_len.png)


**Key realization**

> More complex ≠ better

- Although boosting performed slightly better, it was ~20x slower
- So I chose Logistic Regression (fast + reliable)

## A Small but Important Improvement

Because the dataset is imbalanced, I adjusted prediction probabilities.

Instead of using raw probabilities:
- I corrected them using class distribution

Result:
- Better detection of negative & neutral reviews
- Overall improvement in F1 score, from 0.51 to 0.59

## What Are Customers Complaining About?

Using topic modeling (LDA), I found 3 main themes for negative reviews:

![Negative](/negative_topic.png)

1. Product Quality  
   → damaged, bad smell, not fresh  

2. Delivery & Packaging  
   → late delivery, broken packaging  

3. Product Match  
   → doesn’t match expectation, different color, size, etc.
   

## The Dashboard

![Dashboard](/dashboard.png)

[This app](https://customer-review.streamlit.app/) provides:

### Overview
- Sentiment distribution
- Trend of negative reviews
- Review length insights

### Topic Insights
- Main issues customers face
- Distribution of topics

### Review Explorer
You can input your own text and get (tho, somehow, maybe because of different package version, it failed to run):
- Sentiment prediction
- Topic interpretation

## Final Thoughts

Some key lessons from this project:

- Real-world data is messy and imbalanced  
- Metrics like accuracy can be misleading  
- Simple models can be very powerful  
- Combining sentiment + topic gives deeper insight  

## What’s Next?

- Try more advanced topic modeling (e.g., BERTopic)
- Improve interpretability of topics
- Enhance UI for better user experience
