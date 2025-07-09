# Laporan Akhir Machine Learning :  Mobile Recommendation System - Rafly Ashraffi Rachmat

## Proyek Overview

Di era digital saat ini, konsumen memiliki begitu banyak pilihan dalam membeli smartphone, yang hadir dengan variasi spesifikasi teknis seperti kapasitas RAM, ukuran kamera, daya baterai, sistem operasi, dan kisaran harga yang sangat luas. Banyaknya pilihan ini seringkali membuat pengguna kesulitan dalam menentukan produk yang paling sesuai dengan kebutuhan dan preferensinya.

Proyek ini bertujuan untuk membangun sistem rekomendasi smartphone berbasis data yang dapat membantu pengguna dalam memilih smartphone terbaik berdasarkan spesifikasi dan ulasan pengguna. Dataset yang digunakan memuat informasi penting seperti nama produk, rating pengguna, harga, tautan gambar produk, serta deskripsi teknis (corpus) yang mencakup RAM, penyimpanan internal, baterai, kamera, dan sistem operasi.

## 💼 **Business Understanding**

### 🔍 **Problem Statements**

1. Bagaimana persebaran penggunaan smartphone berdasarkan nama smartphone dan rentang harga yang paling diminati pengguna?
2. Bagaimana performa nama dan model smartphone berdasarkan fitur teknis seperti storage/ram, OS/prosesor, kamera, display, jaringan, dan baterai dibandingkan dengan rating pengguna?
3. Bagaimana spesifikasi teknis smartphone (corpus) mempengaruhi dalam menentukan rating smartphone di berbagai segmen harga?
4. Bagaimana cara membuat sistem rekomendasi smartphone yang optimal dan dapat diimplementasikan secara efektif?

### 🌟 **Goals**

1. Mengetahui persebaran dan popularitas smartphone berdasarkan merek dan segmen harga yang paling diminati pengguna.
2. Menganalisis performa smartphone dengan memvisualisasikan hubungan antara fitur teknis dan rating pengguna.
3. Mengevaluasi pengaruh spesifikasi teknis smartphone terhadap rating di berbagai kategori harga menggunakan visualisasi seperti heatmap dan scatterplot.
4. Mengembangkan sistem rekomendasi smartphone menggunakan pendekatan content-based filtering (cosine similarity), serta mengevaluasi performanya dengan metrik precision.

### 🛠️ **Solution Approach**

Untuk mencapai tujuan di atas, pendekatan berikut akan digunakan dalam analisis dan pengembangan sistem rekomendasi smartphone:

1. Mengimplementasikan Exploratory Data Analysis (EDA) untuk analisis dan visualisasi data.
2. Mengimplementasikan content-based filtering approach menggunakan algoritma cosine similarity untuk merekomendasikan smartphone berdasarkan kesamaan fitur teknis dan preferensi pengguna.
3. Evaluasi performa sistem menggunakan precision sebagai metrik utama, dengan validasi hasil rekomendasi terhadap pencarian berdasarkan substring nama smartphone.

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

![menampilkan jumlah dataset]()

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

