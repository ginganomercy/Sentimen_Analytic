# Laporan Akhir Machine Learning : Mobile Recommendation System - Rafly Ashraffi Rachmat

## Proyek Overview

Di era digital saat ini, konsumen memiliki begitu banyak pilihan dalam membeli smartphone, yang hadir dengan variasi spesifikasi teknis seperti kapasitas RAM, ukuran kamera, daya baterai, sistem operasi, dan kisaran harga yang sangat luas. Banyaknya pilihan ini seringkali membuat pengguna kesulitan dalam menentukan produk yang paling sesuai dengan kebutuhan dan preferensinya.

Proyek ini bertujuan untuk membangun sistem rekomendasi smartphone berbasis data yang dapat membantu pengguna dalam memilih smartphone terbaik berdasarkan spesifikasi dan ulasan pengguna. Dataset yang digunakan memuat informasi penting seperti nama produk, rating pengguna, harga, tautan gambar produk, serta deskripsi teknis (corpus) yang mencakup RAM, penyimpanan internal, baterai, kamera, dan sistem operasi.

## 💼 Business Understanding

### 🔍 Problem Statements

1. Bagaimana persebaran penggunaan smartphone berdasarkan nama smartphone dan rentang harga yang paling diminati pengguna?
2. Bagaimana performa nama dan model smartphone berdasarkan fitur teknis seperti storage/ram, OS/prosesor, kamera, display, jaringan, dan baterai dibandingkan dengan rating pengguna?
3. Bagaimana spesifikasi teknis smartphone (corpus) mempengaruhi dalam menentukan rating smartphone di berbagai segmen harga?
4. Bagaimana cara membuat sistem rekomendasi smartphone yang optimal dan dapat diimplementasikan secara efektif?

### 🌟 Goals

1. Mengetahui persebaran dan popularitas smartphone berdasarkan merek dan segmen harga yang paling diminati pengguna.
2. Menganalisis performa smartphone dengan memvisualisasikan hubungan antara fitur teknis dan rating pengguna.
3. Mengevaluasi pengaruh spesifikasi teknis smartphone terhadap rating di berbagai kategori harga menggunakan visualisasi seperti heatmap dan scatterplot.
4. Mengembangkan sistem rekomendasi smartphone menggunakan pendekatan content-based filtering (cosine similarity), serta mengevaluasi performanya dengan metrik precision.

### 🛠️ Solution Approach

1. Mengimplementasikan Exploratory Data Analysis (EDA) untuk analisis dan visualisasi data.
2. Menggunakan pendekatan content-based filtering dengan algoritma cosine similarity untuk merekomendasikan smartphone.
3. Mengevaluasi performa sistem menggunakan precision, berdasarkan kecocokan hasil dengan kata kunci yang dicari pengguna.

## 📊 Data Understanding

