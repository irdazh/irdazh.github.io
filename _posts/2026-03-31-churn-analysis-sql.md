---
layout: post
title: Churn Analysis (SQL)
categories:
- DA Projects
tags:
- SQL
- Business Intelligence
- Python
description: 'Churn drivers: customer behavior analysis using simple SQL and Python'
media_subpath: "/assets/img/churn-analysis-sql"
date: 2026-03-31 09:04 +0700
---
# Customer Churn Analysis (SQL + Python)

Apa ini? Lagi-lagi sebuah saduran dari *readme* kah? Iya lagi. Iya lagi.

Yak, sila ke [sini](https://github.com/irdazh/churn-analysis-sql) untuk melihat sumber serta duplikatnya, LOL.

## Project Overview
1. Menganalisis perilaku *churn* pada customer (pelanggan berhenti berlangganan)
2. Guna identifikasi **faktor kunci** pemengaruh retensi pelanggan
3. Menggunakan SQL & Python pada customer tenure, contract type, pricing, dan service usage untuk melihat pola dan memahami mengapa pelanggan **churn**.
4. Tujuan: analytical thinking (what a BS, i was using ChatGPT), SQL proficiency (idem, supposed to be understanding), ubah data ke business insights (using ChatGPT). 

## Business Problem

Ah, customer churn merupakan isu kritis nan penting di subscription businesses, yang mana secara langsung berpengaruh pada revenue dan growth (pendapatan dan pertumbuhan)

Maka, proyek ini ditujukan untuk menjawab pertanyaan berikut:   
* Churn rate keseluruhan? 
* Pelanggan manakah yang kemungkinan churn-nya tinggi? 
* Faktor apa saja yang berasosiasi dengan tingkat churn tinggi? 
* Kecenderungan apa yang dimiliki pada pelanggan yang churn?

## Dataset

Dataset yang digunakan diunduh dari [kaggle dataset](https://www.kaggle.com/datasets/yeanzc/telco-customer-churn-ibm-dataset) yang mengandung informasi pelanggan dari bisnis langganan telekomunikasi, mencakup: 
* Demografis pelanggan
* Informasi akun (tenure, contract type)
* Layanan (internet service, support)
* Informasi billing (monthly & total charges)
* Status churn (Yes/No)

## Tools Used
* SQL (SQLite) -- Analisis utama dan segementasi pelanggan
* Python (pandas, matplotlib, seaborn) -- Data cleaning dan visualisasi
* Kaggle Notebook -- Analysis environment (IDE?)
* GitHub -- Dokumentasi

## Analysis Approach

### 1. Data Cleaning

1. Menangani missing values (meskipun nggak ada, LOL)
2. Mengubah status churn ke format biner 0, 1 (sudah dari sananya, awoakwokao)
3. Ubah tipe data (Total Charges ke numerik)

### 2. EDA

Analisis utama -- sila buka notebook sajalah untuk melihat visualisasi -- yang mencakup: 
1. Tingkat churn
2. Churn berdasar tenure group
3. Churn berdasar contract type
4. Churn berdasar monthly charges
5. Segmentasi pelanggan menggunakan dua faktor (contract type dan internet service)

### 2B. Viz Explanation 

Nah, just because I think I'll love it. 
1. Missing value
   
   ![Missing value](/missing_value.png)    
   Oh tidak, ada missing value di Churn Reason.... Oh, tenanglah saja, buat apa pelanggan non-churn mengisi alasan untuk churn? Eak.

2. Tenure months
   
   ![TM](/churn_tenure_cont.png)   
   Terlihat kan? Bagaimana (kecuali 0 tenure months) makin lama tenur, proporsi pelanggan churn cenderung turun. Hal serupa dapat dilihat dari barplot di bawah, ketika kita coba kelompokkan tenur, makin singkat lama tenur makin besar pula proporsi pelanggan churn.    
  ![TM](/churn_tenure_disc.png)

1. Contract type
   
   ![CT](/churn_contract.png)   
    Saya rasa jelas ya, serupa dengan tenure months. Makin rendah tipe kontrak-nya (month-to-month), makin tinggi juga proporsi churn-nya: 40 persen, wagelaseh? (sounds like a boomer)

2. Monthly charges
   
   Ah, bagian ini sangat menarik, favorit saya. Karena setelah berpusing mencari plot yang cocok. Akhirnya, dapat juga density plot (?) Satu, pelanggan non-churn secara umum lebih banyak ketimbang pelanggan churn untuk rentang biaya bulanan mana pun. Dua, dilihat secara lebih detail, pelanggan non-churn memiliki dua puncak, di biaya bulanan rendah (20an) dan tinggi (80an). Tiga,  di lain sisi, density (proporsi) pelanggan churn naik seiring biaya bulanan yang makin tinggi. 

   Simpulan? Biaya bulanan berkorelasi positif dengan proporsi pelanggan churn.
   
   ![DP](/monthly_density.png)
   
   Visual diskrit dapat dilihat pada plot di bawah. Jelas saja, lebih mudah dibaca. 

   ![DP](/monthly_disc.png)


4. Sebetulnya masih ada satu (?) lagi. Tapi sudahlah. Segitu juga lebih dari cukup. 

### 3. SQL Analysis

Digunakan untuk .... menjawab pertanyaan di atas. Ah, \***!

## Key Insights

Jadi, berikut insight-insight yang didapat: 
1. Secara keseluruhan, tingkat churn sekitar 26.5 persen, mengindikasikan adanya cukup banyak pelanggan yang meninggalkan layanan telekomunikasi ini. 
2. Lama tenure berasosiasi kuat dengan tingkat churn     
   * Pelanggan dengan tenure jangka pendek lebih tinggi kemungkinannya untuk churn
   * Pelanggan jangka panjang (ew, what a translation) secara signifikan lebih stabil
3. Tipe contract merupakan faktor utama untuk churn
   * Month-to-month contract punya tingkat churn paling tinggi
   * Contract jangka panjang (tahunan) secara signifikan mengurangi tingkat churn. 
4. Besaran biaya bulanan berasosiasi dengan tingkat churn. 
   * Pelanggan yang churn cenderung memiliki biaya bulanan lebih tinggi.
   * Indikasi adanya price sensitivy atau perceived low value -- ya? 
5. Pelanggan dengan fiber optic internet dan month-to-month contract merupakan pelanggan high-risk (pelanggan dengan tingkat churn tertinggi)

## Business Interpretation

Why whould i do this? Please. 

Analisis di atas menunjukkan bahwa churn didorong atas kombinasi dari beberapa faktor, mencakup:
* Komitmen rendah (month-to-month contract)
* Pelanggan tingkat awal (short tenure)
* Beban biaya tinggi (higher monthly charges)

Faktor-faktor tersebut mengindikasikan bahwa pelanggan riskan untuk churn ketika mereka belum "memiliki kesetiaan" (ew, translation (2)) dan menganggap bahwa layanan yang ada tidaklah worth it dibanding harganya.

## Recommendations

Berdasarkan temuan-temuan di atas, maka beberapa rekomendasi: 
1. Melalui insentif (diskon, pun promosi), dorong pelanggan untuk beralih langganan ke kontrak jangka panjang
2. Untuk pelanggan baru, tingkatkan pengalaman onboarding untuk mengatasi early churn
3. Target kelompok berisiko tinggi (fiber optic + month-to-month user) dengan retention campaigns --- it is what it is, dude. 


## Conclusion

Yak, proyek ini -- secara sangat sederhana -- mendemonstrasikan penggunaan SQL (we don't really need it tbh, hhh) dan Python untuk menganalisis perilaku pelanggan, mengidentifikasi faktor pendorong churn, serta saran yang dapat diaplikasikan. 

Pendekan ini merefleksikan (well, i somehow don't think so) workflow yang jamak digunakan data analis pada problem customer retention dan subscription analytics (?) 

That's it guys. For now, I think I'm done for this \*\*\*st thing, and yeah, see u next time~
