---
layout: post
title: House Price Prediction
date: 2026-02-24 15:12 +0700
categories: [DS Projects]
tags: [regression, xgboost, house price, streamlit]
description: "End-to-end ML project: regression modeling using XGBoost on house prices with Streamlit deployment." 
media_subpath: /assets/img/house-price
---

Mulai dari mana baiknya? Ah, iya, tentu saja sebuah klarifikasi!

Berhubung kemampuan bahasa Inggris saya sedang dalam tahap perbaikan, maka, usahlah kita ubah menggunakan bahasa sehari-hari, yakni, Indonesia. Alasan lain, versi bahasa Inggris dapat dilihat lewat pranala berikut ini: [https://github.com/irdazh/house-price-prediction](https://github.com/irdazh/house-price-prediction), pada bagian README. Kurang lebihnya, versi ini merupakan saduran dari versi bahasa Inggris tersebut. 

# Permasalahan dan Dataset

Pada proyek kali ini, saya buat model machine learning untuk memprediksi harga rumah. Saya buat beberapa model machine learning, mencakup model linear serta model pepohonan (tree-based model), membandingkannya, lantas memilih satu model terbaik untuk ditempatkan ke dalam aplikasi web sederhana (model deployment) menggunakan Streamlit.

Proyek ini menggunakan Ames Housing Dataset dari kompetisi di platform Kaggle, yang tentu saja tidak relevan dengan harga rumah di Indonesia. Data tersebut terdiri atas 1460 baris, dengan target berupa harga penjualan rumah (SalePrice) serta 79 fitur dengan beragam jenis, yang mencakup numerik, ordinal, dan nominal. Beberapa contoh dari fitur tersebut adalah kualitas material rumah (OverallQual), wilayah perumahan (Neighborhood), tipe rumah (MSSubClass), tahun konstruksi (YearBuilt), dan luas bangunan (GrLivArea).

# EDA (Eksplorasi Data)
Dari statistik deskriptif dan visualisasi data yang telah saya buat, didapatkan beberapa simpulan, yang saya terakan di bawah. 

![spd](/sale-price-distribution.png){: h="30" .normal}

Variabel target, yaitu harga penjualan rumah (SalePrice), selayaknya variabel perekonomian lainnya, memiliki distribusi yang cenderung menceng kanan (right-skewed).  Mayoritas rumah memiliki harga standar pada rentang 100 ribu hingga 300 ribu, tetapi ada sebagian kecil rumah yang mencapai harga pada rentang 500 ribu hingga 700 ribu.

![mvh](/missing-value-heatmap.png){: h="30" .left}

Dari heatmap tersebut, terdapat data yang hilang (missing values) pada 19 fitur, baik sistematis ataupun acak. Dalam tahap pemodelan nantinya, fitur dengan data yang hilang berjumlah masif, lebih dari 80 persen, akan dibuang dari model. Sedangkan sisanya, akan dilakukan imputasi. 

![frk](/feature-rank-correlation.png){: h="30" .right}

Heatmap tersebut menunjukkan Korelasi Rank Spearman untuk 14 fitur paling berkorelasi dengan variabel target. Dapat dilihat bahwa hanya beberapa fitur yang berkorelasi sangat kuat dengan variabel target. Di lain sisi, beberapa fitur malah berkorelasi kuat satu dengan yang lainnya. 

![cb](/categorical-boxenplot.png){: h="30" .normal}

Berikutnya ditampilkan boxenplot dari variabel target SalePrice untuk seluruh kelas dari 4 fitur terpilih, yaitu OverallQual, Neighborhood, MSSubClass, dan FullBath. Dari plot pertama, dapat dilihat bahwa bahwa meningkatnya OveralQual dibarengi dengan meningkatnya nilai dari SalePrice. Kedua, wilayah perumahan IDOTRR, MItchel, dan StoneBr terlihat memiliki median harga rumah tertinggi, sedangkan median harga rumah terendah ada di wilayah Sawyer; hal ini menunjukkan adanya korelasi antara harga rumah dengan wilayah perumahan. Ketiga, tipe rumah dengan kode 60 (rumah 2 lantai tipe baru) dan kode 120 (rumah 1 lantai di kawasan terpadu tipe baru) cenderung memiliki median harga rumah yang tinggi, sedangkan rumah dengan kode 30 (rumah 1 lantai tipe lawas) memiliki median harga paling rendah; hal ini juga menunjukkan adanya korelasi antara harga rumah dan tipe rumah. Terakhir, jumlah kamar mandi lengkap (?) juga terlihat berkorelasi dengan harga rumah.

![ns](/numerical-scatterplot.png){: h="30" .normal}

Untuk keempat scatterplot di atas, sila lakukan interpretasi sendiri. Bukan suatu hal yang susah, kan?  

# Pemodelan dan Komparasi

Sebelum masuk ke pemodelan, pada tahap preprocessing, dilakukan split data sebanyak 80 persen untuk data latih dan 20 persen sisanya untuk data uji. Pada data yang hilang, dilakukan imputasi menggunakan kelas baru (None) untuk fitur nominal, serta nilai median untuk fitur numerik dan ordinal. Saya lakukan standardisasi menggunakan StandardScaler untuk fitur numerik (hanya dilakukan untuk model dasar) serta kodifikasi menggunakan OrdinalEncoder untuk fitur nominal. 

Saya gunakan 2 metrik evaluasi dalam proyek kali ini, MSLE dan RMSE. MSLE (root mean squared log error) digunakan untuk memilih model terbaik, yang cocok digunakan untuk variabel target yang memiliki distribusi mendekati log normal (?). Evaluasi dilakukan dengan menggunakan validasi silang 5-fold pada data uji. Hanya saja, untuk interpretasi model, digunakan RMSE (root mean squared error) digunakan untuk memudahkan interpretasi galat model. Aneh? Memang; saya sendiri juga berpikir semacam itu. Mungkin lain kali, harusnya gunakan satu metrik evaluasi saja: gunakan satu metrik yang simpel atau  menyesuaikan tujuan awal pemodelan. 

Pada tahap pemodelan ini, banyak eksperimen yang saya lakukan. 

![mbc](model-basic-comparison.png)
_Basic Model Comparison_

Pertama, untuk pemodelan dasar, dibentuk 4 model linear, 1 KNN, serta 4 model pepohonan. Selain itu, ditambahkan pula beberapa fitur baru (lewat feature engineering) yang pernah saya dapatkan dari platform belajar Kaggle. Meski sayang sekali, keempat fitur baru yang saya buat tidak lebih berguna dari fitur-fitur lainnya. Hasilnya mungkin dapat ditebak, model pepohonan memiliki performa terbaik, diikuti dengan model linear, dan model dengan performa terburuk adalah model KNN, seperti yang dapat dilihat pada gambar di atas. 

Setelahnya, dilakukan pemodelan lebih lanjut pada model pepohonan, menggunakan hyperparameter tuning untuk mendapatkan model dengan konfigurasi terbaik dengan metrik evaluasi MSLE paling rendah. Singkat cerita (karena penjelasan rumit yang tidak diperlukan), didapatkan model terbaik berupa XGBoost dengan parameter tertentu. Meski sebetulnya, peningkatan performa yang ada sangat amat kecil dan terlihat tidak signifikan, tapi tak apalah, tetap saya gunakan sebagai model terbaik untuk saat. 

Sebagai tambahan, sebetulnya, dilakukan juga pemodelan dengan menggunakan hanya sebagian fitur berdasarkan nilai dari mutual information. Tentu saja model ini memiliki performa di bawah model dengan seluruh fitur. Hanya saja, meski model ini bukanlah model terbaik, pendekatan dengan menggunakan sebagian fitur cocok digunakan untuk kondisi lain ke depannya. 

# Model Terbaik dan Interpretasinya

Model terbaik didapat dengan menggunakan algoritma XGBoost dengan hyperparameter tuning. Model tersebut memberikan nilai MSLE terendah sebesar 0.138 dan RMSE sebesar 25,612 (atau sekitar 15.7% deviasi jika kita bandingkan dengan median harga rumah). Tidak seburuk itu, kan? 

![svp](shap-value-plot.png)
_SHAP Feature Importance_

Berdasarkan plot SHAP feature importance di atas, didapatkan 5 fitur paling penting, yang positif memengaruhi harga rumah adalah OverallQual, GrLivArea, TotalBsmtSF, BsmtFinSF1, dan GarageCars. Dalam bahasa manusia, kelima fitur tersebut adalah: kualitas material rumah, luas bangunan, luas area rubanah (basement), luar area rubanah dengan kualitas tertentu (?), serta kapasitas garasi. 

Sepertinya, analisis mendalam terhadap fitur-fitur tersebut akan sangat amat menarik. Tentu saja tidak untuk sekarang: saya sudah bosan dengan seluruh perulangan ini. Hal-hal lawas yang terus ditunda, dijadikan beban di masa mendatang.

# Aplikasi Web
Model terbaik yang telah didapatkan, yaitu XGBoost dengan menggunakan seluruh fitur, tanpa ada embel-embel *feature engineering*, lantas ditempatkan dalam sebuah aplikasi web sederhana menggunakan Streamlit. Sila kunjungi pranala berikut untuk melakukan demo secara langsung: [https://irdazh-house-price-prediction.streamlit.app/](https://irdazh-house-price-prediction.streamlit.app/)!

Pada pembuatan aplikasi web ini, dilakukan pengurangan pada fitur-fitur yang dapat dimasukan oleh pengguna. Dari puluhan faktor penentu harga rumah, hanya akan digunakan 7 fitur yang sekiranya penting (dan juga tidak penting, hanya sekadar untuk uji coba), meliputi: kualitas material rumah, tahun konstruksi, luas bangunan, luas rubanah, kualitas eksterior, kapasitas garasi, dan tipe garasi. Sedang fitur sisanya, dianggap sebagai *missing value*, dan dilakukan imputasi serupa ketika proses pemodelan. 

Pada data numerik dan ordinal, imputasi dilakukan dengan menggunakan nilai median, sehingga, model akan menggunakan nilai rataan yang harusnya terhitung valid untuk data baru. Seharusnya, hal ini tidaklah menimbulkan masalah. Di lain sisi, pada data nominal, imputasi dilakukan dengan membuat kelas baru, yang mana, untuk fitur tanpa *missing value*, hal itu belum dipelajari dalam proses pemodelan. Sehingga, entahlah, mungkin model akan menghasilkan interpolasi yang cenderung bias, mengarang bebas, atau semacamnya?

Ah, untuk sekarang, lupakan saja. Masih bukan ranah dan detailnya. 

![hpp](/hpp-app.png)

Aplikasi web tersebut memiliki beberapa fitur, mencakup: laman masukan detail rumah, informasi model, hasil prediksi yang ditampilkan dengan gauge chart (nirguna), perbandingan hasil prediksi dengan rumah serupa, serta dua fitur lain yang sejatinya lebih baik untuk dihapus saja. Apa pasal saya gunakan gauge chart untuk hasil prediksi? 

# ✨Tumpukan Teknologi✨
- Language: Python
- Libraries: pandas, numpy, matplotlib, seaborn, scikit-learn, xgboost, lightgbm, shap (opsional)
- Dashboard: Streamlit
- Version Control: Git, GitHub
- Deployment: Streamlit Cloud

# Simpulan & Refleksi
Petuah bilang, lebih baik terlambat daripada tidak sama sekali. Lantas, apakah tunda-menunda masuk ke dalamnya? Toh, tetap dilakukan, meski membuat terseok hingga akhir.

*I really wanna blabber about projects I did and competitions I had won in college. Yes, it all mostly was about data analysis and modeling to this kind of level. Yet. It took me a really long time to finish this project. Slowly. Full of boredom. It yet just shows how little I know about this field. I hate it. Stuck at this level, and slowly getting worse and worse. Without any plan or whatsoever. So what's next?*

Mungkin begitulah, tetapi tetap saja, harusnya ada banyak sekali hal baru yang dipelajari, kan?
1. Lokal: hampir seluruh proyek yang saya kerjakan saat masa kuliah menggunakan kaggle, colab, atau platform daring lainnya -- maka, ini sebuah kebaruan; 
2. Git & GitHub: masih level dasar, tapi paling tidak, dapat paham garis besarnya. 
3. Streamlit: kalau ini benar-benar baru, meskipun tentu saja hanyalah *vibe coding* dengan bantuan bot LLM.

Banyak sekali, katanya, *smirk*. Lantas, untuk ke depan?
1. Dari apa yang saya pelajari ketika *probation* sekian minggu, satu hal penting yang melekat adalah intensi, atau niatan. Maka, bagian permasalahan awal menjadi titik pusat atas segalanya -- simpan-simpanlah dulu distraksi semenarik apapun itu. 
2. Lantas, pada tahapan eksplorasi data, awali dengan mencatat asumsi yang melekat pada data. Buatlah batasan pada simpulan nantinya, yang selaras dengan data tersebut.
3. Selanjutnya, tampilkan ringkasan data dan buat visualisasi umum secara keseluruhan menggunakan templat, sebelum masuk ke visualisasi khusus hanya untuk fitur-fitur yang secara teoretis penting dan relevan.
4. Bisa gunakan derajat korelasi, asosiasi, atau mutual information (tidak disarankan), meski tetap saya sarankan untuk fokus ke informasi visual.
5. Tentukan metrik evaluasi yang sederhana, makin sedikit makin baik. 
6. Pada tahapan preprocess, sesuaikan dengan asumsi dan tujuan utama proyek. 
7. Selanjutnya, lakukan saja seperti biasa. 
8. Tidak perlu melakukan analisis komplet, sesuaikan saja dengan tujuan proyek. 
9. *Are hyperparameter tuning and feature engineering that useless?*