Dataset: [Mobile Recommendation System Dataset](https://www.kaggle.com/datasets/gyanprakashkushwaha/mobile-recommendation-system-dataset)

### Variabel

| Variabel  | Tipe Data      | Deskripsi                                                          |
| --------- | -------------- | ------------------------------------------------------------------ |
| `name`    | String         | Nama lengkap smartphone (termasuk warna dan kapasitas penyimpanan) |
| `ratings` | Float          | Rating pengguna, skala 1–5                                         |
| `price`   | Integer/String | Harga, awalnya berupa string dengan simbol mata uang               |
| `imgURL`  | String (URL)   | Tautan gambar produk                                               |
| `corpus`  | String         | Deskripsi spesifikasi teknis smartphone dalam bentuk teks          |

Jumlah data: 2.546 baris, 5 kolom
![menampilkan jumlah dataset](https://raw.githubusercontent.com/ginganomercy/Sentimen_Analytic/d1302a318fc64e0db882ef9ceafd22b95186e20d/Gambar/checkdata1.png)

### Statistik Data

Selanjutnya akan ditampilkan statistik data numerikal secara umum:

| Statistik                | Nilai |
| ------------------------ | ----- |
| Jumlah data (count)      | 2.546 |
| Rata-rata (mean)         | 4.27  |
| Standar deviasi (std)    | 0.21  |
| Nilai minimum (min)      | 2.90  |
| Kuartil 1 (25%)          | 4.10  |
| Median / Kuartil 2 (50%) | 4.30  |
| Kuartil 3 (75%)          | 4.40  |
| Nilai maksimum (max)     | 5.00  |

Tabel di atas memberikan informasi statistik pada masing-masing kolom, antara lain:
- Count adalah jumlah sampel pada data.
- Mean adalah nilai rata-rata.
- Std adalah standar deviasi (mengukur seberapa tersebar data).
- Min yaitu nilai minimum setiap kolom.
- 25% adalah kuartil pertama, yaitu nilai di bawah 25% data berada.
- 50% adalah kuartil kedua, juga disebut median (nilai tengah data).
- 75% adalah kuartil ketiga, yaitu nilai di bawah 75% data berada.
- Max adalah nilai maksimum

Penjelasan:
Dari tabel Data ratings menunjukkan distribusi yang cukup sempit dan condong ke arah nilai tinggi, yang mengindikasikan bahwa mayoritas pengguna memberikan penilaian positif terhadap item yang ada. Hal ini bisa menunjukkan kualitas produk/jasa yang baik atau bisa juga bias penilaian (rating bias).

### Anomali dan Missing Values

* Ditemukan data duplikat berdasarkan `name` (jumlah sebelum dihapus: 2546, setelah dihapus: 2545)
* Terdapat missing value pada kolom `corpus`, serta hasil ekstraksi seperti `storage_ram`, `os_processor`, `camera`, `display`, `network`, dan `battery`
  ![mengecek missing value](https://raw.githubusercontent.com/ginganomercy/Sentimen_Analytic/d1302a318fc64e0db882ef9ceafd22b95186e20d/Gambar/checkdata3.png)

---
## Exploratory Data Analysis (EDA)
### Persebaran penggunaan smartphone berdasarkan nama smarphone dan rentang harga
![EDA](https://raw.githubusercontent.com/ginganomercy/Sentimen_Analytic/66e6eedf7691f9abc1294fcdea4d7bd731a28471/Gambar/top10kombinasibrand.png)

Kesimpulan:
- Brand dan harga adalah dua faktor utama dalam keputusan pembelian smartphone.
- Samsung dan OPPO tampil sebagai brand paling banyak dipilih di berbagai rentang harga.
- Rentang harga menengah (sekitar 10K–30K) adalah segmen pasar paling kompetitif dan diminati.
- Untuk sistem rekomendasi atau strategi pemasaran, fokuskan pada model populer di rentang harga tersebut, dengan storage 64–128 GB, dari brand-brand teratas seperti Samsung, OPPO, dan OnePlus.
- 
### Hubungan antara Rating vs RAM dan Storage
![EDA2](https://raw.githubusercontent.com/ginganomercy/Sentimen_Analytic/f37dae5717c6007611cf4ac27ebfa1394c3de491/Gambar/ratingvsram.png)

Penjelasan:
1. RAM 4–8 GB paling umum dan cenderung mendapat rating ≥ 4.0, mencerminkan performa ideal.
2. Storage ≥ 128 GB sering muncul pada smartphone dengan rating tinggi.
3. Ukuran baterai (dalam plot) tidak terlalu memengaruhi rating secara langsung.
4. RAM sangat besar (≥ 12 GB) tidak selalu berarti rating tinggi, kemungkinan karena faktor lain seperti software atau harga.

### Scatterplot Kamera VS Rating
![EDA3](https://raw.githubusercontent.com/ginganomercy/Sentimen_Analytic/f37dae5717c6007611cf4ac27ebfa1394c3de491/Gambar/kameravsrating.png)

Penjelasan:
1. Mayoritas kamera utama berada di kisaran 12–64 MP, sesuai tren pasar menengah ke atas.
2. Kamera ≥ 48 MP cenderung berkorelasi dengan rating ≥ 4.0, menandakan bahwa resolusi kamera tinggi diapresiasi oleh pengguna.
3. Namun, tidak ada korelasi linear — beberapa smartphone dengan kamera tinggi tetap mendapat rating sedang.

Hal ini menunjukkan bahwa megapiksel bukan satu-satunya faktor, kualitas software kamera dan fitur lain seperti OIS, AI, atau mode malam juga berperan penting dalam pengalaman pengguna.

### Boxplot Rating Berdasarkan Generasi Jaringan
![EDA4](https://raw.githubusercontent.com/ginganomercy/Sentimen_Analytic/f37dae5717c6007611cf4ac27ebfa1394c3de491/Gambar/distribusirating.png)

Penjelasan:
1. Smartphone 5G cenderung memiliki rating lebih tinggi secara konsisten dibanding 3G dan 4G.
2. Median rating untuk 5G terlihat lebih tinggi, dengan distribusi yang lebih stabil dan jarang outlier.
3. Sebaliknya, 3G dan 4G menunjukkan variasi rating yang lebih besar, dengan beberapa perangkat 4G mendapat rating rendah.

Hal ini menunjukkan bahwa dukungan jaringan terbaru (5G) menjadi nilai tambah dalam penilaian pengguna — meskipun bisa jadi karena ponsel 5G juga dibekali spesifikasi lebih tinggi.

### Kolerasi Fitur Teknis dengan Rating Pengguna
![EDA5](https://raw.githubusercontent.com/ginganomercy/Sentimen_Analytic/f37dae5717c6007611cf4ac27ebfa1394c3de491/Gambar/korelasifiturteknis.png)

Penjelasan:
1. Rating pengguna memiliki korelasi lemah dengan hampir semua fitur teknis (nilai korelasi mendekati 0).
2. RAM, storage, kamera, dan baterai hanya menunjukkan korelasi sangat rendah terhadap rating (di bawah 0.2), artinya peningkatan spesifikasi teknis tidak selalu berbanding lurus dengan kepuasan pengguna.
3. Network generation (3G/4G/5G) juga tidak menunjukkan hubungan kuat terhadap rating, meskipun ada tren 5G cenderung disukai.

Korelasi paling tinggi pun tetap berada dalam kategori lemah, sehingga faktor lain seperti harga, brand, desain, dan pengalaman pengguna kemungkinan besar lebih menentukan dalam penilaian.

### Heatmap Korelasi Fitur Teknis vs Rating per Segmen Harga

![EDA6](https://raw.githubusercontent.com/ginganomercy/Sentimen_Analytic/f37dae5717c6007611cf4ac27ebfa1394c3de491/Gambar/korelasiratingpersegmen.png)

Kesimpulan:
1. Segmen Harga Low
 - Korelasi lemah secara umum antara fitur teknis dan rating.
 - Fitur seperti RAM, storage, dan kamera memiliki korelasi positif kecil hingga sedang terhadap rating.
 - Display dan baterai menunjukkan pengaruh minim, mengindikasikan bahwa di segmen ini pengguna cenderung puas dengan fitur dasar asalkan harganya terjangkau.
2. Segmen Harga Mid
 - RAM dan kamera mulai menunjukkan korelasi positif yang lebih kuat terhadap rating.
 - Storage dan baterai juga mulai memberi kontribusi terhadap kepuasan pengguna.
 - Ini menunjukkan bahwa di segmen menengah, pengguna mulai mempertimbangkan kombinasi performa dan daya tahan.
3. Segmen Harga High
Korelasi terkuat ditemukan di segmen ini, terutama pada:
 - RAM dan rating: menandakan performa multitasking sangat penting.
 - Storage dan kamera: fitur premium ini memengaruhi persepsi kualitas pengguna.

Fitur-fitur teknis secara umum memiliki korelasi yang lebih jelas terhadap rating, mencerminkan ekspektasi pengguna yang tinggi di segmen ini.

---

## 🪑 Data Preparation

### 1. Penghapusan Duplikasi

* Menggunakan fungsi `drop_duplicates()` untuk menghapus duplikasi berdasarkan `name`.
* Total baris setelah penghapusan: 2545
  ![data duplikasi](https://raw.githubusercontent.com/ginganomercy/Sentimen_Analytic/d1302a318fc64e0db882ef9ceafd22b95186e20d/Gambar/checkdata2.png)
  

### 2. Penanganan Missing Value

* Kolom `corpus` dipecah menjadi enam fitur teknis: `storage_ram`, `os_processor`, `camera`, `display`, `network`, dan `battery`
* Missing value pada kolom hasil ekstraksi diisi dengan "unknown"
* Baris dengan `corpus` kosong dihapus dari dataset
* Validasi ulang memastikan semua kolom tidak memiliki missing value
  ![menangani missing value](https://raw.githubusercontent.com/ginganomercy/Sentimen_Analytic/d1302a318fc64e0db882ef9ceafd22b95186e20d/Gambar/checkdata4.png)

### 3. Pembersihan Harga

* Kolom `price` dibersihkan dari simbol mata uang (`₹`) dan tanda koma
* Diketik ulang ke format numerik `float64`
* Contoh hasil pembersihan: 23999.0, 12999.0, dll.
  ![menghapus price](https://raw.githubusercontent.com/ginganomercy/Sentimen_Analytic/c18d10023ee2516aa944a9e8ab76eb3b6d2d2539/Gambar/checkdata7.png)

### 4. TF-IDF Vectorization

* Menggabungkan kolom `name`, `price`, `ratings`, dan `corpus` menjadi satu teks representasi per produk
* Menggunakan `TfidfVectorizer` untuk mengubah representasi teks menjadi vektor numerik
* Hasil vektorisasi digunakan dalam perhitungan cosine similarity antar produk

---

## 🤖 Modeling & Result

### Metode: Content-Based Filtering

* Menggunakan cosine similarity antar vektor TF-IDF untuk mengukur kemiripan antar produk
* Fungsi `smart_content_based_recommendation()` digunakan untuk mengembalikan Top-10 produk yang paling mirip berdasarkan input keyword produk

Content-based filtering menggunakan cosine similarity sebagai algoritma untuk membuat sistem rekomendasi berdasarkan content-based filtering approach. Cosine similarity mengukur kesamaan antara dua vektor dan menentukan apakah kedua vektor tersebut menunjuk ke arah yang sama. Ia menghitung sudut cosinus antara dua vektor. Semakin kecil sudut cosinus, semakin besar nilai cosine similarity. Cosine similarity dirumuskan sebagai berikut.

$$Cos (\theta) = \frac{\sum_1^n a_ib_i}{\sqrt{\sum_1^n a_i^2}\sqrt{\sum_1^n b_i^2}}$$

Pada python, kita akan menggunakan  `cosine_similarity` untuk mendapatkan nilai cosinus dua vektor dalam matriks. Cosine similarity memiliki kelebihan seperti output yang ternormalisasi (rentang -1 hingga 1) sehingga memudahkan interpretasi, penggunaan yang mudah dan sederhana, serta efisien untuk data sparse berdimensi tinggi, seperti TF-IDF. Meski demikian, cosine similarity memiliki beberapa kelemahan, seperti menganggap seluruh faktor/parameter sama penting, sensitif terhadap perubahan 'sudut vektor', dan tidak selalu cocok untuk data negatif. Setelah dibentuk sistem rekomendasi, selanjutnya akan diuji sistem rekomendasi ini untuk menampilkan top 10 rekomendasi berdasarkan name, price, rating dan corpus oleh user. Diperoleh hasil berikut.

### Contoh Hasil Rekomendasi

smart_content_based_recommendation("SAMSUNG Galaxy")

| Index | Name                                | Price   | Ratings |
| ----- | ----------------------------------- | ------- | ------- |
| 0     | SAMSUNG Galaxy A04 (Black, 128 GB)  | 11990.0 | 4.0     |
| 1     | SAMSUNG Galaxy A04 (Copper, 128 GB) | 12799.0 | 4.0     |
| 2     | SAMSUNG A04 e (Copper, 64 GB)       | 9999.0  | 4.1     |
| 3     | SAMSUNG Galaxy A04 (Copper, 64 GB)  | 11199.0 | 4.4     |
| 4     | SAMSUNG Galaxy A12 (Black, 64 GB)   | 12999.0 | 4.3     |
| 5     | SAMSUNG Galaxy M11 (Black, 32 GB)   | 12999.0 | 4.3     |
| 6     | SAMSUNG Galaxy M11 (Violet, 64 GB)  | 12999.0 | 4.4     |
| 7     | SAMSUNG Galaxy M11 (Violet, 64 GB)  | 12999.0 | 4.4     |
| 8     | SAMSUNG Galaxy M11 (Violet, 64 GB)  | 12999.0 | 4.4     |
| 9     | SAMSUNG Galaxy M11 (Violet, 64 GB)  | 12999.0 | 4.4     |

---

## ✅ Evaluation

### Metode Evaluasi

Evaluasi dilakukan menggunakan metrik **Precision**, yaitu proporsi rekomendasi yang relevan dibandingkan dengan jumlah total rekomendasi yang diberikan.

**Formula Precision**:

$$
\text{Precision} = \frac{\text{True Positive}}{\text{Total Rekomendasi}}
$$

### Hasil Evaluasi

| Total Rekomendasi | True Positive | Precision |
| ----------------- | ------------- | --------- |
| 10                | 10            | 1.00      |

### Interpretasi

* Semua produk yang direkomendasikan relevan dengan input "SAMSUNG Galaxy A04 (Green, 128 GB)".
* Rekomendasi mencakup varian warna atau kapasitas lain dari model yang sama dan model sejenis.
* **Precision 1.00 (100%)** menandakan performa sangat baik dari sistem rekomendasi berbasis content-based filtering untuk produk ini.

### Kelebihan

* Relevansi sangat tinggi pada pencarian berbasis nama produk dan merek.
* Cocok untuk eksplorasi varian smartphone yang mirip.

### Keterbatasan

* Belum mencakup metrik lain seperti **recall** atau **F1-score**.
* Validasi masih berdasarkan satu contoh input.

### Kesimpulan

Sistem rekomendasi memberikan hasil yang sangat relevan dengan **precision sebesar 1.00** pada kasus "SAMSUNG Galaxy A04 (Green, 128 GB)", menunjukkan akurasi tinggi dalam pencarian berbasis konten.

---

## 📂 Referensi

1. Gyan Prakash Kushwaha (2022). [Mobile Recommendation System Dataset](https://www.kaggle.com/datasets/gyanprakashkushwaha/mobile-recommendation-system-dataset)
2. Aurélien Géron. *Hands-On Machine Learning with Scikit-Learn, Keras, and TensorFlow*. O'Reilly.
3. [Scikit-learn Cosine Similarity](https://scikit-learn.org/stable/modules/metrics.html#cosine-similarity)
4. [Wikipedia: TF-IDF](https://en.wikipedia.org/wiki/Tf%E2%80%93idf) | [Wikipedia: Cosine Similarity](https://en.wikipedia.org/wiki/Cosine_similarity)
5. GitHub: [Gambar visualisasi dan source](https://github.com/ginganomercy/Sentimen_Analytic)
