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

Key Visualizations

Inventory Trend

Shows how inventory levels evolved over time.
The trend indicates a sharp increase from late December to early February followed by a gradual decline toward June.

This suggests seasonal stock buildup followed by normalization.

Inventory Value by Category

Technology products represent the largest share of inventory value.
This may indicate higher product prices or stronger demand within that category.

Stock Level Distribution

Inventory levels show a right-skewed distribution, with most products stocked below 500 units.

Interestingly, the distribution appears bimodal, suggesting standardized stocking tiers rather than purely demand-driven inventory decisions.

Low Stock Risk Products

No products were found below their reorder point.
Even the most at-risk items remain roughly 100–150 units above their reorder thresholds, indicating conservative safety stock policies.

Dashboard 2 — Inventory Efficiency Analysis

This dashboard focuses on operational efficiency and identifies products that may be tying up capital or posing supply risks.

Units Sold vs Inventory

This scatter plot compares demand with inventory levels.

Key observations:

Inventory levels cluster around three tiers (~200, ~400, and ~800 units)

Units sold vary within a narrow range (approximately 1100–1300)

This suggests inventory levels may follow fixed stocking policies rather than demand-driven allocation.

Fast vs Slow Moving Products

Fast-moving products:

Binders Model 2

Chairs Model X39

Storage Model 3

Slow-moving products:

Storage Model 1

Paper Model 3

Chairs Model 3

While all products show inventory turnover greater than one, indicating inventory does move during the period, relative differences still highlight potential inefficiencies.

Slow-moving items may occupy warehouse space longer and tie up working capital.

Inventory Turnover Analysis

Products with lower turnover ratios may benefit from:

Reduced reorder quantities

Adjusted safety stock levels

Closer monitoring of demand trends

This helps prevent overstocking and improves inventory utilization.

Supplier Risk Analysis

Supplier C presents the highest operational risk:

Average lead time: ~14 days

Highest observed stockout rate

Longer replenishment cycles increase the likelihood of stock shortages.

Possible mitigation strategies include:

Increasing safety stock for Supplier C products

Negotiating faster delivery times

Diversifying suppliers

Key Insights

Demand across products is relatively consistent, with units sold falling within a narrow range.

Inventory levels appear to follow predefined stocking tiers, suggesting potential misalignment between demand and stocking policies.

Some products exhibit slower turnover, indicating opportunities to optimize reorder strategies and reduce excess stock.

Supplier C introduces supply chain risk due to longer lead times, which may require additional inventory buffers or supplier renegotiation.

Recommendations

Based on the analysis:

Implement demand-driven inventory policies instead of fixed stocking tiers.

Adjust reorder quantities for slow-moving products.

Review supplier contracts to reduce lead time variability.

Maintain safety stock buffers for products with long supplier lead times.

These improvements could reduce holding costs, improve stock availability, and optimize working capital usage.

Project Structure
inventory-analysis/
│
├── data/
│   └── inventory_dataset.csv
│
├── dashboards/
│   └── tableau_dashboard.twb
│
├── images/
│   └── dashboard_screenshots.png
│
└── README.md
Conclusion

This project demonstrates how data analytics and visualization tools can be used to evaluate inventory health, identify inefficiencies, and support better operational decision-making.

The approach illustrates a typical workflow for business intelligence analysts working on supply chain or retail inventory optimization problems.



