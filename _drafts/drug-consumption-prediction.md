---
layout: post
title: Drug Consumption Prediction
categories:
- DS Projects
tags:
- classification
- gradient boosting
- random forest
- drug consumption
- threshold optimization
description: 'An undergraduate thesis: imbalanced data classification on drug consumption
  using threshold optimization combined with RF and GB.'
media_subpath: "/assets/img/drug-consumption"
---
Ah, since the original file is in Indonesian, should I do it in English, instead? Oh, such a weird logic, but let’s do it. It won’t be that long, right? Truth be told, it had a different structure than the one I usually worked on. It was somehow more *mbulet* — not in a simple straightforward structure (?). Also, it lacked some theoretical framework and reason on some of its steps -- and yet, it still passed. My bad. I'll probably revise one or two things to align with my storytelling -- as well as make things a bit simpler. 

Ah, ternyata lebih mudah jika menggunakan bahasa Indonesia. Tidak perlu menyiapkan mental model yang begitu besar. Maka, dengan senang hati, akan saya lanjutkan saja dengan bahasa Indonesia. Biarlah biar seperti ini saja. 

Sebelum lanjut, coba bayangkan skenario berikut. 

Pada pagi hari yang kelam, pada suatu rumah sakit, terdapat 100 orang antre untuk pemeriksaan penyakit. Kesemuanya memiliki gejala yang serupa: batuk, pilek, demam, juga ruam kemerahan pada sela-sela jari kaki. Diagnosis ditujukan untuk memeriksa virus varian baru, yang katanya, membawa efek yang amat sangat berbahaya. Sehingga, prediksi yang akurat akan sangat membantu.

Lewat uji lab historis, diketahui bahwa probabilitas seseorang yang memiliki gejala-gejala di atas terinfeksi virus ini adalah 2 persen. Masalahnya, demi kebutuhan cerita ini, uji lab dikatakan membutuhkan waktu 30 menit, itu pun tidak dapat dilakukan secara bersamaan, sehingga kurang efektif untuk pasien sebanyak itu. 

Lantas, saya, seorang statistisi andal, datang dengan pongahnya, membawa metode baru untuk keperluan diagnosis. Hanya butuh waktu kurang dari 5 menit, untuk melakukan diagnosis kepada seluruh pasien, dengan akurasi di atas 90 persen, bahkan mendekati 99 persen. Tidakkah saya terlihat heroik dan sungguhlah keren? 

Pada semua orang, saya katakan, “Itu gejala penyakit lain, anda tidak terinfeksi virus varian baru ini.” 

## Problem & Dataset
Dengan asumsi bahwa 2 dari 100 orang pada cerita di atas benar-benar terinfeksi virus varian baru, maka diagnosis yang saya lakukan hanya memiliki galat atau kesalahan prediksi sebesar 2 persen, atau dengan kata lain, memiliki akurasi sebesar 98 persen. Hebat, bukan?

Tentu saja tidak. Apa kabar 2 orang yang salah prediksi tersebut? Apakah dibiarkan saja untuk wafat lebih cepat? 

Cerita pengantar di atas merupakan satu permasalahan klasik dalam persoalan klasifikasi, yaitu data tidak seimbang (imbalanced data). Adanya ketidakseimbangan kelas pada distribusi data asal, yang ditunjukkan dengan perbedaan proporsi yang terpaut jauh, dapat membuat model cenderung bias ke kelas mayoritas. Hasilnya? Bahkan, dalam kasus ini, model dengan akurasi begitu tinggi (98 persen) bisa memberikan keputusan yang amat berbahaya.

Ah, kecuali jika kita hanya melihat nyawa sebagai statistik belaka. Itu lain lagi. 

Maka, pada tugas akhir tersebut, saya coba selesaikan permasalahan data tidak seimbang pada persoalan klasifikasi. Saya kombinasikan beberapa metode yang sudah ada untuk diterapkan pada data Drug Consumption (Quantified) dari UCI Machine Learning Repository. 

