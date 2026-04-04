---
layout: post
title: "Understanding Customer Reviews: Sentiment & Topics"
categories:
- DS Projects
tags:
- classification
- nlp
description: 'An undergraduate thesis: imbalanced data classification on drug consumption
  using threshold optimization combined with RF and GB.'
media_subpath: "/assets/img/customer-review"
---

## Goals
Companies receive thousands of customer reviews but cannot read them all. 
The goal is to automatically analyze them and answer questions like:
1. What percentage of reviews are positive, neutral, or negative?
2. What main issues customers complain about?
3. Are complaints increasing over time?
4. Which product categories have the worst sentiment?

Deliverable:
- NLP analysis
- Insight dashboard
- Clear business recommendations

## Dataset
I'll use Tokopedia product reviews dataset in kaggle by idk, lemme look it up later. 
It's heavily imbalanced and upon looking it yesterday, still uncleaned and raw. 

## System Architecture
- (Main) Pipeline: raw reviews, data cleaning, EDA, sentiment classification, 
- Later On: topic modeling, insights, dashboard

## Log
1. Wed, 11 March: plan, ideas, brainstorming, get the data: tokped
2. Fri, 13 March: copasting from kaggle's notebooks, chatting with GPT, trying in kaggle
   doing raw reviews, do text cleaning, stuck at stopwords and lemmatization, should we do it?


## 🧠 Why I Built This

When looking at e-commerce reviews, a simple question came up:

> “Are customers actually satisfied, and if not, why?”

This project explores that using:
- Sentiment analysis
- Topic modeling
- An interactive dashboard

---

## 📊 The Data Reality

After cleaning the dataset:
- No duplicate reviews
- Still heavily imbalanced  
  → ~92.6% positive reviews

This immediately tells us:

⚠️ Accuracy alone will be misleading

---

## 🔍 What Customers Talk About

From simple word frequency:

**Positive reviews**
→ fast delivery, good quality, matches expectation

**Negative reviews**
→ complaints, dissatisfaction, broken items

**Neutral reviews**
→ more contextual and less emotional

---

## 🤖 Modeling Approach

I tested multiple models:
- Naive Bayes
- Logistic Regression
- HistGradientBoosting

### Key realization:

> More complex ≠ better

Although boosting performed slightly better:
- It was ~20x slower

So I chose:

✅ Logistic Regression (fast + reliable)

---

## ⚙️ A Small but Important Improvement

Because the dataset is imbalanced, I adjusted prediction probabilities.

Instead of using raw probabilities:
- I corrected them using class distribution

Result:
- Better detection of negative & neutral reviews
- Overall improvement in F1 score

---

## 🧠 What Are Customers Complaining About?

Using topic modeling (LDA), I found 3 main themes:

1. Product Quality  
   → damaged, bad smell, not fresh  

2. Delivery & Packaging  
   → late delivery, broken packaging  

3. Product Match  
   → doesn’t match description  

---

## 📊 The Dashboard

The app provides:

### 📌 Overview
- Sentiment distribution
- Trend of negative reviews
- Review length insights

### 🧠 Topic Insights
- Main issues customers face
- Distribution of topics

### 🔍 Review Explorer
You can input your own text and get:
- Sentiment prediction
- Topic interpretation

---

## 💡 Final Thoughts

Some key lessons from this project:

- Real-world data is messy and imbalanced  
- Metrics like accuracy can be misleading  
- Simple models can be very powerful  
- Combining sentiment + topic gives deeper insight  

---

## 🚀 What’s Next?

- Try more advanced topic modeling (e.g., BERTopic)
- Improve interpretability of topics
- Enhance UI for better user experience


  
