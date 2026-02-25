---
layout: post
title: Drug Consumption Prediction
categories: [DS Projects]
tags: [classification, gradient boosting, random forest, drug consumption, threshold optimization]
description: "An undergraduate thesis: imbalanced data classification on drug consumption using threshold optimization combined with RF and GB." 
media_subpath: /assets/img/drug-consumption
---

Ah, since the original file is in Indonesian, should I do it in English, instead? Oh, such a weird logic, but let’s do it. It won’t be that long, right? Truth be told, it had a different structure than the one I usually worked on. It was somehow more mbulet — not in a simple straightforward structure (?). Also, it lacked some theoretical framework and reason on some of its steps.

Ah, ternyata lebih mudah jika menggunakan bahasa Indonesia. Tidak perlu menyiapkan mental model yang begitu besar. Maka, dengan senang hati, akan saya lanjutkan saja dengan bahasa Indonesia. Biarlah biar seperti ini saja. Sebelum lanjut, coba bayangkan skenario berikut. 

Pada pagi hari yang kelam, pada suatu rumah sakit, terdapat 100 orang antre untuk pemeriksaan penyakit. Kesemuanya memiliki gejala yang serupa: batuk, pilek, demam, juga ruam kemerahan pada sela-sela jari kaki. Diagnosis ditujukan untuk memeriksa virus varian baru, yang katanya, membawa efek yang amat sangat berbahaya. Sehingga, prediksi yang akurat akan sangat membantu.

Lewat uji lab historis, diketahui bahwa probabilitas seseorang yang memiliki gejala-gejala di atas terinfeksi virus ini adalah 2 persen. Masalahnya, demi kebutuhan cerita ini, uji lab dikatakan membutuhkan waktu 30 menit, itu pun tidak dapat dilakukan secara bersamaan, sehingga kurang efektif untuk pasien sebanyak itu. 

Lantas, saya, seorang statistisi andal, datang dengan pongahnya, membawa metode baru untuk keperluan diagnosis. Hanya butuh waktu kurang dari 5 menit, untuk melakukan diagnosis kepada seluruh pasien, dengan akurasi di atas 90 persen, bahkan mendekati 99 persen. Tidakkah saya terlihat heroik dan sungguhlah keren? 

Pada semua orang, saya katakan, “Itu gejala penyakit lain, anda tidak terinfeksi virus varian baru ini.” 

# Problem & Dataset
Dengan asumsi bahwa 2 dari 100 orang pada cerita di atas benar-benar terinfeksi virus varian baru, maka diagnosis yang saya lakukan hanya memiliki galat atau kesalahan prediksi sebesar 2 persen, atau dengan kata lain, memiliki akurasi sebesar 98 persen. Hebat, bukan?

Tentu saja tidak. Apa kabar 2 orang yang salah prediksi tersebut? Apakah dibiarkan saja untuk wafat lebih cepat? 

Cerita pengantar di atas merupakan satu permasalahan klasik dalam persoalan klasifikasi, yaitu data tidak seimbang (imbalanced data). Adanya ketidakseimbangan kelas pada distribusi data asal, yang ditunjukkan dengan perbedaan proporsi yang terpaut jauh, dapat membuat model cenderung bias ke kelas mayoritas. Hasilnya? Bahkan, dalam kasus ini, model dengan akurasi begitu tinggi (98 persen) bisa memberikan keputusan yang amat berbahaya.

Ah, kecuali jika kita hanya melihat nyawa sebagai statistik belaka. Itu lain lagi. 

Maka, pada tugas akhir tersebut, saya coba selesaikan permasalahan data tidak seimbang pada persoalan klasifikasi. Saya kombinasikan beberapa metode yang sudah ada untuk diterapkan pada data Drug Consumption (Quantified) dari UCI Machine Learning Repository. 

Data tersebut memuat hasil tes kepribadian serta frekuensi konsumsi 18 jenis NAPZA, baik legal maupun ilegal, pada 1885 responden. Terdapat 7 variabel prediktor hasil tes psikologi, yang mencakup NEO-FFI-R, BIS-11, dan ImpSS, serta 5 variabel prediktor kondisi sosiodemografi responden berupa level edukasi, usia, jenis kelamin, negara, dan etnis. 

Pada proyek ini, saya hanya berfokus pada satu variabel respon berupa konsumsi heroin, dengan **memodifikasi** 5 kelas frekuensi asal menjadi 2 kelas baru untuk memudahkan pengerjaan. Kelas pertama berlabel 0 menunjukkan bukan pengguna heroin, sedangkan kelas kedua berlabel 1 menunjukkan pengguna heroin. Kelas pertama terdiri atas responden dengan konsumsi heroin terakhir lebih dari satu dekade yang lalu atau tidak pernah sama sekali. 

# EDA (Exploratory Data Analysis)
Berikut ringkasan eksplorasi dan visualisasi data. Ringkas? Saya rasa tidak terlalu. Ah, sudahlah, toh *it is what it is*.

![hb](/heroin-barplot.png)

Gambar di atas menunjukkan sebaran kelas pada variabel respon, heroin. Label 0 menunjukkan kelas bukan pengguna heroin, sedangkan label 1 menunjukkan
kelas pengguna heroin. Dari grafik batang tersebut, dapat dilihat bahwa kelas positif, pengguna heroin, memiliki frekuensi yang jauh lebih rendah dibandingkan
kelas negatif (11.2% dibandingkan dengan 88.8%). Hal ini menunjukkan adanya ketidakseimbangan pada data, dengan IR (imbalanced ratio) sebesar 1:7.89.

![nb](/numeric-boxenplot.png)

Selanjutnya, gambar di atas merupakan boxen plot variabel prediktor numerik. Boxen plot
tersebut memperlihatkan sebaran variabel prediktor numerik untuk setiap kelas variabel respon heroin. Dari plot tersebut, dapat dilihat bahwa pengguna heroin cenderung memiliki nilai ascore, cscore, dan escore yang lebih rendah. Di lain sisi, pengguna heroin cenderung memiliki nilai impuslive, nscore, oscore, dan ss yang lebih tinggi.

![nb](/categoric-normalized.png)

Normalized bar plot di atas menunjukkan sebaran kelas pada variabel respon heroin terhadap kelas pada variabel prediktor. Dari grafik yang pertama, dapat dilihat bahwa seiring bertambahnya usia, proporsi pengguna heroin cenderung turun. Dari
grafik kedua, laki-laki cenderung memiliki proporsi pengguna heroin lebih tinggi
dibandingkan dengan perempuan. Dari grafik ketiga, meski ada sedikit inkonsistensi,
makin tinggi level edukasi responden, makin rendah pula proporsi pengguna heroin. Dari grafik keempat, responden yang berasal dari Selandia Baru, memiliki
proporsi pengguna heroin paling tinggi. Di lain sisi, responden dengan etnis mixed white-asian juga memiliki proporsi pengguna heroin paling tinggi. Hanya saja, melihat rendahnya representasi responden dari negara dan etnis tersebut yang dapat
dilihat pada gambar di bawah, tidak dapat diambil kesimpulan bahwa negara dan etnis
tersebut lebih buruk dari yang lain.

![nb](/categoric-unnormalized.png)

# Modeling
Sebelum masuk ke pemodelan, marilah kita bahas metrik evaluasi yang digunakan dalam proyek kali ini.



# Model Comparison


# Tech Stack
- Language: Python
- Libraries: pandas, numpy, matplotlib, seaborn, scikit-learn

# Conclusion & Reflection (?)
Ambil saja satu dua hikmahnya, jika memang selalu seperti itu. 