Data tersebut memuat hasil tes kepribadian serta frekuensi konsumsi 18 jenis NAPZA, baik legal maupun ilegal, pada 1885 responden. Terdapat 7 variabel prediktor hasil tes psikologi, yang mencakup NEO-FFI-R, BIS-11, dan ImpSS, serta 5 variabel prediktor kondisi sosiodemografi responden berupa level edukasi, usia, jenis kelamin, negara, dan etnis. 

Pada proyek ini, saya hanya berfokus pada satu variabel respon berupa konsumsi heroin, dengan **memodifikasi** 5 kelas frekuensi asal menjadi 2 kelas baru untuk memudahkan pengerjaan. Kelas pertama berlabel 0 menunjukkan bukan pengguna heroin, sedangkan kelas kedua berlabel 1 menunjukkan pengguna heroin. Kelas pertama terdiri atas responden dengan konsumsi heroin terakhir lebih dari satu dekade yang lalu atau tidak pernah sama sekali. 

## EDA (Exploratory Data Analysis)
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

## Modeling
### Evaluation Metrics
Sebelum masuk ke pembentukan model, marilah kita bahas metrik evaluasi yang akan digunakan. Masih ingat dengan cerita di atas, bagaimana metrik akurasi memberikan nilai yang tinggi meskipun model yang dipakai tidaklah berguna?

Enam buah. Sebanyak itulah metrik evaluasi yang akan dipakai di sini. Tiga buah (recall/sensitivity, F-measure, dan G-mean) merupakan metrik evaluasi utama, dan tiga lainnya (accuracy, specificity, dan precision) digunakan sebagai pembanding.

Perlukah saya jelaskan masing-masingnya di sini? Toh, tidak mungkin dibaca secara mendetail kan? Berhubung saya *mager*, silakan cari referensi yang membahas metrik-metrik tersebut secara detail. 

Ringkasnya, recall merupakan kemampuan model dalam menyaring seluruh kelas positif; F-measure merupakaan rataan harmonik dari metrik evaluasi precision dan recall yang mana fokus utamanya pada kelas positif; dan G-mean merupakaan rataan geometrik dari metrik evaluasi recall dan specificity yang mana mengombinasikan performa kedua kelas. 

Pada konteks riil dengan data pengguna heroin, optimasi recall dapat digunakan dengan menjaring sebanyak mungkin pengguna heroin, meskipun kasus salah tangkap jauh lebih banyak. Anggap saja sebuah harga untuk tindakan preventif. 

Di lain sisi, optimasi F-measure dan G-mean menangkap sebanyak mungkin pengguna heroin dengan tetap memerhatikan kasus salah tangkap agar tidak terlalu banyak.

Rumit? Memang. Itu saja bukan sebuah solusi umum, hanya satu dari banyak kemungkinan kasus.

### Algorithms and Methods
Akan dibentuk 2 model sebagai tolok ukur (baseline), yaitu Logistic Regression dan SVM, serta 2 model utama: Random Forest dan Gradient Boosting. Model-model tersebut akan dikombinasikan dengan 3 metode optimasi ambang batas: Pmin, MID, dan 3 metode empiris. Termasuk model tanpa menggunakan metode optimasi ambang batas, terdapat total 24 (4 x 6) kombinasi model. 

Empat algoritma yang saya gunakan harusnya sudah familiar. Namun, bagaimana dengan metode optimasi ambang batas? Metode ini bekerja dengan menggeser ambang batas standar (0.5) pada nilai **prediksi probabilitas** untuk melakukan prediksi ke dalam kelas tertentu.

Sebagai contoh, sebuah model memberikan nilai probabilitas bahwa seseorang tersebut merupakan pengguna heroin sebesar 0.3. Pada model dengan ambang batas standar, 0.5, berhubung 0.3 kurang dari 0.5, maka orang tersebut akan dikelompokkan sebagai **bukan** pengguna heroin. Di lain sisi, dengan menggeser ambang batas ke 0.2, nilai probabilitas menjadi lebih dari ambang batas, sehingga orang tersebut akan dikelompokkan sebagai pengguna heroin. 