#### memeriksa data duplikasi
![data duplikasi](https://github.com/user-attachments/assets/fec138a2-4e38-4c9e-9809-e57f7739e403)

Dari Hasil diatas terlihat bahwa tidak ada data yang terduplikasi.

#### memeriksa missing value
![mengecek missing value](https://github.com/user-attachments/assets/3ad1e5fd-7cde-4160-8249-d28e6944e45b)

Dari hasil diatas diketahui bahwa terdapat missing velue di 7 kolom yaitu corpus, storage_ram, os_processor, camera, display, network, dan battery.saya uraikan corpus untuk menangani jika terjadi data missing value dri tiap kriteria yang ada di corpus.


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


## Data Preparation
#### Menangani missing velue
![menangani missing velue](https://github.com/user-attachments/assets/b6c942ad-fa58-4288-9d91-90217a441ad2)

Dari Hasil diatas terlihat bahwa sudah tidak ada missing velue karena sudah ditangani.

#### Pembersihan Kolom Price
![menghapus price](https://github.com/user-attachments/assets/136362e5-aa23-40f4-adbe-06a665c41f8b)

Dari hasil diatas menunjukan bahwa kolom price dengan simbol rupe dan koma dihapus dan mengonversi menjadi float.

#### Extract Kolom Corpus
![Ekstract kolom corpus](https://github.com/user-attachments/assets/f074c2d9-24dd-4c97-bf3d-82659de67f3b)

agar lebih mudah mengerti dataset maka kolom corpus dipisah menjadi 6 kolom yang terdiri dari storage_ram, os_processor, camera, display, network, dan battery tujuannya agar mudah mengecek apakah terjadi missing value, duplikasi, dan memudahkan visualisasi.

Karena berbeda antara content-based filtering dengan collaborative filtering, maka data preparation dari kedua approach tersebut akan dilakukan secara masing-masing. Teknik Data preparation yang dilakukan terdiri dari:
- TF-IDF Vectorizer 
- Encoding Data User Rating
- Train-test-split Data User Rating

### 1. Content-Based Filtering
Untuk content-based filtering, kita akan fokus pada name,price,ratings,corpus yang sudah disatukan untuk menjadi dasar pembuatan sistem rekomendasi tersebut. Oleh karena itu, dataframe hanya terdiri 4 kolom dari data yang dimiliki:
* `Name`
* `Price`
* `Rating`
* `Corpus`
* `Brand_Product`

Selanjutnya, digunakan TfidfVectorizer() pada kolom kombinasi name, price, dan rating untuk menghasilkan output berupa angka antara 0 - 1. Lalu, dibentuk dataframe yang berisi kolom kombinasi name,price, dan rating yang telah dilakukan vektorisasi dengan TfidfVectorizer() sebagai kolom dan seluruh nama product brand skincare sebagai barisnya. Hal ini dilakukan karena akan digunakan cosine similarity pada content-based filtering, dimana cosine similarity memerlukan bentuk angka agar dapat dihitung. Contoh dari dataframe dapat dilihat pada tabel berikut.

| **brand\_product**                                                              | **10**   | **10000** | **10190** | **10280** | **10300** | **10390** | **10397** | **10449** | **10470** | **10490** | ... | **y91** | **y91i** | **y93** | **y95** | **yellow** | **youth** | **z1pro** | **z1x** | **z2** | **zero** |
| ------------------------------------------------------------------------------- | -------- | --------- | --------- | --------- | --------- | --------- | --------- | --------- | --------- | --------- | --- | ------- | -------- | ------- | ------- | ---------- | --------- | --------- | ------- | ------ | -------- |
| REDMI Note 12 Pro 5G (Onyx Black, 128 GB) \| \$23999.0 \| Rating: 4.2           | 0.000000 | 0.0       | 0.0       | 0.0       | 0.0       | 0.0       | 0.0       | 0.0       | 0.0       | 0.0       | ... | 0.0     | 0.0      | 0.0     | 0.0     | 0.0        | 0.0       | 0.0       | 0.0     | 0.0    | 0.0      |
| OPPO F11 Pro (Aurora Green, 128 GB) \| \$20999.0 \| Rating: 4.5                 | 0.000000 | 0.0       | 0.0       | 0.0       | 0.0       | 0.0       | 0.0       | 0.0       | 0.0       | 0.0       | ... | 0.0     | 0.0      | 0.0     | 0.0     | 0.0        | 0.0       | 0.0       | 0.0     | 0.0    | 0.0      |
| REDMI Note 11 (Starburst White, 64 GB) \| \$13149.0 \| Rating: 4.2              | 0.000000 | 0.0       | 0.0       | 0.0       | 0.0       | 0.0       | 0.0       | 0.0       | 0.0       | 0.0       | ... | 0.0     | 0.0      | 0.0     | 0.0     | 0.0        | 0.0       | 0.0       | 0.0     | 0.0    | 0.0      |
| OnePlus Nord CE 5G (Blue Void, 256 GB) \| \$21999.0 \| Rating: 4.1              | 0.000000 | 0.0       | 0.0       | 0.0       | 0.0       | 0.0       | 0.0       | 0.0       | 0.0       | 0.0       | ... | 0.0     | 0.0      | 0.0     | 0.0     | 0.0        | 0.0       | 0.0       | 0.0     | 0.0    | 0.0      |
| REDMI 10 Power (Sporty Orange, 128 GB) \| \$18996.0 \| Rating: 4.2              | 0.294548 | 0.0       | 0.0       | 0.0       | 0.0       | 0.0       | 0.0       | 0.0       | 0.0       | 0.0       | ... | 0.0     | 0.0      | 0.0     | 0.0     | 0.0        | 0.0       | 0.0       | 0.0     | 0.0    | 0.0      |
| ...                                                                             | ...      | ...       | ...       | ...       | ...       | ...       | ...       | ...       | ...       | ...       | ... | ...     | ...      | ...     | ...     | ...        | ...       | ...       | ...     | ...    | ...      |
| SAMSUNG Galaxy S20 FE 5G (Cloud Navy, 128 GB) \| \$27440.0 \| Rating: 4.2       | 0.000000 | 0.0       | 0.0       | 0.0       | 0.0       | 0.0       | 0.0       | 0.0       | 0.0       | 0.0       | ... | 0.0     | 0.0      | 0.0     | 0.0     | 0.0        | 0.0       | 0.0       | 0.0     | 0.0    | 0.0      |
| REDMI Note 9 (Shadow Black, 64 GB) \| \$11999.0 \| Rating: 4.3                  | 0.000000 | 0.0       | 0.0       | 0.0       | 0.0       | 0.0       | 0.0       | 0.0       | 0.0       | 0.0       | ... | 0.0     | 0.0      | 0.0     | 0.0     | 0.0        | 0.0       | 0.0       | 0.0     | 0.0    | 0.0      |
| OnePlus 9 5G (Astral Black, 128 GB) \| \$30203.0 \| Rating: 3.9                 | 0.000000 | 0.0       | 0.0       | 0.0       | 0.0       | 0.0       | 0.0       | 0.0       | 0.0       | 0.0       | ... | 0.0     | 0.0      | 0.0     | 0.0     | 0.0        | 0.0       | 0.0       | 0.0     | 0.0    | 0.0      |
| SAMSUNG Galaxy S22 Ultra 5G (Phantom Black, 256 GB) \| \$20463.0 \| Rating: 4.3 | 0.000000 | 0.0       | 0.0       | 0.0       | 0.0       | 0.0       | 0.0       | 0.0       | 0.0       | 0.0       | ... | 0.0     | 0.0      | 0.0     | 0.0     | 0.0        | 0.0       | 0.0       | 0.0     | 0.0    | 0.0      |
| vivo T2x 5G (Aurora Gold, 128 GB) \| \$13999.0 \| Rating: 4.4                   | 0.000000 | 0.0       | 0.0       | 0.0       | 0.0       | 0.0       | 0.0       | 0.0       | 0.0       | 0.0       | ... | 0.0     | 0.0      | 0.0     | 0.0     | 0.0        | 0.0       | 0.0       | 0.0     | 0.0    | 0.0      |


🔍 Kesimpulan

Kode ini membentuk DataFrame cosine_sim_df dari matriks cosine similarity, dengan baris dan kolom diberi label brand_product (gabungan nama, harga, dan rating produk). Struktur ini memudahkan analisis kemiripan antar produk secara langsung berdasarkan representasi teks. Hasil sampling dari matriks menunjukkan beberapa nilai kemiripan antar produk, yang bisa digunakan untuk menampilkan rekomendasi produk serupa dalam sistem content-based filtering.

### 2. Collaborative Filtering
Untuk collaborative filtering, kita juga akan fokus pada user_id, rating beserta corpus dari data tersebut. Berbeda dengan content-based, kita hanya akan mengambil 3 kolom dari data yang dimiliki, yaitu
* `user_id`
* `track_name`
* `Rating`

Karena `user_id` dan `track_name` memiliki tipe data string dan unik, maka dilakukan encoding terhadap kedua kolom tersebut, kemudian dibentuk dataframe yang berisi kolom `user_id` yang sudah diencoding, kolom `track_name` yang sudah diencoding, dan `Ratings`. Contoh dari dataframe dapat dilihat pada tabel berikut.

| **track** | **name** | **ratings** |
| --------- | -------- | ----------- |
| 982       | 752      | 4.2         |
| 1003      | 765      | 4.2         |
| 2144      | 1655     | 4.5         |
| 1620      | 1252     | 4.2         |
| 1425      | 1102     | 4.3         |
| ...       | ...      | ...         |
| 1459      | 1130     | 4.2         |
| 1676      | 1294     | 4.1         |
| 1122      | 860      | 4.2         |
| 1889      | 1459     | 4.1         |
| 1455      | 1126     | 4.3         |

Penjelasan:

1. Data telah diacak secara menyeluruh (100%) menggunakan fungsi .sample(frac=1).
2. Hal ini bertujuan untuk menghilangkan bias urutan data, yang penting sebelum digunakan dalam model collaborative filtering.
3. Parameter random_state=42 memastikan bahwa proses pengacakan dapat direproduksi, penting untuk debugging dan eksperimen ilmiah.

**Mengapa diperlukan melakukan Encoding data?**
- Encoding data perlu dilakukan karena pada Collaborative Filtering, model harus belajar dari pola interaksi pengguna terhadap item. Data perlu diubah ke dalam bentuk numerik agar model neural network dapat memprosesnya.


Setelah data yang diperlukan telah diencoding, selanjutnya data dibagi menjadi dua, yaitu data training dan data testing untuk pembuatan dan pelatihan model. Data training digunakan untuk melatih model dengan data yang ada, sedangkan data testing digunakan untuk menguji model yang dibuat menggunakan data yang belum dilatih. Pembagian data ini dilakukan dengan perbandingan 80% : 20% untuk data training dan data testing.

**Mengapa diperlukan melakukan Train-test-split data?**

- Memisahkan data menjadi set pelatihan dan pengujian memungkinkan kita untuk mengevaluasi kinerja model pada data yang tidak pernah dilihat sebelumnya. Ini memberikan gambaran yang lebih akurat tentang seberapa baik model yg kita buat.

## Modelling and Result

### 1. Content-Based Filtering

Content-based filtering menggunakan cosine similarity sebagai algoritma untuk membuat sistem rekomendasi berdasarkan content-based filtering approach. Cosine similarity mengukur kesamaan antara dua vektor dan menentukan apakah kedua vektor tersebut menunjuk ke arah yang sama. Ia menghitung sudut cosinus antara dua vektor. Semakin kecil sudut cosinus, semakin besar nilai cosine similarity. Cosine similarity dirumuskan sebagai berikut.

$$Cos (\theta) = \frac{\sum_1^n a_ib_i}{\sqrt{\sum_1^n a_i^2}\sqrt{\sum_1^n b_i^2}}$$

Pada python, kita akan menggunakan  `cosine_similarity` untuk mendapatkan nilai cosinus dua vektor dalam matriks. Cosine similarity memiliki kelebihan seperti output yang ternormalisasi (rentang -1 hingga 1) sehingga memudahkan interpretasi, penggunaan yang mudah dan sederhana, serta efisien untuk data sparse berdimensi tinggi, seperti TF-IDF. Meski demikian, cosine similarity memiliki beberapa kelemahan, seperti menganggap seluruh faktor/parameter sama penting, sensitif terhadap perubahan 'sudut vektor', dan tidak selalu cocok untuk data negatif. Setelah dibentuk sistem rekomendasi, selanjutnya akan diuji sistem rekomendasi ini untuk menampilkan top 10 rekomendasi berdasarkan name, price, rating dan corpus oleh user. Diperoleh hasil berikut.

`content_based_phone_recommendations('SAMSUNG Galaxy')`

| Index | Name                                            | Price   | Ratings | Brand Product                                                            |
| ----- | ----------------------------------------------- | ------- | ------- | ------------------------------------------------------------------------ |
| 9     | SAMSUNG Galaxy A04 (Green, 128 GB)              | 12999.0 | 4.0     | SAMSUNG Galaxy A04 (Green, 128 GB) \| \$12999.0 \| Rating: 4.0           |
| 13    | SAMSUNG Galaxy Z Flip4 5G (Bora Purple, 128 GB) | 24463.0 | 3.7     | SAMSUNG Galaxy Z Flip4 5G (Bora Purple, 128 GB)                          |
| 55    | SAMSUNG M32 5G (Sky blue, 128 GB)               | 16200.0 | 4.2     | SAMSUNG M32 5G (Sky blue, 128 GB) \| \$16200.0 \| Rating: 4.2            |
| 70    | SAMSUNG Galaxy A13 (Black, 64 GB)               | 18490.0 | 4.1     | SAMSUNG Galaxy A13 (Black, 64 GB) \| \$18490.0 \| Rating: 4.1            |
| 96    | SAMSUNG Galaxy A72 (Awesome Black, 128 GB)      | 23537.0 | 4.3     | SAMSUNG Galaxy A72 (Awesome Black, 128 GB) \| \$23537.0 \| Rating: 4.3   |
| 99    | SAMSUNG Galaxy S21 FE 5G (Graphite, 128 GB)     | 31999.0 | 4.3     | SAMSUNG Galaxy S21 FE 5G (Graphite, 128 GB) \| \$31999.0 \| Rating: 4.3  |
| 128   | SAMSUNG Galaxy M12 (Blue, 128 GB)               | 15499.0 | 4.3     | SAMSUNG Galaxy M12 (Blue, 128 GB) \| \$15499.0 \| Rating: 4.3            |
| 133   | SAMSUNG Galaxy On7 (Gold, 8 GB)                 | 5999.0  | 4.2     | SAMSUNG Galaxy On7 (Gold, 8 GB) \| \$5999.0 \| Rating: 4.2               |
| 138   | SAMSUNG Galaxy F42 5G (Matte Black, 128 GB)     | 20999.0 | 4.3     | SAMSUNG Galaxy F42 5G (Matte Black, 128 GB) \| \$20999.0 \| Rating: 4.3  |
| 145   | SAMSUNG Galaxy A73 5G (Awesome Mint, 256 GB)    | 20537.0 | 4.2     | SAMSUNG Galaxy A73 5G (Awesome Mint, 256 GB) \| \$20537.0 \| Rating: 4.2 |

penjelasan:

Hasil dari code diatas menunjukan bahwa true positive: 9 dan precision = 0.90 yang artinya dari hasil rekomendasi berdasarkan name, price, ratings, dan corpus berhasil memberikan rekomendasi sesuai sebanyak 9 rekomendasi dan tidak sesuai 1 rekomendasi.
