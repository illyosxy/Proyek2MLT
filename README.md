# Proyek2MLT - Book Recomendation
Proyek kedua Membuat Model Sistem Rekomendasi untuk memenuhi submission Dicoding

## Project Overview

Di era digital ini, informasi bagaikan arus deras yang tak terbendung dimana kita dihadapkan dengan lautan informasi yang begitu luas dan mengalir deras. Bagi kebanyakan orang, situasi ini dapat menimbulkan perasaan kewalahan. Tanpa kemampuan untuk memilah dan menyaring informasi, kita berisiko tenggelam dalam arus data yang tak berkesudahan dan menghabiskan waktu berharga di internet. <br/> <br/>
Era digital menghadirkan dua sisi mata uang yakni Kemudahan Akses Informasi dan Banjir Informasi. Kemudahan akses informasi menyebabkan data menjadi melimpah, mudah, dan cepat diperoleh serta memudahkan pencarian informasi dan membuka berbagai peluang. Sedangkan Banjir informasi menyebabkan Data yang melimpah tidak selalu berkualitas baik dan kita kesulitan untuk memilih dan memilah informasi.
Teknologi machine learning menjadi kunci dalam pengembangan sistem rekomendasi yang efektif. Machine learning memungkinkan sistem untuk mempelajari pola dan preferensi pengguna berdasarkan data interaksi dan riwayat pencarian serta memberikan rekomendasi yang sesuai dengan minat pengguna. Penerapan sistem rekomendasi buku dalam era digital menawarkan beberapa manfaat seperti meningkatkan engagement serta dapat meningkatkan penjualan. <br/> <br/>
Sistem rekomendasi buku berbasis machine learning merupakan solusi yang tepat untuk membantu pengguna dalam menghadapi arus informasi di era digital. Dengan kemampuannya untuk menyaring data dan memberikan rekomendasi yang dipersonalisasi, sistem ini dapat meningkatkan engagement, dan penjualan.

## Business Understanding

Secara umum, sistem rekomendasi merupakan sebuah sistem yang ditujukan untuk menyarankan sesuatu yang relevan kepada pengguna seperti sebuah produk, film, hingga tempat wisata. Sistem rekomendasi sangat penting di beberapa industri karena dapat menghasilkan pendapatan dalam jumlah besar ketika efisien.

### 1. Problem Statements
Bagaimana memberikan rekomendasi yang efektif dan cepat kepada pengguna?

### 2. Goals
Tujuan dari proyek ini adalah untuk menghasilkan sistem rekomendasi yang dapat memberikan saran ataupun rekomendasi yang memudahkan pengguna dengan efektif dan efisien.

### 3. Solution Approach
Terdapat dua solusi untuk mencapai tujuan diatas yaitu penggunaan pendekatan "Content Based Filtering" dan "Collaborative Filtering". Pendekatan ini dipilih karena kedua pendekatan ini dapat menjadi solusi yang saling melengkapi. Ide dari Content Based Filtering adalah merekomendasikan sesuatu yang mirip dengan sesuatu yang disukai pengguna di masa lalu. Sedangkan Collaborative Filtering bergantung pada pendapat komunitas atau grup yang dimiliki oleh pengguna. Pada projek ini saya menerapkan metode berbasis model Machine Learning yang bekerja dengan membangun 3 tipe layer yaitu input layer, hidden layer dan output layer agar dapat menemukan pola yang optimal dalam mengeneralisasi data.

