---
layout: post
title: Inventory Analytics Dashboard
categories:
- DA Projects
tags:
- dashboard
- business intelligence
- inventory analytics
description: 'BI project: a not so simple dashboard on Inventory System.'
media_subpath: "/assets/img/inventory-analytics"
---

Kalau toh sebagian besarnya diselesaikan oleh AI, untuk apa bersusah payah mengetik manual?  
Oh iya, tunggulah versi terbaru di masa depan yang tidak pasti itu. 

## Project Overview
Proyek ini menganalisis performa inventaris untuk memahami efisiensi stok, risiko supplier, 
dan potensi optimasi keduanya. Menggunakan dataset inventaris retail hasil simulasi ChatGPT,
analisis berfokus pada identifikasi pola pada jumlah stok, permintaan produk, serta performa supplier. 

Ringkasnya, bagaimana kita menggunakan data analytics dan business intelligence untuk 
membantu membuat keputusan terarah pada manajemen inventaris.

## Business Problem
Manajemen inventaris memainkan peranan penting dalam industri retail. Manajemen yang serampangan dapat menyebabkan: 
- Kelebihan stok yang memakan modal
- Kekurangan stok yang mengurangi penjualan
- Inefisiensi terhadap supplier
- Strategi reorder yang tidak selaras

Sehingga, proyek ini ditujukan untuk menjawab beberapa pertanyaan kunci: 
1. Apakah tingkat stok saat ini sehat?
2. Produk mana yang terjual cepat atau lebih lambat?
3. Apakah kebijakan inventarisasi saat ini selaras dengan permintaan?
4. Apakah ada risiko terkait supplier yang memengaruhi ketersediaan stok?

## Dataset
Dataset ini didesain menyerupai sistem inventarisasi di industri retail. 
Terdiri atas 7200 baris hasil simulasi ChatGPT yang merupakan catatan inventarisasi 40 produk selama 180 hari (6 bulan). 
Terdapat 8 fitur utama: product name, category, supplier, inventory level, units sold, reorder point, lead time, dan inventory value. 

## Dashboard 1 -- Inventory Health Overview
Dashboard ini memberikan gambaran umum dari performa inventaris 

### Key Metrics
- Inventory Value: total stok saat ini ketika diuangkan (monetary value)
- Inventory Turnover: menunjukkan seberapa sering persediaan terjual dan diganti
- Days of Inventory: rerata jumlah hari produk menginap di gudang
- Stockout Rate: persentase kasus tidak terpenuhinya permintaan karena kurangnya stok 

### Key Visualizations
1. Inventory Trend

