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
date: 2026-02-25 00:00 +0000
---
Kalau toh sebagian besarnya diselesaikan oleh AI, untuk apa bersusah payah mengetik manual? 
Jika hendak mengotak-atik dashboard secara langsung, lakukan [di sini!](https://public.tableau.com/app/profile/daud.muhamad.azhari/viz/InventorySupplyChainAnalytics/Dashboard1)

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
- Inventory Value: total stok saat ini ketika diuangkan (monetary value), sekitar $340 juta 
- Inventory Turnover: menunjukkan seberapa sering persediaan terjual dan diganti, sebesar 105 unit
- Days of Inventory: rerata jumlah hari produk menginap di gudang, selama 69 hari
- Stockout Rate: persentase kasus tidak terpenuhinya permintaan karena kurangnya stok, hanya sekitar 2%

### Key Visualizations
1. Inventory Trend

    Grafik di bawah menunjukkan trend jumlah stok seiring waktu. Grafik tersebut mengindikasikan adanya kenaikan tajam dari akhir Desember hingga awal Februari, yang diikuti dengan penurunan secara bertahap hingga bulan Juni. 

    ![inventory](/trend.png)

    Hal di atas menunjukkan adanya penumpukan stok musiman yang diikuti dengan proses normalisasi. 

1. Inventory Value by Category

    ![Graph here](/category.png)

    Produk-produk teknologi menyumbang nilai inventaris terbesar, meski tidak jauh berbeda dengan kategori lain. Hal ini bisa saja mengindikasikan harga produk ataupun permintaan yang lebih tinggi pada produk dalam kategori teknologi. 

3. Stock Level Distribution

    Jumlah stok menunjukkan distribusi menceng kanan, dengan mayoritas produk memiliki stok di bawah 500 unit. 

    ![level](/level.png)
    
    Menariknya, distribusi terlihat memiliki dua puncak, menandakan adanya standardisasi dalam proses inventarisasi, bukan murni berdasarkan jumlah permintaan pasar. 

4. Low Stock Risk Products

    ![low](/low.png)

    Tidak ada produk dengan stok kurang dari reorder point. 
    
    Bahkan pada item dengan risiko paling tinggi, tetap memiliki sekitar 100 hingga 150 unit di atas ambang batas reorder, mengindikasikan strategi inventarisasi yang cenderung konservatif.

## Dashboard 2 — Inventory Efficiency Analysis
Dashboard kedua berfokus pada efisiensi operasional: identifikasi produk yang membutuhkan modal penyimpanan besar serta produk yang memiliki risiko ketersediaan.  

1. Units Sold vs Inventory  
Scatter plot berikut membandingkan tingkat permintaan dengan tingkat persediaan. 

    ![scatter](/scatter.png)

    Poin-poin inti: 
       - Tingkat persediaan terkluster di sekitar tiga level (~200, ~400, dan ~800 unit)
       - Jumlah unit yang terjual cenderung seragam, memiliki variasi yang rendah (sekitar 1100–1300)
       - Hal ini menunjukkan bahwa tingkat persediaan mungkin mengikuti strategi inventarisasi tetap daripada dialokasikan berdasarkaan jumlah permintaan. 

1. Fast vs Slow Moving Products
   - Top 3 produk dengan laju tercepat: Binders Model 2, Chairs Model X39, Storage Model 3
   - Top 3 produk dengan laju terlambat: Storage Model 1, Paper Model 3, Chairs Model 3

    ![fastmoving](/fastmoving.png)

    Meskipun semua produk menunjukkan perputaran persediaan (inventory turnover) lebih dari satu, yang menunjukkan bahwa persediaan memang bergerak selama periode tersebut, perbedaan relatif bisa jadi menunjukkan potensi inefisiensi.

    Barang dengan laju lambat cenderung menempati ruang gudang lebih lama dan dapat meningkatkan biaya penyimpanan.

2. Inventory Turnover Analysis

    ![turnover](/turnover.png)

    Produk dengan rasio perputaran (inventory turnover) yang lebih rendah dapat disiasati dengan:
      - Pengurangan jumlah pemesanan ulang (reorder
      - Penyesuaian tingkat stok pengaman (safety stock)
      - Pemantauan tren permintaan yang lebih ketat (demand trend)

    Hal ini ditujukan untuk mencegah kelebihan stok dan meningkatkan pemanfaatan inventaris.

1. Supplier Risk Analysis
   
    Dari grafik di bawah, Supplier C memiliki risiko operasional tertinggi:
    - Waktu tunggu rata-rata: ~14 hari
    - Tingkat kekurangan stok tertinggi yang diamati
    - Siklus pengisian ulang yang lebih panjang meningkatkan kemungkinan kekurangan stok.

    ![supplier](/supplier.png)

    Maka dari itu, beberapa mitigasi yang dapat dilakukan:
      - Meningkatkan stok pengaman untuk produk dari Supplier C
      - Negosiasi waktu pengiriman yang lebih cepat
      - Diversifikasi ke supplier lain 

## Key Insights
- Permintaan di seluruh produk relatif konsisten, dengan unit yang terjual berada dalam kisaran yang sempit.
- Tingkat persediaan tampaknya mengikuti tingkatan stok yang telah ditentukan sebelumnya, menunjukkan potensi ketidaksesuaian antara permintaan dan kebijakan penyimpanan.
- Beberapa produk menunjukkan perputaran yang lebih lambat, menunjukkan peluang untuk mengoptimalkan strategi pemesanan ulang (reorder) dan mengurangi kelebihan stok.
- Supplier C memiliki risiko ketidaksediaan tinggi karena lamanya waktu tunggu, yang mungkin memerlukan buffer persediaan tambahan atau negosiasi ulang.

## Recommendations
Berdasarkan analisis di atas:   
  - Terapkan kebijakan persediaan berbasis permintaan, bukan tingkatan persediaan tetap.
  - Sesuaikan jumlah pemesanan ulang untuk produk yang pergerakannya lambat.
  - Tinjau kontrak dengan supplier untuk mengurangi variabilitas waktu tunggu.
  - Tambahkan buffer sebagai pengaman untuk produk dengan waktu tunggu yang lama.

Hal-hal di atas dapat mengurangi biaya penyimpanan, meningkatkan ketersediaan stok, dan mengoptimalkan penggunaan biaya penyimpanan.

## Conclusion
Proyek ini menunjukkan bagaimana data analytics dan alat visualisasi dapat digunakan untuk mengevaluasi status inventarisasi, mengidentifikasi inefisiensi, dan mendukung pengambilan keputusan operasional yang lebih baik.

Pendekatan ini menggambarkan workflow yang umum digunakan analis business intelligence dalam menyelesaikan masalah optimasi rantai pasok dan inventarisasi dalam industri retail.