## Data Understanding
Dataset yang digunakan dalam proyek ini merupakan data rekomendasi buku yang dapat diunduh di [Kaggle - Book Recommendation Dataset](https://www.kaggle.com/datasets/arashnic/book-recommendation-dataset). 

### 1. Informasi dan Uraian Data

Terdapat 3 buah File yang akan digunakan dalam proyek kali ini yaitu Users, Books, dan Ratings. File tersebut memiliki format CSV.

- File Users yang berisi informasi berikut:
   * `User-ID` : Nomor identitas pengguna.
   * `Location` : Lokasi pengguna
   * `Age` : Umur Pengguna

- File Books yang berisi informasi berikut:
   * `ISBN` : International Standard Book Number adalah kode identifikasi buku yang bersifat unique
   * `Book-Title` : Judul buku 
   * `Book-Author` : Penulis buku
   * `Year-Of-Publication` : Tahun publikasi buku
   * `Image-URL-S` : Link untuk melihat gambar kecil dari buku 
   * `Image-URL-M` : Link untuk melihat gambar sedang dari buku
   * `Image-URL-L` : Link untuk melihat gambar besar dari buku

- File Ratings yang berisi informasi berikut:
   * `User-ID` : Nomor identitas pemberi rating
   * `ISBN` : International Standard Book Number adalah kode identifikasi buku yang bersifat unique
   * `Book-Rating` : Rating yang diberikan pengguna

### 2. Exploratory Data Analysis (EDA)

  - Book-Title
    * Jumlah Judul Buku :  242135
    * Jumlah Nomor ISBN Buku :  271360
      -  Terdapat perbedaan jumlah antara Judul buku dan nomor ISBN.
      -  Nomor ISBN cenderung bersifat unik bagi setiap buku.
      -  Perbedaan jumlah ini disebabkan terdapat judul buku yang sama persis namun berbeda secara isi atau/dan penulis.
  
  - Book-Author
    * Jumlah Penulis Buku :  102024
    * Jumlah Nomor ISBN Buku :  271360
      -  Terdapat 102.024 jumlah penulis dari 271.360 jenis buku yang berbeda.
      -  Terdapat beberapa buku yang ditulis oleh penulis yang sama.
  
  - Jumlah rating yang diberikan :  1149780

  - Jumlah Buku Yang Diberi Rating : 340556

  - Jumlah pengguna yang memberikan rating :  105283

## Data Preparation :

### 1. Data Merge
Pada langkah ini digabungkan data pada file rating dan books berdasarkan kolom `ISBN` dengan fungsi `merge()` agar pada satu data memiliki informasi lengkap berupa buku dan rating.

### 2. Mengecek dan Mengatasi Missing Value
Pada langkah Selanjutnya, dibuang baris data yang meiliki missing value dengan fungsi `dropna()` agar ketika proses pelatihan model tidak terdapat informasi yang hilang.

## Content Based Filtering :

### 1. Cutting Dataset 
Pada proyek kali ini hanya menggunakan 10.000 baris data saja karena keterbatasan komputasi.

### 2. Data Conversion
Proses ini menggunakan fungsi `tolist()` untuk memenuhi persyaratan input TF-IDF Vectorizer yaitu input list.

### 3. Making Dictionary
Proses ini menghasilkan sebuah data baru hasil keseluruhan proses sebelumnya. Data disimpan pada variable books_new.

## Modelling (Content Based Filtering)

Pendekatan ini bekerja dengan melihat kemiripan suatu konten seperti judul buku dan lain sebagainya. Model ini akan menghitung tingkat kemiripan antar judul buku lalu memberikan hasil rekomendasi buku kepada pengguna dengan judul buku yang memiliki tingkat kemiripan yang paling tinggi. Model ini menjadi solusi dalam menghasilkan sistem rekomendasi yang efektif dan efisien.

### 1. TF-IDF Vectorizer
Teknik ini bertujuan untuk mengukur seberapa penting suatu kata terhadap kata-kata lain dalam dokumen. Teks yang berbeda dalam sebuah konten mungkin memiliki panjang yang berbeda, tergantung dari panjang dokumen. Oleh karena itu diperlukan proses normalisasi menggunakan fungsi ` TfidfVectorizer()`. Fitur judul buku lebih relevan dalam memberikan rekomendasi berdasarkan kemiripan. Setelah itu dilakukan proses transformasi ke bentuk matrix dengan fungsi `fit_transform()`. Setelah itu, untuk menghasilkan vektor tf-idf dalam bentuk matriks digunakan fungsi `todense()`. Proses ini diperlukan untuk dapat menghitung tingkat kemiripan judul buku.

### 2. Cosine Similarity
Cosine similarity digunakan untuk mengukur kesamaan antara dua vektor dan menentukan apakah kedua vektor tersebut menunjuk ke arah yang sama. Dalam proyek ini, cosine similarity digunakan untuk mengukur kesamaan nama judul buku.
Proses ini menggunakan fungsi `cosine_similarity()`. Pada tahapan ini, dihitung cosine similarity pada dataframe `tfidf_matrix` yang diperoleh pada tahapan TD-IDF Vectorizer sebelumnya. Proses ini menghasilkan output berupa matriks kesamaan dalam bentuk array. 

### 3. Menyajikan Top-N Recommendation
Selanjutnya yaitu membuat sebuah fungsi yang dapat memberi hasil rekomendasi dengan parameter fungsi yang terdiri dari fitur ISBN dan cosine_sim_df yang didapatkan pada langkah sebelumnya. Cara kerja fungsi ini adalah Mengambil data dengan menggunakan `argpartition()`, kemudian mengubah dataframe menjadi numpy dan membuat range yang terdiri dari `range(start, stop, step)`. Setelah itu, mengambil data dengan similarity terbesar dari index yang ada dan menghapus nama buku yang dimasukan oleh pengguna sehingga tidak merekomendasikan nama buku yang sama dengan yang dimasukan pengguna melalui fungsi `drop()`. Setelah itu akan mengembalikan dalam bentuk dataframe.

Berikut hasil rekomendasi dari buku dengan ISBN `0380898179` :

- **Data Buku `0380898179`** :

| id | ISBN | Book Author | Book Title |
|--|---|:---:|---|
| 5326 |	0380898179 |	Kathleen E. Woodiwiss |	So Worthy My Love |

- **5 Rekomendasi Buku, Berdasarkan Konten Buku `0380898179`**

| No | ISBN | Book Author | Book Title |
|--|---|:---:|---|
| 0	| 0380761483 |	Kathleen E. Woodiwiss |	So Worthy My Love |
| 1	| 0375409440 | TONI MORRISON |	Love |
| 2	| 0380792540 | Tamar Myers	| So Faux, So Good (Den of Antiquity) |
| 3	| 0671737643 |	Judith McNaught |	Whitney, My Love |
| 4	| 0800786289 |	David B. Biebel	| If God Is So Good, Why Do I Hurt So Bad? |

Dari gambar di atas terlihat kita ingin mencari rekomendasi dari buku yang berjudul So Worthy My Love dan sistem kita sudah dapat merekomendasikan judul buku yang serupa dengan keyword 'My Love' dan 'So'.

## Collaborative Filtering :

### 1. Encoding
Mengubah `userID` menjadi list tanpa nilai yang sama dengan fungsi `unique()` dan `tolist()` serta menyimpannya dalam variabel `user_ids`. Setelah itu,  Melakukan encoding `user_ids` ke dalam indeks integer dan Melakukan proses encoding angka ke ke `user_ids`. Begitu juga sama untuk `ISBN`.

### 2. Feature Mapping
Tahap dilakukan agar data siap digunakan untuk pemodelan.

### 3. Membagi Data untuk Training dan Validasi
Tahap ini membagi dataset menjadi 80% data train dan 20% data test.

## Modelling (Collaborative Filtering)

Model ini bekerja dengan mengidentifikasi buku yang mirip dan tidak pernah dibeli pengguna dengan pertimbangan rating yang telah diberikan sebelumnya. Model ini menjadi solusi dalam menghasilkan sistem rekomendasi yang efektif dan efisien karena mempertimbangkan preferensi pengguna dan hanya hitungan detik dalam memberikan rekomendasi.

### 1. RecommenderNet
Pertama, dilakukan proses embedding terhadap data pengguna dan buku. Selanjutnya, dilakukan operasi perkalian dot product antara embedding pengguna dan buku. Selain itu, kita juga dapat menambahkan bias untuk setiap pengguna dan buku. Skor kemiripan ditetapkan dalam skala [0,1].

### 2. Compiling 
Dilakukan inisiasi model menggunakan RecommenderNet yang telah dibuat sebelumnya dengan variabel yang berisi jumlah pengguna dan buku serta ukuran embedding. Setelah itu, dilakukan proses compiling model. Model ini menggunakan *Binary Crossentropy* untuk menghitung *loss function*, *Adam* sebagai *optimizer*, dan *root mean squared error* (RMSE) sebagai *metrics evaluation*. 

### 3. Training
Parameter training yang digunakan adalah `x`, `y`, `batch_size = 64`, `epochs = 100`, `validation_data = (x_val, y_val)` dan `callbacks = [reduce_lr, early_stop]`.

### 4. Top-N Recommendation
Berikut hasil rekomendasi untuk user id `241191` :

- **Books with High Ratings from User**

| ISBN | Book Title | Rating |
|---|---|---|
| 0002550156 | I hope [Raisa Maksimovna Gorbacheva] | 5.0 |
| 0812885066 | The Only Astrology Book You'll Ever Need [Joanna Martine Woolfolk] | 0.0 |
| 0385479565 | The Hot Zone [Richard Preston] | 6.0 |
| 0586043756 | The Road to Gandolfo [Michael Shepherd] | 7.0 |
| 0743411447 | Jolie Blon's Bounce [James Lee Burke] | 0.0 |


- **Top 10 Books Recommendation**

| ISBN | Book Title | Rating |
|---|---|---|
| 0091842050 | The Blue Day Book: A Lesson in Cheering Yourself Up [Bradley Trevor Greive] | 10.0 |
| 0394800389 | Fox in Socks (I Can Read It All by Myself Beginner Books) [Dr. Seuss] | 10.0 |
| 0823401898 | The Shrinking of Treehorn [Florence Parry Heide] | 10.0 |
| 1563891336 | Death: The High Cost of Living [Neil Gaiman] | 10.0 |
| 3522128001 | Die unendliche Geschichte: Von A bis Z [Michael Ende] | 10.0 |
| 0920668364 | Love You Forever [Robert Munsch] | 9.5 |
| 0316779059 | The Baby Book: Everything You Need to Know About Your Baby from Birth to Age Two [Martha Sears] | 9.0 |
| 1844262553 | Free [Paul Vincent] | 9.0 |
| 2205054252 | Le Combat ordinaire, tome 1 [Larcenet] | 9.0 |
| 0064440508 | A Kiss for Little Bear [Else Holmelund Minarik] | 8.5 |

## Kelebihan dan Kekurangan Setiap Pendekatan

### Content Based Filtering

- **Kelebihan** : Model dapat memberikan rekomendasi yang serupa dengan buku yang telah kita beli sehingga relatif dapat membeli buku yang tepat dan telah terbukti diminati kita karena berdasarkan kemiripan judul buku di masa lalu.

- **Kekurangan** : Cenderung model hanya memberikan rekomendasi buku yang mirip atau relatif bukan buku yang unik.

### Collaborative Filtering

- **Kelebihan** : Model dapat memberikan rekomendasi yang lebih unik karena mempertimbangkan segi preferensi (rating) bukan konten yang pernah dibeli pengguna dan relatif masih disukai oleh konsumen karena memiilki rating serupa dengan buku yang pernah dibeli. 

- **Kekurangan** : Cenderung model hanya memberikan rekomendasi buku unik dan kemungkinan tidak disukai konsumen karena belum terbukti diminati sebab tidak berdasarkan kemiripan judul buku di masa lalu.

## Evaluation

### 1. Model Content Based Filtering

Formula metrik Recomender System Precision (RSP) ini adalah sebagai berikut :

$$RSP = R_R/R_A$$

Keterangan : 

$R_R$ = Jumlah rekomendasi yang relevan

$R_A$ = Jumlah keseluruhan rekomendasi yang prediksi model


Cara kerja metrik ini adalah dengan membandingkan seberapa banyak prediksi model yang relevan atau sesuai dengan keseluruhan rekomendasi yang telah diberikan. 

Berikut hasil rekomendasi dari buku dengan ISBN `0380898179` :

- **Data Buku `0380898179`** :

| id | ISBN | Book Author | Book Title |
|--|---|:---:|---|
| 5326 |	0380898179 |	Kathleen E. Woodiwiss |	So Worthy My Love |


- **5 Rekomendasi Buku, Berdasarkan Konten Buku `0380898179`**

| No | ISBN | Book Author | Book Title |
|--|---|:---:|---|
| 0	| 0380761483 |	Kathleen E. Woodiwiss |	So Worthy My Love |
| 1	| 0375409440 | TONI MORRISON |	Love |
| 2	| 0380792540 | Tamar Myers	| So Faux, So Good (Den of Antiquity) |
| 3	| 0671737643 |	Judith McNaught |	Whitney, My Love |
| 4	| 0800786289 |	David B. Biebel	| If God Is So Good, Why Do I Hurt So Bad? |

Sehingga presisi sistem rekomendasi *Content Based Filtering* pada sampel ini adalah 5/5 = 100%.

### 2. Model Collaborative Filtering

Formula metrik Root Mean Squared Error (RMSE) adalah sebagai berikut :

$$RMSE = \sqrt{\sum{(Y_t - Y_p)^2} \over n}$$

Keterangan :

$Y_t$ = Y true

$Y_p$ = Y predict

n = jumlah data

Cara kerja metrik ini adalah dengan menyelisihkan nilai aktual dengan nilai prediksi lalu dikuadratkan kemudian ditotalkan dengan seluruh data dan selanjutnya dibagi dengan jumlah data, terakhir diakarkan. 

<div><img src="https://github.com/illyosxy/Proyek2MLT/assets/144518223/46713f31-36c0-439c-b4f7-7247f1d74c13"/></div>

Jika dilihat dari performa model *Collaborative Filtering* maka model ini sudah cukup bagus karena cenderung memiliki error yang menurun dan relatif stabil seiring pertambahan epochs. Selain itu, model dapat dikatakan cukup *good fit*, kemudian relatif hasil RMSE *training* dan validasi sudah baik untuk kasus sistem rekomendasi.

## Conclusion

Pada projek ini dapat disimpulkan bahwa sistem ini telah berhasil menyelesaikan masalah bisnis dan mencapai tujuan yang ada melalui pembangunan model dengan 2 pendekatan yaitu **Content Based Filtering** dan **Collaborative Filtering**. Yang mana kedua pendekatan ini relatif dapat saling melengkapi dalam rangka mengoptimalkan performa sistem rekomendasi dalam memberikan rekomendasi yang efektif dan efisien. 

## Reference

[1] P. Mathew, B. Kuriakose and V. Hegde, "Book Recommendation System through content based and collaborative filtering method," 2016 International Conference on Data Mining and Advanced Computing (SAPIENCE), Ernakulam, India, 2016, pp. 47-52, doi: 10.1109/SAPIENCE.2016.7684166. <br/>
[2] Yiu-Kai Ng. 2020. CBRec: a book recommendation system for children using the matrix factorisation and content-based filtering approaches. Int. J. Bus. Intell. Data Min. 16, 2 (2020), 129–149. https://doi.org/10.1504/ijbidm.2020.104738