Pmin merupakan nilai probabilitas apriori pada kelas minoritas (proporsi kelas positif, pengguna heroin). MID merupakan nilai tengah dari Pmin dan ambang batas standar (0.5). Sedangkan metode empiris menentukan ambang batas optimal untuk **suatu metrik tertentu** secara empiris menggunakan data validasi. Dalam kasus ini, akan digunakan metode empiris berupa optR, optF,
dan optG yang ditujukan untuk mengoptimalkan 3 metrik evaluasi berbeda, yaitu recall, F-measure, dan G-mean.

Berhubung data yang ada sudah terkuantifikasi, tahapan preprocessing tidak perlu untuk dilakukan. Selanjutnya, model akan dibentuk dan dievaluasi berdasarkan 6 metrik evaluasi menggunakan stratified 10-fold cross-validation (hasil rataan metrik dari 10 kali pemodelan validasi silang).

### Modeling Result
Ada empat algoritma dikombinasikan dengan 6 ambang batas yang berbeda. Mari kita lihat model dasar saja, Logistic Regression. 

![log](/logistic-eval.png)

Gambar di atas menunjukkan tabel hasil metrik evaluasi dengan stratified 10-fold cross-validation untuk model Logistic Regression. Berikut poin-poin penting yang perlu digarisbawahi. 

- Accuracy model tinggi (88.7%)
- Hanya saja, model cenderung berfokus pada kelas mayoritas, dan mengabaikan kelas minoritas (kelas positif, pengguna heroin)
- Hal itu ditunjukkan dengan specificity yang sangat tinggi (99.0%) serta recall yang sangat kecil (7.6%)
- Artinya, model hanya dapat menyaring sebanyak 7.6% pengguna heroin, meski kesalahan prediksi tersebut (hanya) sebesar 39.0% (1 - precision)
- Nilai F-measure dan G-mean juga cenderung rendah, menunjukkan bahwa model cenderung bias pada kelas mayoritas

Nah, metode optimasi ambang batas secara konsisten menyeimbangkan dominasi kelas mayoritas. Seluruh metode optimasi menurunkan nilai accuracy, precision, dan specificity yang dibarengi dengan naiknya nilai recall, F-measure, dan G-mean. Hanya derajat kekuatannya saja yang bervariasi.

Dengan mengambil nilai recall sebagai acuan, metode MID memiliki efek paling moderat, diikuti dengan metode optF, optG, Pmin, dan optR.

Sebagai gambaran, kita ambil metode optR. Dengan rerata ambang batas sebesar 0.036, didapatkan nilai akurasi yang sangat rendah 45.5%. Sebagai gantinya, model dapat menjaring sebanyak 94.8% pengguna heroin. Meski kabar buruknya? Lebih dari 80 persennya (1 - precision) salah diprediksi sebagai pengguna heroin. 

Bandingkan saja dengan ambang batas standar, yang hanya menyaring 7.6% pengguna heroin, dengan kesalahan prediksi pengguna heroin hanya sekitar 40%.

Mana yang lebih baik? Saya kira tidak dua-duanya. Hehe. 

Maka dari itu, konteks riil sangat dibutuhkan untuk menentukan kesalahan prediksi manakah yang lebih ditolerir? Kita bisa gunakan batas minimal suatu metrik (misalnya nilai recall harus lebih dari 20 persen, nilai precision harus lebih dari 50 persen, dan sebagainya), atau dengan membuat matriks biaya khusus untuk kesalahan prediksi. 

Begitulah. 

Ah iya, model lain menghasilkan nilai evaluasi yang serupa. Saya kira karena data yang digunakan cenderung berdistribusi mendekati normal (atau setidaknya simetris), tidak banyak nilai outlier, serta memiliki nilai yang seragam. Hasilnya? Model dasar seperti Logistic Regression memberikan hasil serupa dibandingkan dengan model yang lebih kompleks: SVM, Random Forest dan Gradient Boosting. 

Ketiga model itu tidak akan dibahas secara mendetail. Asumsikan saja hasilnya serupa.

## Model Comparison
Jika hasilnya serupa, lantas, untuk apa kita lakukan perbandingan model? Terlebih lagi, merepotkan diri menggunakan Uji Nemenyi, yang mana, cenderung tidak berguna?

