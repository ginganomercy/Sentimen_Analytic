# Laporan Akhir Machine Learning :  Mobile Recommendation System - Rafly Ashraffi Rachmat

## Proyek Overview

![animasi mobile phone](https://github.com/user-attachments/assets/ed108435-3876-4d73-8c98-1ee6f484df08)

Di era digital saat ini, konsumen memiliki begitu banyak pilihan dalam membeli smartphone, yang hadir dengan variasi spesifikasi teknis seperti kapasitas RAM, ukuran kamera, daya baterai, sistem operasi, dan kisaran harga yang sangat luas. Banyaknya pilihan ini seringkali membuat pengguna kesulitan dalam menentukan produk yang paling sesuai dengan kebutuhan dan preferensinya.

Proyek ini bertujuan untuk membangun sistem rekomendasi smartphone berbasis data yang dapat membantu pengguna dalam memilih smartphone terbaik berdasarkan spesifikasi dan ulasan pengguna. Dataset yang digunakan memuat informasi penting seperti nama produk, rating pengguna, harga, tautan gambar produk, serta deskripsi teknis (corpus) yang mencakup RAM, penyimpanan internal, baterai, kamera, dan sistem operasi.

## 💼 **Business Understanding**

### 🔍 **Problem Statements**

1. Bagaimana persebaran penggunaan smartphone berdasarkan nama smartphone dan rentang harga yang paling diminati pengguna?
2. Bagaimana performa nama dan model smartphone berdasarkan fitur teknis seperti storage/ram, OS/prosesor, kamera, display, jaringan, dan baterai dibandingkan dengan rating pengguna?
3. bagaimana spesifikasi teknis smartphone (corpus) mempengaruhi dalam menentukan rating smartphone di berbagai segmen harga?
4. Bagaimana cara membuat sistem rekomendasi smartphone yang optimal dan dapat diimplementasikan secara efektif?

### 🌟 **Goals**

1. Mengetahui persebaran dan popularitas smartphone berdasarkan merek dan segmen harga yang paling diminati pengguna.
2. Menganalisis performa smartphone dengan memvisualisasikan hubungan antara fitur teknis dan rating pengguna.
3. Mengevaluasi pengaruh spesifikasi teknis smartphone terhadap rating di berbagai kategori harga menggunakan visualisasi seperti heatmap dan scatterplot.
4. Mengembangkan sistem rekomendasi smartphone menggunakan pendekatan content-based filtering (cosine similarity), serta mengevaluasi performanya dengan metrik precision.

### 🛠️ **Solution Approach**

Untuk mencapai tujuan di atas, pendekatan berikut akan digunakan dalam analisis dan pengembangan sistem rekomendasi smartphone:

1. Mengimplementasikan Exploratory Data Analysis (EDA) untuk analisis dan visualisasi data.
2. Mengimplementasikan content-based filtering approach menggunakan algoritma cosine similarity.
3. Evaluasi Performa Model menggunakan metrik seperti Precision untuk mengukur efektivitas sistem rekomendasi dalam menyarankan smartphone yang relevan.

## Data Understanding

Dataset yang digunakan untuk membuat sistem rekomendasi smartphone pada responden diambil dari platform kaggle. Dataset dapat diakses pada link [berikut](https://www.kaggle.com/datasets/gyanprakashkushwaha/mobile-recommendation-system-dataset).

### Keterangan Variabel

Dataset ini memiliki 6 variabel dengan keterangan sebagai berikut.

| **Nama Variabel** | **Tipe Data**  | **Deskripsi**                                                                             |
| ----------------- | -------------- | ----------------------------------------------------------------------------------------- |
| `name`            | String         | Nama lengkap smartphone beserta varian warna dan kapasitas penyimpanan.                   |
| `ratings`         | Float          | Nilai rating pengguna terhadap smartphone, biasanya dalam skala 1 hingga 5.               |
| `price`           | Integer/String | Harga smartphone. Perlu dibersihkan jika menggunakan simbol mata uang (misalnya `₹`).     |
| `imgURL`          | String (URL)   | Tautan gambar produk dari situs e-commerce.                                               |
| `corpus`          | String         | Deskripsi spesifikasi teknis (storage, RAM, OS, prosesor, kamera, dll) dalam bentuk teks. |
| `user_id`         | String         | ID unik pengguna atau penanda entri smartphone di dataset.                                |

![menampilkan jumlah dataset](https://github.com/user-attachments/assets/69cb56a4-585e-4ebb-9a51-42b15e4325d9)

Dapat dilihat bahwa data yang digunakan adalah sebanyak 2546 data dengan 6 fitur.

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

... (lanjutan konten tidak berubah) ...