Pada proyek aslinya, dilakukan tiga kali Uji Nemenyi, masing-masing untuk membandingkan metode optimasi mana sajakah yang memiliki performa terbaik untuk setiap metrik evaluasi recall, F-measure, dan G-mean. Hal ini tentu saja digunakan untuk **validasi** bahwa metode yang kita lakukan ada manfaatnya. Berguna. Bukan hanya bualan belaka. 

Baiklah, mari mulai dari metrik evaluasi recall.

### Recall Optimization
![barplot-recall](/barplot-recall.png)

Lihat saja gambar di atas. Seluruh model cenderung memiliki performa yang serupa: metode empiris optR memberikan nilai recall tertinggi, diikuti dengan Pmin, MID, dan barulah ambang batas standar. 

Sekilas saja. Jika memang hendak optimasi metrik evaluasi recall, secara maksimal kita bisa gunakan langsung metode empiris maupun metode Pmin. Di lain sisi, kita juga bisaa gunakan metode optimasi MID untuk mendapat metrik evaluasi yang moderat. Mirip-mirip apa yang dapat disimpulkan di pembahasan sebelumnya, bukan? 

![uji-recall](/uji-recall.png)

Secara formal, Uji Nemenyi dilakukan untuk 16 kombinasi model dan metode. Dari gambar di atas, dapat dilihat bahwa optimasi recall didapat dengan menggunakan metode optR, yang mana secara statistik tidak berbeda denganm metode Pmin sehingga dapat digunakan sebagai alternatif pengganti. 

Di lain sisi, kombinasi model dan metode terbaik (khususnya optR) berbeda secara statistik dibandingkan dengan ambang batas standar untuk keseluruhan model.

### F-measure Optimization
Lantas, bagaimana dengan metrik evaluasi F-measure. Kombinasi model dan metode mana saja yang dapat mengoptimalkan metrik evaluasi ini? 

![fmeasbarplot](/barplot-f.png)

Gambar tersebut menjelaskan sebagian besarnya. Terlihat bahwa ketiga metode optimasi ambang batas cenderung memiliki nilai F-measure yang serupa, meski masih memiliki urutan yang konsisten per modelnya.

Hanya saja, menggunakan Uji Nemenyi yang dapat dilihat pada gambar di bawah, ketiga metode ambang batas tersebut (optF, Pmin, dan MID) tidak memiliki perbedaan yang signifikan secara statistik. Sehingga, ketiga metode dapat dipakai secara bergantian untuk mendapatkan nilai F-measure yang optimal. 

![fmeas](/nemenyi-f.png)

Eits, tetapi tunggu dulu. Berdasar uji tersebut, ambang batas standar seluruh model juga tidak berbeda secara statistik dibandingkan dengan metode MID untuk seluruh model, serta dibandingkan dengan model Random Forest untuk seluruh metode. Paham kan? 

Ah, seperti ada yang janggal dan mengganjal kan? 

Saya rasa soal pemilihan uji yang digunakan. Biarkan saya menawarkan proposal baru: 
1. Bagaimana jika perbandingan hanya fokus pada seluruh metode untuk setiap model? Kita bandingkan saja dengan ambang batas standar. 
2. Lalu dilanjutkan dengan komparasi kombinasi model dengan metode optimasi ambang batas. Yap, kita pisahkan saja dua hal tersebut. 
3. Opsi lain? Tidak perlu dilakukan uji statistik. Selain merepotkan dan overrated, bukannya tidak diperlukan? Harusnya perbedaan sekecil apa pun bisa dianggap beda, kan? Atau entahlah.

## Tech Stack
- Language: Python
- Libraries: pandas, numpy, matplotlib, seaborn, scikit-learn

## Conclusion & Reflection
Ambil saja satu dua hikmahnya, jika memang selalu seperti itu. *Nah, guess I was way too lazy to make a TLDR part. So, a short **that is that** is enough, right?*

Dan ya, katanya jalan masih panjang? Maka sudah seharusnya, terus belajar, memperbaiki diri. Jadi lebih bijaksana? 

Ah, full of bs.
